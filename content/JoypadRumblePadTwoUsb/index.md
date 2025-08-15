---
title: JoypadRumblePadTwoUsb
---
# Logitech Rumblepad 2 USB Driver  
  
  
  
Tested with a Logitec Rumblepad 2 USB. Other Logitech analog Joypad might work. Please send feedback.  
  
## Description  
  
  
|| USB Register || Byte of HID Packet || Function || Atari Memory Shadow || original Label || new USB label ||  
|  $10           |  1                 | left handle horiz movement  | $270 (624)  | PADDL0 | RPADLHH     |  
|  $11           |  2                 | left handle vertic movement | $271 (625)  | PADDL1 | RPADLHV     |  
|  $12           |  3                 | right handle horiz movement  | $272 (626)  | PADDL2 | RPADRHH     |  
|  $13           |  4                 | right handle vertic movement | $273 (627)  | PADDL3 | RPADRHV     |  
|  $14           |  5 Bit 0-4         | digital Joypad | $274 (628)  | PADDL4 | RPADDJY     |  
|  $14           |  5 Bit 5-7         | Button 1-4 | $275 (629)  | PADDL5 | RPADBUT1  |  
|  $15           |  6                 | Button 5-10 | $276 (630)  | PADDL6 | RPADBUT2  |  
|  $16           |  7                 | Mode Button Status | $277 (631)  | PADDL7 | RPADMODE  |  
  
  
- Byte 1: left handle horizontal movement ($00 = left, $80 = middle, $FF= right)  
- Byte 2: left handle vertical movement ($00 = up, $80 = middle, $FF= down)  
- Byte 3: right handle horizontal movement ($00 = left, $80 = middle, $FF= right)  
- Byte 4: right handle vertical movement ($00 = up, $80 = middle, $FF= down)  
- Byte 5: Bit 0-3 digital Joypad (see below)  
- Byte 5: Bit 4 - Button 1, Bit 5 - Button 2, Bit 6 - Button 3, Bit 7 - Button 8  
- Byte 6: Bit 0-5 - Button 5-10  
- Byte 7: Bit 2 - Vibration Switch, Bit 3 - Mode Switch and LED  
- Byte 8: unknown  
  
The digital Joypad has a unique value for each direction:  
```
.
          up
          0
        7 | 1
left  6---8---2 right
        5 | 3
          4
         down
```
  
## Device dependent source  
  
### Digital Disk Control Driver  
  
This Source must be included into the [Base HID Driver](../BaseHIDDriver/index.md).  
  
```
01000          .LI OFF
01010 ****************************
01020 ** 6502 USB DEVELOPMENT   **
01030 ** (C) 2004 BY ABBUC      **
01040 ** REGIONALGRUPPE FFM     **
01050 ** DEVICE DRIVER FOR      **
01060 ** LOGITECH RUMBLE PAD 2  **
01070 ** VERSION 1.0 20041214   **
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
01250 RPADLHH  = $0270
01260 RPADLHV  = $0271
01270 RPADRHH  = $0272
01280 RPADRHV  = $0273
01290 RPADDJY  = $0274
01300 RPADBUT1 = $0275
01310 RPADBUT2 = $0276
01320 RPADMODE = $0277
01330 ;
01340 ------------------------------
01350 POLLDEVICE
01360 ;
01370          LDA #03
01380          JSR PROCESS
01390 ;        AND #01
01400 ;        BEQ .2  ; NO DATA
01410 ;
01420          LDX #$14
01430          JSR REGFETCH
01440          PHA         ; SAVE VALUE TO STACK
01450          AND #$0F    ; CLEAR TO NIBBLE BIT 4-7
01460          STA RPADDJY
01470          PLA         ; RESTORE VALUE FROM STACK
01480          LSR         ; MOVE TOP NIBBLE
01490          LSR         ; DOWN
01500          LSR
01510          LSR
01520          STA RPADBUT1 ; STORE IN SHADOW
01530 ;
01540          LDX #$15
01550          JSR REGFETCH
01560          STA RPADBUT2
01570 ;
01580 .2       RTS
01590 ------------------------------
01600 USB2ATA
01610          LDA #$0F
01620          STA STICK0
01630          LDA #1
01640          STA STRIG0
01650 ;
01660          LDA RPADBUT1
01670          ORA RPADBUT2
01680          BEQ GETSTICK1
01690          LDA #0
01700          STA STRIG0
01710 ;
01720 GETSTICK1
01730          LDY RPADDJY
01740          LDA JOYTAB,Y
01750          STA STICK0
01760          RTS
01770 ------------------------------
01780 JOYTAB   .DA #14,#6,#7,#5,#13,#9,#11,#10,#15
01790 ------------------------------
01800 VBI
01810          LDA STICK0
01820          EOR #$0F
01830          BNE .1
01840          LDA STRIG0
01850          BEQ .1
01860 ;
01870          JSR POLLDEVICE
01880          JSR USB2ATA
01890 .1       JMP XITVBV
01900 ------------------------------
01910          .OR $7400
01920 ------------------------------
01930 PRINTDEVICE
01940          JSR PRINT
01950          .AS "Logitech Rumblepad 2 Driver"
01960          .HX 40
01970          RTS
01980 ------------------------------
01990 PRINTVERSION
02000          JSR PRINT
02010          .AS "Version 1.0 (DIGITAL)   "
02020          .HX 40
02030          RTS
02040 ------------------------------
02050 PRINTCOPY
02060          JSR PRINT
02070          .AS "(c) 20041214 C. Strotmann/ABBUC"
02080          .HX 40
02090          RTS
02100 ------------------------------
```
  
