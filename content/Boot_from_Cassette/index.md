---
title: Boot from Cassette
---
# Casette boot  
  
## CAS Image  
- [Binary_Loader_BL-C_0.2.cas](attachments/Binary_Loader_BL-C_0.2.cas) ; CAS image of a boot loader, which afterwards enables the Atari to load a binary file. Please hold START pressed when booting and press RETURN after the beep.  
  
  
What is a bootable program ?  
  
A bootable program is a program which will be automatically loaded at powering up the  
ATARI, and directly after loading be executed.  
  
A bootable program needs a header with specific information about the program, such as the  
length and the start address. The header of a bootable program looks like the following  
scheme:  
  
![](attachments/casboot.png)  
  
  
  
- The first byte is unused, and should equal zero.  
- The second  byte contains the length of the program, in records (128  bytes, rounded up).  
- The next word contains the store-address of the program.  
- The last word contains the initialization-address of the program. This vector will be transferred to the CASINI-vector ($02,$03).  
  
After these 6 bytes there has to be the boot continuation code. This is a short program the OS will jump to directly after loading. This program can continue the boot process (multi-stage boot) or stop the cassette by the following sequence  
  
```
LDA #$3C 
STA PACTL ;$D302
```
  
The program then allows the DOSVEC ($0A, $0B) to point to the start address of the program. It is also possible to store in MEMLO ($02E7, $02E8), the first unused memory address. The continuation code must return to the OS with C=0 (Carry clear). Now OS jumps via DOSVEC to the application program.  
  
So far we know what a bootable cassette looks like, but how do we create such a bootable tape?  
  
If there is a program, we only have to put the header in front of it (including the continuation code) and to save it as normal data on the tape. We can use the later described program to write the contents of a buffer on the tape or the boot generator.  
  
If the program is saved, we can put the tape in the recorder, press the yellow START-key, power on the ATARI and press RETURN. Now the program on the tape will be booted.  
  
The next listing shows us the general outline of a bootable program.  
  
```
; general outline of an
; bootable program

; start of program
        ORG  $700    ; or any other address

; the booloader datastructure

START   DFB 0        ; byte 1 always 0
        DFB END-START+127/128  ; num or sectors
        DFW START      ; target address
        DFW INIT     ; init address

; boot continuation code

        LDA #$3C
        STA PACTL     ; stop cassette motor

        LDA #END:L    ; low bye free location
        STA MEMLO
        LDA #END:H    ; high byte free location
        STA MEMLO+1

        LDA #RESTART:L  ; restart vector
        STA DOSVEC
        LDA #RESTART:H
        STA DOSVEC+1

        CLC             ; everything OK
        RTS             ; return to OS

; init code

INIT    RTS

; the main program

RESTART ...
        RTS

; end of main program

END     EQU *

```
  
Making a bootable disk is in fact the same as for the cassette. The only exceptions are as follows.  
  
The program (including the header) must be stored up from sector one. The boot continuation code doesn't need to switch off anything such as the cassette motor.  
  
How to create a bootable disk?  
  
This is only a bit more complicated than the cassette version. We have to write the program, sector by sector, to disk. You can also make a bootable cassette first and then copy it directly to disk.  
