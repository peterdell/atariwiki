# Speedlink Competition Pro USB  
  
  
Tested with a Speedlink Competition Pro USB. Might work with other digital gamepads. String descriptor returns "Gamepad".  
  
## Description  
  
|| USB Register || Byte of HID Packet || Function || Atari Memory Shadow || original Label || new USB label ||  
|  $10           |  1                 | Horizontal Movement (left/right)  | $270 (624)  | PADDL0 | JHORIZ     |  
|  $11           |  2                 | Vertical Movement (up/down) | $271 (625)  | PADDL1 | JVERT     |  
|  $12           |  3                 | Buttons 1-4  | $272 (626)  | PADDL2 | JBUTTON     |  
  
  
### Byte 3: Buttons  
  
|| Bit  || Button  ||  
|  1   |   1     |  
|  2   |   2     |  
|  3   |   3     |  
|  4   |   4     |  
  
  
## Device dependent source  
  
This Source must be included into the [Base HID Driver](../BaseHIDDriver/index.md).  
  
```
01000          .LI OFF
01010 ****************************
01020 ** 6502 USB DEVELOPMENT   **
01030 ** (C) 2005 BY ABBUC      **
01040 ** REGIONALGRUPPE FFM     **
01050 ** DEVICE DRIVER FOR      **
01060 ** COMPETITON PRO USB     **
01070 ** VERSION 1.0 20050111   **
01080 ** LICENSED UNDER THE     **
01090 ** GNU PUBLIC LICENSE     **
01100 ** (GPL) VERS. 2 OR LATER **
01110 **                        **
01120 ****************************
01130 ; THIS FILE MUST BE INCLUDED
01140 ; FROM USBHID.SRC!
01150 ;
01160 ; ATARI MEMORY LOCATIONS
01170 ;
01180 STICK0   = $0278
01190 STICK1   = $0279
01200 STRIG0   = $0284
01210 STRIG1   = $0285
01220 ;
01230 ; USB JOYSTICK SHADOW REGISTER
01240 ;
01250 JHORIZ   = $0270
01260 JVERT    = $0271
01270 JBUTTON  = $0272
01280 ;
01290 ------------------------------
01300 POLLDEVICE
01310 ;
01320          LDA #03
01330          JSR PROCESS
01340 ;        AND #01
01350 ;        BEQ .2  ; NO DATA
01360 ;
01370          LDX #$10
01380          JSR REGFETCH
01390          STA JHORIZ
01400 ;
01410          LDX #$11
01420          JSR REGFETCH
01430          STA JVERT
01440 ;
01450          LDX #$12
01460          JSR REGFETCH
01470          STA JBUTTON
01480 ;
01490 .2       RTS
01500 ------------------------------
01510 USB2ATA
01520          LDA #$0F
01530          STA STICK0
01540          LDA #1
01550          STA STRIG0
01560 ;
01570          LDA JBUTTON
01580          BEQ GETSTICK
01590          LDA #0
01600          STA STRIG0
01610 ;
01620 GETSTICK
01630          LDA STICK0
01640          LDX JHORIZ
01650          CPX #$80
01660          BEQ .10  ; NOTHING
01670          BCC .2   ; LEFT
01680          EOR #$08 ; RIGHT
01690          BPL .3
01700 .2       EOR #$04 ; LEFT
01710 .3       STA STICK0
01720 .10
01730          LDX JVERT
01740          CPX #$80
01750          BEQ .20  ; NOTHING
01760          BCC .12  ; UP
01770          EOR #$02 ; DOWN
01780          BPL .13
01790 .12      EOR #$01 ; UP
01800 .13      STA STICK0
01810 .20      RTS
01820 ------------------------------
01860 VBI
01870          LDA STICK0
01880          EOR #$0F
01890          BNE .1
01900          LDA STRIG0
01910          BEQ .1
01920 ;
01930          JSR POLLDEVICE
01940          JSR USB2ATA
01950 .1       JMP XITVBV
01960 ------------------------------
01970          .OR $7400
01980 ------------------------------
01990 PRINTDEVICE
02000          JSR PRINT
02010          .AS "COMPETITION PRO USB Driver"
02020          .HX 40
02030          RTS
02040 ------------------------------
02050 PRINTVERSION
02060          JSR PRINT
02070          .AS "Version 1.0 "
02080          .HX 40
02090          RTS
02100 ------------------------------
02110 PRINTCOPY
02120          JSR PRINT
02130          .AS "(c) 20050111 C. Strotmann/ABBUC"
02140          .HX 40
02150          RTS
02160 ------------------------------
```
  
  
