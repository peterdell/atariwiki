# Driver for Logitech Formula GP Analog with Rockfire USB Adapter  
  
  
  
  
Tested with a Logitec Formula GP Wheel (Analog Version) and a Rockfire USB Adapter set to switch "1". Other Logitech Wheels might work. Please send feedback.  
  
![](attachments/LogitechFormulaGP.jpg)  
  
  
The RockFire Adapter can be used to attach all kinds of PC Controller with Game-Port Interface via USB to the Atari USB Cart.  
  
The Rockfire USB-Nest Joystick Converter extends the USB port to support all conventional analog 15-pin game port controllers. This converter is built with a unique 4-mode selectable switch for maximum compatibility with CMS Controller super 8 + (Mode 4).  
  
Features:  
  
- Mode Selector switch  
- Mode 1: (TM FCS compatible)  
- Mode 2: (CH FLIGHTSTICK PRO compatible)  
- Mode 3: 2-4 Axis (X and Y), 4 Function buttons  
- Mode 4: 2 Axis (X and Y), 8 Function buttons  
  
![](attachments/usb-nest-trnsprnt.gif)  
  
## Description  
  
|| USB Register || Byte of HID Packet || Function || Atari Memory Shadow || original Label || new USB label ||  
|  $10           |  1                 | Wheel movement  | $270 (624)  | PADDL0 | LWHEEL     |  
|  $11           |  2                 | Buttons 1-6 | $271 (625)  | PADDL1 | LBUTTON     |  
  
  
- Byte 1: Wheel movement (< $25 = left, $26-$2F = middle, >$30 = right)  
- Byte 2: Buttons 1-6  
  
  
## Device dependent source  
  
This Source must be included into the [Base HID Driver](../BaseHIDDriver/index.md).  
  
```
01000          .LI OFF
01010 ****************************
01020 ** 6502 USB DEVELOPMENT   **
01030 ** (C) 2009 BY ABBUC      **
01040 ** REGIONALGRUPPE FFM     **
01050 ** DEVICE DRIVER FOR      **
01060 ** LOGITECH FORMULA GP    **
01070 ** VERSION 1.0 20090717   **
01080 ** LICENSED UNDER THE     **
01090 ** GNU PUBLIC LICENSE     **
01100 ** (GPL) VERS. 3 OR LATER **
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
01420          STA LWHEEL
01430 ;
01440          LDX #$14
01450          JSR REGFETCH
01470          STA LBUTTON
01480 ;
01530          LDX #$11
01540          JSR REGFETCH
01550          STA LACCEL
01560          STA LTHROTL
01600          STA LBRAKE
01610 ;
01620 .2       RTS
01630 ------------------------------
01640 USB2ATA
01650          LDA #$0F
01660          STA STICK0
01670          LDA #1
01680          STA STRIG0
01690 ;
01700          LDA LBUTTON
01710          BEQ GETSTICK
01720          LDA #0
01730          STA STRIG0
01740 ;
01750 GETSTICK
01760          LDA STICK0
01770          LDX LWHEEL
01771          CPX #$30
01780          BPL .1   ; RIGHT
01790          CPX #$25
01800          BMI .2   ; LEFT
01810          BNE .10
01820 .1       EOR #$04 ; LEFT
01830          BPL .3
01840 .2       EOR #$08 ; RIGHT
01850 .3       STA STICK0
01860 .10      RTS
01870 ------------------------------
01880 VBI
01890          LDA STICK0
01900          EOR #$0F
01910          BNE .1
01920          LDA STRIG0
01930          BEQ .1
01940 ;
01950          JSR POLLDEVICE
01960          JSR USB2ATA
01970 .1       JMP XITVBV
01980 ------------------------------
01990          .OR $72A0
02000 ------------------------------
02010 PRINTDEVICE
02020          JSR PRINT
02030          .AS "Logitech Wheel Driver"
02040          .HX 9B
02050          .AS "Formula GP"
02060          .HX 40
02070          RTS
02080 ------------------------------
02090 PRINTVERSION
02100          JSR PRINT
02110          .AS "Version 1.0 "
02120          .HX 40
02130          RTS
02140 ------------------------------
02150 PRINTCOPY
02160          JSR PRINT
02170          .AS "(c) 20090717 C. Strotmann/ABBUC"
02180          .HX 40
02190          RTS
02200 ------------------------------
```
  
## PolePosition Patch  
  
