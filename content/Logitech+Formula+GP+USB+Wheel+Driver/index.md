# Logitech Formula GP USB Driver  
  
  
Tested with a Logitec Formula GP Wheel USB. Other Logitech Wheels might work. Please send feedback.  
  
## Description  
  
  
|| USB Register || Byte of HID Packet || Function || Atari Memory Shadow || original Label || new USB label ||  
|  $10           |  1                 | Wheel movement  | $270 (624)  | PADDL0 | LWHEEL     |  
|  $11           |  2                 | Buttons 1-6 | $271 (625)  | PADDL1 | LBUTTON     |  
|  $12           |  3                 | Accelleration (Brake and Throttle)  | $272 (626)  | PADDL2 | LACCEL     |  
|  $13           |  4                 | Throttle | $273 (627)  | PADDL3 | LTHROTL     |  
|  $14           |  5                 | Brake | $274 (628)  | PADDL4 | LBRAKE     |  
  
  
- Byte 1: Wheel movement ($00 = left, $80 = middle, $FF= right)  
- Byte 2: Buttons 1-6  
- Byte 3: Accelleration (Throttle and Brake) ($00 = Brake, $80 = idle, $FF= Throttle)  
- Byte 4: Throttle ($00 = accellerate, $FF= idle)  
- Byte 5: Brake ($00 = Idle, $FF= Brake)  
  
  
## Device dependent source  
  
This Source must be included into the [Base HID Driver](../BaseHIDDriver/index.md).  
  
```
01000          .LI OFF
01010 ****************************
01020 ** 6502 USB DEVELOPMENT   **
01030 ** (C) 2005 BY ABBUC      **
01040 ** REGIONALGRUPPE FFM     **
01050 ** DEVICE DRIVER FOR      **
01060 ** LOGITECH FORMULA GP    **
01070 ** VERSION 1.0 20050106   **
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
01250 LWHEEL   = $0270
01260 LBUTTON  = $0271
01270 LACCEL   = $0272
01280 LTHROTL  = $0273
01290 LBRAKE   = $0274
01300 ;
01310 ------------------------------
01320 POLLDEVICE
01330 ;
01340          LDA #03
01350          JSR PROCESS
01360 ;        AND #01
01370 ;        BEQ .2  ; NO DATA
01380 ;
01390          LDX #$10
01400          JSR REGFETCH
01410          STA LWHEEL
01420 ;
01430          LDX #$11
01440          JSR REGFETCH
01450          STA LBUTTON
01460 ;
01470          LDX #$12
01480          JSR REGFETCH
01490          STA LACCEL
01500 ;
01510          LDX #$13
01520          JSR REGFETCH
01530          STA LTHROTL
01540 ;
01550          LDX #$14
01560          JSR REGFETCH
01570          STA LBRAKE
01580 ;
01590 .2       RTS
01600 ------------------------------
01610 USB2ATA
01620          LDA #$0F
01630          STA STICK0
01640          LDA #1
01650          STA STRIG0
01660 ;
01670          LDA LBUTTON
01680          BEQ GETSTICK
01690          LDA #0
01700          STA STRIG0
01710 ;
01720 GETSTICK
01730          LDA STICK0
01740          LDX LWHEEL
01750          CPX THLEFT
01760          BCC .1   ; LEFT
01770          CPX THRIGHT
01780          BCS .2   ; RIGHT
01790          BCC .10
01800 .1       EOR #$04 ; LEFT
01810          BPL .3
01820 .2       EOR #$08 ; RIGHT
01830 .3       STA STICK0
01840 .10      RTS
01850 ------------------------------
01860 THLEFT   .HX 40 ; THRESHOLD LEFT
01870 THRIGHT  .HX C0 ; THRESHOLD RIGHT
01880 ------------------------------
01890 VBI
01900          LDA STICK0
01910          EOR #$0F
01920          BNE .1
01930          LDA STRIG0
01940          BEQ .1
01950 ;
01960          JSR POLLDEVICE
01970          JSR USB2ATA
01980 .1       JMP XITVBV
01990 ------------------------------
02000          .OR $7400
02010 ------------------------------
02020 PRINTDEVICE
02030          JSR PRINT
02040          .AS "Logitech FORMULA GP Driver"
02050          .HX 40
02060          RTS
02070 ------------------------------
02080 PRINTVERSION
02090          JSR PRINT
02100          .AS "Version 1.0 "
02110          .HX 40
02120          RTS
02130 ------------------------------
02140 PRINTCOPY
02150          JSR PRINT
02160          .AS "(c) 20050106 C. Strotmann/ABBUC"
02170          .HX 40
02180          RTS
02190 ------------------------------
```
  
  
  