### Analog Handle Driver  
  
This Source must be included into the [Base HID Driver](../BaseHIDDriver/index.md).  
  
```
01000          .LI OFF
01010 ****************************
01020 ** 6502 USB DEVELOPMENT   **
01030 ** (C) 2004 BY ABBUC      **
01040 ** REGIONALGRUPPE FFM     **
01050 ** DEVICE DRIVER FOR      **
01060 ** LOGITECH RUMBLE PAD 2  **
01070 ** VERSION 1.0 20041213   **
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
01250 RPADLHH  = $0270
01260 RPADLHV  = $0271
01270 RPADRHH  = $0272
01280 RPADRHV  = $0273
01290 RPADDJY  = $0274
01300 RPADBUT1 = $0275
01310 RPADBUT2 = $0276
01320 RPADMODE = $0277
01330 ;
01340 ------------------------------
01350 ; THRESHOLD ANALOG->DIGITAL
01360 THLEFT   .HX 60
01370 THRIGHT  .HX A0
01380 THUP     .HX 60
01390 THDOWN   .HX A0
01400 ------------------------------
01410 POLLDEVICE
01420 ;
01430          LDA #03
01440          JSR PROCESS
01450 ;        AND #01
01460 ;        BEQ .2  ; NO DATA
01470 ;
01480          LDX #$10
01490          JSR REGFETCH
01500          STA RPADLHH
01510          LDX #$11
01520          JSR REGFETCH
01530          STA RPADLHV
01540          LDX #$12
01550          JSR REGFETCH
01560          STA RPADRHH
01570          LDX #$13
01580          JSR REGFETCH
01590          STA RPADRHV
01600          LDX #$14
01610          JSR REGFETCH
01620          PHA         ; SAVE VALUE TO STACK
01630          AND #$0F    ; CLEAR TO NIBBLE BIT 4-7
01640          STA RPADDJY
01650          PLA         ; RESTORE VALUE FROM STACK
01660          LSR         ; MOVE TOP NIBBLE
01670          LSR         ; DOWN
01680          LSR
01690          LSR
01700          STA RPADBUT1 ; STORE IN SHADOW
01710 ;
01720          LDX #$15
01730          JSR REGFETCH
01740          STA RPADBUT2
01750 ;
01760          LDX #$16
01770          JSR REGFETCH
01780          STA RPADMODE
01790 ;
01800 .2       RTS
01810 ------------------------------
01820          .OR $0400
01830 USB2ATA
01840          LDA #$0F
01850          STA STICK0
01860          STA STICK1
01870          LDA #1
01880          STA STRIG0
01890          STA STRIG1
01900 ;
01910          LDA RPADBUT1
01920          ORA RPADBUT2
01930          BEQ GETSTICK1
01940          LDA #0
01950          STA STRIG0
01960          STA STRIG1
01970 ;
01980 GETSTICK1
01990          LDA STICK0
02000          LDX RPADLHH
02010          CPX THLEFT
02020          BCC .1   ; LEFT
02030          CPX THRIGHT
02040          BCS .2   ; RIGHT
02050          BCC .10
02060 .1       EOR #$04 ; LEFT
02070          BPL .3
02080 .2       EOR #$08 ; RIGHT
02090 .3       STA STICK0
02100 .10
02110          LDX RPADLHV
02120          CPX THUP
02130          BCC .11  ; UP
02140          CPX THDOWN
02150          BCS .12  ; DOWN
02160          BCC GETSTICK2
02170 .11      EOR #$01 ; UP
02180          BNE .13
02190 .12      EOR #$02 ; DOWN
02200 .13      STA STICK0
02210 GETSTICK2
02220          LDA STICK1
02230          LDX RPADRHH
02240          CPX THLEFT
02250          BCC .1   ; LEFT
02260          CPX THRIGHT
02270          BCS .2   ; RIGHT
02280          BCC .10
02290 .1       EOR #$04 ; LEFT
02300          BPL .3
02310 .2       EOR #$08 ; RIGHT
02320 .3       STA STICK1
02330 .10
02340          LDX RPADRHV
02350          CPX THUP
02360          BCC .11  ; UP
02370          CPX THDOWN
02380          BCS .12  ; DOWN
02390          BCC .20
02400 .11      EOR #$01 ; UP
02410          BNE .13
02420 .12      EOR #$02 ; DOWN
02430 .13      STA STICK1
02440 .20      RTS
02450 ------------------------------
02460 VBI
02470          LDA STICK0
02480          EOR #$0F
02490          BNE .1
02500          LDA STRIG0
02510          BEQ .1
02520 ;
02530          JSR POLLDEVICE
02540          JSR USB2ATA
02550 .1       JMP XITVBV
02560 ------------------------------
02570          .OR $7400
02580 ------------------------------
02590 PRINTDEVICE
02600          JSR PRINT
02610          .AS "Logitech Rumblepad 2 Driver"
02620          .HX 40
02630          RTS
02640 ------------------------------
02650 PRINTVERSION
02660          JSR PRINT
02670          .AS "Version 1.0"
02680          .HX 40
02690          RTS
02700 ------------------------------
02710 PRINTCOPY
02720          JSR PRINT
02730          .AS "(c) 20041213 C. Strotmann/ABBUC"
02740          .HX 40
02750          RTS
02760 ------------------------------

```
