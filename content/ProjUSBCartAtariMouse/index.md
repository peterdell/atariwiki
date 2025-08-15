---
title: ProjUSBCartAtariMouse
---
# Generic USB Mouse Driver  
  
  
Tested with a Logitech Mouse USB. Might work with other mice.  
  
## Description  
  
|| USB Register || Byte of HID Packet || Function || Atari Memory Shadow || original Label || new USB label ||  
|  $10           |  1                 | Buttons  | $06F2  | -- | MBUTTON     |  
|  $11           |  2                 | Vertical displacement (up/down) | $06F1  | -- | MVERT     |  
|  $12           |  3                 | Horizontal displacement (left/right)  | $06F0  | -- | MHORIZ     |  
|  $13           |  4                 | Wheel  | $06F3  | -- | MWHEEL     |  
  
- Byte 3: Buttons  
|| Bit  || Button  ||  
|  1   |   left     |  
|  2   |   right     |  
|  3   |   middle     |  
  
  
- Byte 4 - Wheel  
|| Value  || Button  ||  
|  $FF (255)   |   up     |  
|  $01 (001)   |   down     |  
  
  
## Device dependent source  
  
This Source must be included into the [Base HID Driver](../BaseHIDDriver/index.md).  
  
```
01000          .LI OFF
01010 ****************************
01020 ** 6502 USB DEVELOPMENT   **
01030 ** (C) 2005 BY ABBUC      **
01040 ** REGIONALGRUPPE FFM     **
01050 ** DEVICE DRIVER FOR      **
01060 ** USB MOUSE (GENERIC)    **
01070 ** VERSION 1.0 20050121   **
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
01230 XM       = $06F4
01240 YM       = $06F5
01250 SDMCTL   = $022F
01260 PMBASE   = $D407
01270 GRACTL   = $D01D
01280 HPOS0    = $D000
01290 PCOL0    = $02C0
01300 GPRIOR   = $026F
01310 ;
01320 ; USB JOYSTICK SHADOW REGISTER
01330 ;
01340 MHORIZ   = $06F0
01350 MVERT    = $06F1
01360 MBUTTON  = $06F2
01370 MWHEEL   = $06F3
01380 ;
01390 ------------------------------
01400 POLLDEVICE
01410 ;
01420          LDA #03
01430          JSR PROCESS
01440          AND #01
01450          BEQ .2  ; NO DATA
01460 ;
01470          LDX #$10
01480          JSR REGFETCH
01490          STA MBUTTON
01500 ;
01510          LDX #$11
01520          JSR REGFETCH
01530          STA MVERT
01540 ;
01550          LDX #$12
01560          JSR REGFETCH
01570          STA MHORIZ
01580 ;
01590          LDX #$13
01600          JSR REGFETCH
01610          STA MWHEEL
01620 ;
01630 .2       RTS
01640 ------------------------------
01650 USB2ATA
01660          LDA #1
01670          STA STRIG0
01680 ;
01690          LDA MBUTTON
01700          BEQ GETMOUSE
01710          LDA #0
01720          STA STRIG0
01730 ;
01740 GETMOUSE
01750          LDA XM
01760          CLC
01770          ADC MVERT
01780          STA XM
01790 ;
01800          LDA YM
01810          CLC
01820          ADC MHORIZ
01830          STA YM
01840 PLAYER
01850          CLC
01860          LDA XM
01870          CLC
01880          ADC #49
01890          STA HPOS0
01900          LDX #0
01910          TXA
01920 .1       STA $7C00,X
01930          INX
01940          BNE .1
01950          LDX YM
01960          LDY #0
01970 .2       LDA PLAYTAB,Y
01980          STA $7C20,X
01990          INX
02000          INY
02010          CPY #11
02020          BNE .2
02030 .20      RTS
02040 ------------------------------
02050 VBI
02060 ;
02070          LDA #0
02080          STA MVERT
02090          STA MHORIZ
02100          STA MBUTTON
02110          STA MWHEEL
02120 ;
02130          JSR POLLDEVICE
02140          JSR USB2ATA
02150 .1       JMP XITVBV
02160 ------------------------------
02170 PLAYTAB
02180          .HX 0080C0E0F0E0E0B0
02190          .HX 101000
02200 ------------------------------
02210          .OR $7400
02220 ------------------------------
02230 PRINTDEVICE
02240          JSR PRINT
02250          .AS "USB MOUSE Driver"
02260          .HX 40
02270          RTS
02280 ------------------------------
02290 PRINTVERSION
02300          JSR PRINT
02310          .AS "Version 1.0 "
02320          .HX 40
02330          RTS
02340 ------------------------------
02350 PRINTCOPY
02360          JSR PRINT
02370          .AS "(c) 20050121 C. Strotmann/ABBUC"
02380          .HX 40
02390 ;
02400 ; PM GRAPHIC INIT
02410 ;
02420          LDA #$FF
02430          STA PCOL0
02440          LDA #$78
02450          STA PMBASE
02460          LDA #$3A
02470          STA SDMCTL
02480          LDA #2
02490          STA GRACTL
02500          STA GPRIOR
02510          RTS
02520 ------------------------------
```
  
  