```
01000          .LI OFF
01010 ****************************
01020 ** 6502 USB DEVELOPMENT   **
01030 ** (C) 2004 BY ABBUC      **
01040 ** REGIONALGRUPPE FFM     **
01050 ** USB HID BASE DRIVER    **
01060 ** FOR USB SL811HS        **
01070 ** VERSION 2.0 20041213   **
01080 ** LICENSED UNDER THE     **
01090 ** GNU PUBLIC LICENSE     **
01100 ** (GPL) VERS. 2 OR LATER **
01110 **                        **
01120 ****************************
01130 ;
01140          .OR $2500
01150          .OF "D:POLEUSB.COM"
01160 ;
01170 ; SL811 MEMORY ADDRESSES
01180 ; CHANGE ACCORDING TO YOUR
01190 ; CONFIGURATION
01200 USBSEL   = $D500
01210 USBDTA   = $D501
01220 ;
01230 ; USB REGISTER SL811
01240 ;
01250 CTL      = $00 ; USBA HOST CTL
01260 BUFADR   = $01 ; BUFFER ADDRESS
01270 BUFLEN   = $02 ; BUFFER LEN
01280 PIDEP    = $03 ; HOST PID
01290 PKSTAT   = $03 ; PAKET STATUS
01300 FNADDR   = $04 ; USB ADDR (WO)
01310 MCNTRL   = $05 ; MAIN CONTROL
01320 CDTASET  = $0E
01330 SOFCNT   = $0F ; CNTRL 2 REG
01340 SOFLOW   = $0E ; SOF LOW
01350 INTSTAT  = $0D ; IRQ STATUS
01360 ;
01370 ; USB CONSTANTS
01380 ;
01390 ; INTENA AND INTSTAT MASKS
01400 EP0DONE  = $01
01410 EP1DONE  = $02
01420 EP2DONE  = $04
01430 EP3DONE  = $08
01440 DMADONE  = $10
01450 SOFRECV  = $20
01460 USBRSET  = $40
01470 DMASTAT  = $80
01480 ;
01490 ; ENDPOINT CONTROL REG
01500 EPC0     = $00 ; ENDPOINT 0
01510 EPC1     = $10 ; ENDPOINT 1
01520 EPC2     = $20 ; ENDPOINT 2
01530 EPC3     = $30 ; ENDPOINT 3
01540 ;
01550 ; ENDPOINT REGISTER OFFSET
01560 ;
01570 EPC      = $00 ; CONTROL
01580 EPBA     = $01 ; BASE ADDRESS
01590 EPBL     = $02 ; BASE LENGTH
01600 EPPS     = $03 ; PACKET STATUS
01610 EPTC     = $04 ; TRANSFERCOUNT
01620 ;
01630 ; PID VALUES
01640 ;
01650 SOFPID   = $05 ; SOF PID
01660 INPID    = $90 ; PACKET ID
01670 SETPID   = $D0 ; SET ADDRESS REQ
01680 ;
01690 ; SET ADDRESS PACKET
01700 ;
01710 SETADDR  .HX 0005010000000000
01720 ;
01730 ; SET CONFIG PACKET
01740 ;
01750 SETCONF  .HX 0009010000000000
01760 ;
01770 VCOUNT   = $D40B
01780 CONSOL   = $D01F
01790 ;
01800 ------------------------------
01810 USBRESET
01820          LDA #$AE ; SET SOF
01830          LDX #SOFCNT ; HIGH COUNT
01840          JSR REGSTORE
01850 ;
01860          LDA #$08    ; RESET USB
01870          LDX #MCNTRL ; FULLSPEED
01880          JSR REGSTORE
01890 ;
01900          LDA #$10
01910          JSR PAUSE
01920 ;
01930          LDA #00
01940          LDX #MCNTRL
01950          JSR REGSTORE
01960 ;
01970          RTS
01980 ------------------------------
01990 QUERYUSBRESET
02000 ; OUT: A=0 NO USB RESET
02010 ;    A!=0 USBRESET
02020 ;
02030          LDX #INTSTAT
02040          JSR REGFETCH
02050          AND #USBRSET
02060          RTS
02070 ------------------------------
02080 CLEARIRQ
02090          LDA #$FF
02100          LDX #INTSTAT
02110          JMP REGSTORE
02120 ------------------------------
02130 SPEED
02140 ; OUT: A=0 LOW SPEED DEVICE
02150 ;      A!=0 HIGH SPEED DEVICE
02160 ;           OR ERROR
02170 ;
02180          JSR USBRESET
02190          JSR CLEARIRQ
02200          LDA #10
02210          JSR PAUSE
02220          JSR QUERYUSBRESET
02230          BEQ .1 ; NO RESET
02240          JSR CLEARIRQ
02250          LDA #$FF
02260          RTS
02270 ;
02280 .1       LDX #INTSTAT
02290          JSR REGFETCH
02300          AND #DMASTAT
02310          BNE .2
02320 ;
02330 ; LOW SPEED
02340 ;
02350          LDA #$AE
02360          LDX #SOFCNT
02370          JSR REGSTORE
02380 ;
02390          LDA #$E0
02400          LDX #CDTASET
02410          JSR REGSTORE
02420 ;
02430          LDA #$05
02440          LDX #MCNTRL
02450          JSR REGSTORE
02460 ;
02470          JSR SETUPUSB
02480          LDA #$00
02490 ;
02500 ; FULL SPEED OR ERROR
02510 ;
02520 .2
02530          RTS
02540 ------------------------------
02550 SETUPUSB
02560          LDA #$50
02570          LDX #EPC0+EPPS
02580          JSR REGSTORE
02590 ;
02600          LDA #$00
02610          LDX #EPC0+EPTC
02620          JSR REGSTORE
02630 ;
02640          LDA #$01
02650          LDX #EPC0
02660          JSR REGSTORE
02670 ;
02680          LDA #25
02690          JSR PAUSE
02700 ;
02710          JSR CLEARIRQ
02720          RTS
02730 ------------------------------
02740 INITDEVICE
02750          LDA #08
02760          LDX #MCNTRL
02770          JSR REGSTORE
02780 ;
02790          LDA #14
02800          JSR PAUSE
02810 ;
02820          LDA #$21
02830          LDX #MCNTRL
02840          JSR REGSTORE
02850 ;
02860          LDA #$10    ; $10 ADDR
02870          LDX #BUFADR ; DATABUF
02880          JSR REGSTORE
02890 ;
02900          LDA #$8     ; 8 BYTE
02910          LDX #BUFLEN ; DATABUF
02920          JSR REGSTORE
02930 ;
02940          LDA #$E0    ; 1MS EOP
02950          LDX #SOFLOW
02960          JSR REGSTORE
02970 ;
02980          LDA #$EE
02990          LDX #SOFCNT
03000          JSR REGSTORE
03010 ;
03020 ; SET BUFFER FOR SETUP-ADDRESS
03030 ; REQUEST = 1
03040 ;
03050          LDY #8
03060 .1       TYA
03070          CLC
03080          ADC #$F  ; BUF ADDR
03090          TAX
03100          LDA SETADDR-1,Y
03110          JSR REGSTORE
03120          DEY
03130          BNE .1
03140 ;
03150          LDA #00     ; WE USE
03160          LDX #FNADDR ; ADDR 0
03170          JSR REGSTORE
03180 ;
03190          LDA #SETPID
03200          LDX #PIDEP
03210          JSR REGSTORE
03220 ;
03230 .2       LDA #07
03240          JSR PROCESS
03250          AND #04
03260          BNE .2
03270 ;
03280          LDA #20
03290          JSR PAUSE
03300 ;
03310          LDA #INPID
03320          LDX #PIDEP
03330          JSR REGSTORE
03340 ;
03350          LDA #03
03360          JSR PROCESS
03370 ;
03380 ; SELECT CONFIGURATION 1
03390 ;
03400          LDY #8
03410 .3       TYA
03420          CLC
03430          ADC #$F
03440          TAX
03450          LDA SETCONF-1,Y
03460          JSR REGSTORE
03470          DEY
03480          BNE .3
03490 ;
03500          LDA #01
03510          LDX #FNADDR ; NEW ADDR
03520          JSR REGSTORE
03530 ;
03540          LDA #SETPID
03550          LDX #PIDEP
03560          JSR REGSTORE
03570 ;
03580 .4       LDA #07
03590          JSR PROCESS
03600          AND #04
03610 ;
03620          BNE .4
03630 ;
03640          LDA #INPID
03650          LDX #PIDEP
03660          JSR REGSTORE
03670 ;
03680          LDA #03
03690          JSR PROCESS
03700 ;
03710          LDA #INPID
03720          ORA #01
03730          LDX #PIDEP
03740          JSR REGSTORE
03750 ;
03760          RTS
03770 ------------------------------
03780 ; PRINT INLINE STRING
03790 ; END MARKER '@'
03800 ;
03810 PRINT    PLA         get Return address
03820          STA $D0     from Stack
03830          PLA         and store
03840          STA $D1     as pointer
03850 ;
03860 INCP     INC $D0     increase
03870          BNE .1      pointer
03880          INC $D1
03890 .1       LDX #0      read Char from RAM
03900          LDA ($D0,X)
03910          CMP #'@     End?
03920          BEQ ENDPR   yes==>
03930          JSR PUTCHAR Print Char
03940          JMP INCP    back to loop
03950 ;
03960 ENDPR    LDA $D1     store pointer
03970          PHA         as new
03980          LDA $D0     return address
03990          PHA         on stack
04000          RTS         continue pgm
04010 ;            after text
04020 ------------------------------
04030 PUTCHAR  TAX         Print char
04040          LDA $E407   with OS
04050          PHA         Routine
04060          LDA $E406
04070          PHA
04080          TXA
04090          RTS         JUMP
04100 ------------------------------
04110 CR       LDA #$9B
04120          JMP PUTCHAR
04130 ------------------------------
04140 WAITDEVICE
04150          JSR PRINT
04160          .HX 9B
04170          .AS "ATARI USB HID DRIVER"
04180          .HX 9B
04190          .AS "Version 2.0 / GNU License"
04200          .HX 9B
04210          .AS "(c) 2004 ABBUC e.V."
04220          .HX 9B
04230          .AS "H. Reminder, T. Grasel, C. Strotmann"
04240          .HX 9B9B40
04250          JSR PRINTDEVICE
04260          JSR CR
04270          JSR PRINTVERSION
04280          JSR CR
04290          JSR PRINTCOPY
04300          JSR CR
04310          JSR CR
04320          JSR PRINT
04330          .AS "WAIT FOR DEVICE, [START] TO SKIP..."
04340          .HX 9B40
04350 .1       JSR SPEED
04360          BEQ .2
04370 ; QUERY CONSOL KEYS
04380          LDA CONSOL
04390          AND #1 ; START KEY
04400          BEQ .3 ; SKIP USB
04410          BNE .1
04420 ;
04430 .2       JSR PRINT
04440          .AS "LOW SPEED DEVICE DETECTED!"
04450          .HX 9B40
04460 ;
04470          JSR INITDEVICE
04480          JSR PRINT
04490          .AS "WHEEL INITILIZED."
04500          .HX 9B40
04510          JMP $0680
04520 ;
04530 .3       JSR PRINT
04540          .AS "USB detection skipped,"
04550          .HX 9B
04560          .AS "no USB Driver installed!"
04570          .HX 9B40
04580          JMP $0680
04590 ------------------------------
04600 RESPART  .OR $7F00
04610 REGFETCH
04620 ; IN:  X=USB REGISTER
04630 ; OUT: A=USB DATA
04640          STX USBSEL
04650          LDA USBDTA
04660          RTS
04670 ------------------------------
04680 REGSTORE
04690 ; IN:  A=USB DATA
04700 ;      X=USB REGISTER
04710          STX USBSEL
04720          STA USBDTA
04730          RTS
04740 ------------------------------
04750 PAUSE
04760 ; IN:  A=NUMBER OF 1/50 SEC
04770          TAX
04780 .1       LDA VCOUNT
04790          BNE .1
04800          DEX
04810          BNE .1
04820          RTS
04830 ------------------------------
04840 PROCESS
04850 ; IN:  A=USB COMMAND
04860 ; OUT: A=RETURNCODE
04870          PHA
04880          LDA #01
04890          LDX #INTSTAT
04900          JSR REGSTORE
04910 ;
04920          PLA
04930          LDX #CTL
04940          JSR REGSTORE
04950 ;
04960 .1       LDX #INTSTAT
04970          JSR REGFETCH
04980          AND #$01
04990          BEQ .1
05000 ;
05010          LDX #PKSTAT
05020          JSR REGFETCH
05030          RTS
05040 ------------------------------
05050          .LI OFF
05060 ****************************
05070 ** 6502 USB DEVELOPMENT   **
05080 ** (C) 2004 BY ABBUC      **
05090 ** REGIONALGRUPPE FFM     **
05100 ** DEVICE DRIVER FOR      **
05110 ** LOGITECH WHEEL VIBRFEED**
05120 ** VERSION 1.0 20050430   **
05130 ** LICENSED UNDER THE     **
05140 ** GNU PUBLIC LICENSE     **
05150 ** (GPL) VERS. 2 OR LATER **
05160 **                        **
05170 ****************************
05180 ; THIS FILE MUST BE INCLUDED
05190 ; FROM USBHID.SRC!
05200 ;
05210 ; ATARI MEMORY LOCATIONS
05220 ;
05230 STICK0   = $0278
05240 STICK1   = $0279
05250 STRIG0   = $0284
05260 STRIG1   = $0285
05270 ;
05280 ; USB JOYSTICK SHADOW REGISTER
05290 ;
05300 RWHEEL   = $0270
05320 RBUTTON  = $0271
05350 RACCEL   = $0272
05360 RACCTGL  = $0273
05370 ;
05380 ------------------------------
05390 POLLDEVICE
05400 ;
05410          LDA #03
05420          JSR PROCESS
05430 ;        AND #01
05440 ;        BEQ .2  ; NO DATA
05450 ;
05460          LDX #$10
05470          JSR REGFETCH
05480          STA RWHEEL
05490          LDX #$11
05500          JSR REGFETCH
05520          STA RACCEL
05530          LDX #$14
05535          JSR REGFETCH
05550          STA RBUTTON
05700 ;
05710 .2       RTS
05720 ------------------------------
05730 USB2ATA
05740          LDA #$0F
05750          STA STICK0
05770          LDA #1
05780          STA STRIG0
05800 ;
05810          LDA RACCEL
05820          CMP #$36
05830          BMI .5 ; NO BRAKE
05840          LDA #0
05850          STA STRIG0 ; BRAKE
05855          BEQ .6
05860 .5
05880          CMP #$3A ; ACCEL?
05890          BMI .6
05900          LDA RACCTGL
05910          EOR #01
05920          STA RACCTGL
05930          STA STRIG0
05935 .6
05936          LDA STICK0
05940          LDX RWHEEL
05945          CPX #$2E
05950          BPL .8
05960          CPX #$2B
05970          BPL .10
05990          EOR #$04 ; LEFT
06000          BNE .10
06010 .8       EOR #$08 ; RIGHT
06030 .10      TAX
06040          LDA RBUTTON
06050          AND #5
06060          BEQ .11
06070          LDA #14  ; LOW SHIFT
06090          BNE .21
06100 .11      LDA RBUTTON
06110          AND #$A
06120          BEQ .20
06140          LDA #13  ; High SHIFT
06141          BNE .21
06145 .20      TXA
06150 .21      STA STICK0
06190          RTS
06220 ------------------------------
06230 LDYSTICK
06240          STX SAVE1
06250          STA SAVE2
06260          JSR POLLDEVICE
06270          JSR USB2ATA
06280          LDY STICK0
06290          LDX SAVE1
06300          LDA SAVE2
06310          RTS
06320 ------------------------------
06330 LDASTRIG STX SAVE1
06340          STY SAVE2
06350          JSR POLLDEVICE
06360          JSR USB2ATA
06370          LDA STRIG0
06380          LDX SAVE1
06390          LDY SAVE2
06400          RTS
06410 ------------------------------
06420 SAVE1    .HX 00
06430 SAVE2    .HX 00
06440 ------------------------------
06450          .OR $2900
06460 PRINTDEVICE
06470          JSR PRINT
06480          .AS "Logitech Wheel GP Patch"
06490          .HX 40
06500          RTS
06510 ------------------------------
06520 PRINTVERSION
06530          JSR PRINT
06540          .AS "Version 1.0"
06550          .HX 40
06560          RTS
06570 ------------------------------
06580 PRINTCOPY
06590          JSR PRINT
06600          .AS "(c) 20090717 C. Strotmann/ABBUC"
06610          .HX 40
06620          RTS
06630 ------------------------------
06640 PATCH
06650 ; let's patch
06660          .OR $365A
06670          JSR LDYSTICK
06680 ;
06690          .OR $351E
06700          JSR LDASTRIG
06710 ------------------------------
06720          .OR $02E0
06730          .DA WAITDEVICE
06740 ------------------------------
```
  
Source and patched PolePosition Game can be found on ATR Disk attached to this article.  
  
  
