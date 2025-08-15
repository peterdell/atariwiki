---
title: Digital Joypad Driver
---
# Digital Joypad Driver  
  
Tested with a Logitec Wingman Precision USB. Other digital Joypad might work. Please send feedback.  
  
## Logitech Rumblepad 2 USB Driver (new Modular Driver Version 2)  
  
see [Logitech Rumblepad 2 USB](../JoypadRumblePadTwoUsb/index.md)  
  
## Generic VBI Driver  
  
Will work with Atari Basic, Turbo Basic, ACTION!, XFORTH.  
  
Load driver and use Stick(0) and Strig(0) as normal.  
  
### Related Pages  
  
- [Boulder Dash 1 Patch](../AtariJoypadBouderDashPatch/index.md)  
  
```
01000          .LI OFF
01010 **************************
01020 ** 6502 USB DEVELOPMENT **
01030 ** (C) 2004 BY ABBUC    **
01040 ** REGIONALGRUPPE FFM   **
01050 ** DIGITAL JOYPAD DRIVER**
01060 ** FOR USB SL811HS      **
01070 ** VERSION 1.0 20041030 **
01080 **************************
01090 ;
01100          .OR $3500
01110          .OF "D:USBJOYPD.COM"
01120 ;
01130 ; SL811 MEMORY ADDRESSES
01140 ; CHANGE ACCORDING TO YOUR
01150 ; CONFIGURATION
01160 USBSEL   = $D500
01170 USBDTA   = $D501
01180 ;
01190 ; USB REGISTER SL811
01200 ;
01210 CTL      = $00 ; USBA HOST CTL
01220 BUFADR   = $01 ; BUFFER ADDRESS
01230 BUFLEN   = $02 ; BUFFER LEN
01240 PIDEP    = $03 ; HOST PID
01250 PKSTAT   = $03 ; PAKET STATUS
01260 FNADDR   = $04 ; USB ADDR (WO)
01270 MCNTRL   = $05 ; MAIN CONTROL
01280 CDTASET  = $0E
01290 SOFCNT   = $0F ; CNTRL 2 REG
01300 SOFLOW   = $0E ; SOF LOW
01310 INTSTAT  = $0D ; IRQ STATUS
01320 ;
01330 ; USB CONSTANTS
01340 ;
01350 ; INTENA AND INTSTAT MASKS
01360 EP0DONE  = $01
01370 EP1DONE  = $02
01380 EP2DONE  = $04
01390 EP3DONE  = $08
01400 DMADONE  = $10
01410 SOFRECV  = $20
01420 USBRSET  = $40
01430 DMASTAT  = $80
01440 ;
01450 ; ENDPOINT CONTROL REG
01460 EPC0     = $00 ; ENDPOINT 0
01470 EPC1     = $10 ; ENDPOINT 1
01480 EPC2     = $20 ; ENDPOINT 2
01490 EPC3     = $30 ; ENDPOINT 3
01500 ;
01510 ; ENDPOINT REGISTER OFFSET
01520 ;
01530 EPC      = $00 ; CONTROL
01540 EPBA     = $01 ; BASE ADDRESS
01550 EPBL     = $02 ; BASE LENGTH
01560 EPPS     = $03 ; PACKET STATUS
01570 EPTC     = $04 ; TRANSFERCOUNT
01580 ;
01590 ; PID VALUES
01600 ;
01610 SOFPID   = $05 ; SOF PID
01620 INPID    = $90 ; PACKET ID
01630 SETPID   = $D0 ; SET ADDRESS REQ
01640 ;
01650 ; SET ADDRESS PACKET
01660 ;
01670 SETADDR  .HX 0005010000000000
01680 ;
01690 ; SET CONFIG PACKET
01700 ;
01710 SETCONF  .HX 0009010000000000
01720 ;
01730 ; ATARI MEMORY LOCATIONS
01740 ;
01750 STICK0   = $0278
01760 STRIG0   = $0284
01770 SETVBV   = $E45C
01780 XITVBV   = $E462
01790 VCOUNT   = $D40B
01800 ;
01810 ------------------------------
01820 USBRESET
01830          LDA #$AE ; SET SOF
01840          LDX #SOFCNT ; HIGH COUNT
01850          JSR REGSTORE
01860 ;
01870          LDA #$08    ; RESET USB
01880          LDX #MCNTRL ; FULLSPEED
01890          JSR REGSTORE
01900 ;
01910          LDA #$10
01920          JSR PAUSE
01930 ;
01940          LDA #00
01950          LDX #MCNTRL
01960          JMP REGSTORE
01970 ;
01990 ------------------------------
02000 QUERYUSBRESET
02010 ; OUT: A=0 NO USB RESET
02020 ;    A!=0 USBRESET
02030 ;
02040 ;
02050 ;
02060          LDX #INTSTAT
02070          JSR REGFETCH
02080          AND #USBRSET
02090          RTS
02100 ------------------------------
02110 CLEARIRQ
02120          LDA #$FF
02130          LDX #INTSTAT
02140          JMP REGSTORE
02150 ------------------------------
02160 SPEED
02170 ; OUT: A=0 LOW SPEED DEVICE
02180 ;      A!=0 HIGH SPEED DEVICE
02190 ;           OR ERROR
02200 ;
02210          JSR USBRESET
02220          JSR CLEARIRQ
02230          LDA #10
02240          JSR PAUSE
02250          JSR QUERYUSBRESET
02260          BEQ .1 ; NO RESET
02270          JSR CLEARIRQ
02280          LDA #$FF
02290          RTS
02300 ;
02310 .1       LDX #INTSTAT
02320          JSR REGFETCH
02330          AND #DMASTAT
02340          BNE .2
02350 ;
02360 ; LOW SPEED
02370 ;
02380          LDA #$AE
02390          LDX #SOFCNT
02400          JSR REGSTORE
02410 ;
02420          LDA #$E0
02430          LDX #CDTASET
02440          JSR REGSTORE
02450 ;
02460          LDA #$05
02470          LDX #MCNTRL
02480          JSR REGSTORE
02490 ;
02500          JSR SETUPUSB
02510          LDA #$00
02520 ;
02530 ; FULL SPEED OR ERROR
02540 ;
02550 .2
02560          RTS
02570 ------------------------------
02580 SETUPUSB
02590          LDA #$50
02600          LDX #EPC0+EPPS
02610          JSR REGSTORE
02620 ;
02630          LDA #$00
02640          LDX #EPC0+EPTC
02650          JSR REGSTORE
02660 ;
02670          LDA #$01
02680          LDX #EPC0
02690          JSR REGSTORE
02700 ;
02710          LDA #25
02720          JSR PAUSE
02730 ;
02740          JMP CLEARIRQ
02760 ------------------------------
02770 INITJOYPD
02780          LDA #08
02790          LDX #MCNTRL
02800          JSR REGSTORE
02810 ;
02820          LDA #14
02830          JSR PAUSE
02840 ;
02850          LDA #$21
02860          LDX #MCNTRL
02870          JSR REGSTORE
02880 ;
02890          LDA #$10    ; $10 ADDR
02900          LDX #BUFADR ; DATABUF
02910          JSR REGSTORE
02920 ;
02930          LDA #$8     ; 8 BYTE
02940          LDX #BUFLEN ; DATABUF
02950          JSR REGSTORE
02960 ;
02970          LDA #$E0    ; 1MS EOP
02980          LDX #SOFLOW
02990          JSR REGSTORE
03000 ;
03010          LDA #$EE
03020          LDX #SOFCNT
03030          JSR REGSTORE
03040 ;
03050 ; SET BUFFER FOR SETUP-ADDRESS
03060 ; REQUEST = 1
03070 ;
03080          LDY #8
03090 .1       TYA
03100          CLC
03110          ADC #$F  ; BUF ADDR
03120          TAX
03130          LDA SETADDR-1,Y
03140          JSR REGSTORE
03150          DEY
03160          BNE .1
03170 ;
03180          LDA #00     ; WE USE
03190          LDX #FNADDR ; ADDR 0
03200          JSR REGSTORE
03210 ;
03220          LDA #SETPID
03230          LDX #PIDEP
03240          JSR REGSTORE
03250 ;
03260 .2       LDA #07
03270          JSR PROCESS
03280          AND #04
03290          BNE .2
03300 ;
03310          LDA #20
03320          JSR PAUSE
03330 ;
03340          LDA #INPID
03350          LDX #PIDEP
03360          JSR REGSTORE
03370 ;
03380          LDA #03
03390          JSR PROCESS
03400 ;
03410 ; SELECT CONFIGURATION 1
03420 ;
03430          LDY #8
03440 .3       TYA
03450          CLC
03460          ADC #$F
03470          TAX
03480          LDA SETCONF-1,Y
03490          JSR REGSTORE
03500          DEY
03510          BNE .3
03520 ;
03530          LDA #01
03540          LDX #FNADDR ; NEW ADDR
03550          JSR REGSTORE
03560 ;
03570          LDA #SETPID
03580          LDX #PIDEP
03590          JSR REGSTORE
03600 ;
03610 .4       LDA #07
03620          JSR PROCESS
03630          AND #04
03640 ;
03650          BNE .4
03660 ;
03670          LDA #INPID
03680          LDX #PIDEP
03690          JSR REGSTORE
03700 ;
03710          LDA #03
03720          JSR PROCESS
03730 ;
03740          LDA #INPID
03750          ORA #01
03760          LDX #PIDEP
03770          JSR REGSTORE
03780 ;
03790          RTS
03800 ------------------------------
03810 ; PRINT INLINE STRING
03820 ; END MARKER '@'
03830 ;
03840 PRINT    PLA         get Return address
03850          STA $D0     from Stack
03860          PLA         and store
03870          STA $D1     as pointer
03880 ;
03890 INCP     INC $D0     increase
03900          BNE .1      pointer
03910          INC $D1
03920 .1       LDX #0      read Char from RAM
03930          LDA ($D0,X)
03940          CMP #'@     End?
03950          BEQ ENDPR   yes==>
03960          JSR PUTCHAR Print Char
03970          JMP INCP    back to loop
03980 ;
03990 ENDPR    LDA $D1     store pointer
04000          PHA         as new
04010          LDA $D0     return address
04020          PHA         on stack
04030          RTS         continue pgm
04040 ;            after text
04050 ------------------------------
04060 PUTCHAR  TAX         Print char
04070          LDA $E407   with OS
04080          PHA         Routine
04090          LDA $E406
04100          PHA
04110          TXA
04120          RTS         JUMP
04130 ------------------------------
04140 WAITJOYPAD
04150          JSR PRINT
04160          .HX 9B
04170          .AS "ATARI USB JOYPAD DRIVER"
04180          .HX 9B
04190          .AS "(c) 2004 ABBUC e.V."
04200          .HX 9B
04210          .AS "H. Reminder, T. Grasel, C. Strotmann"
04220          .HX 9B9B
04230          .AS "WAIT FOR DEVICE..."
04240          .HX 9B40
04250 .1       JSR SPEED
04260          CMP #0
04270          BNE .1
04280          JSR PRINT
04290          .AS "LOW SPEED DEVICE DETECTED!"
04300          .HX 9B40
04310 ;
04320          JSR INITJOYPD
04330          JSR PRINT
04340          .AS "JOYPAD INITILIZED."
04350          .HX 9B40
04360          LDX /JOYVBI
04370          LDY #JOYVBI
04380          LDA #7
04390          JMP SETVBV
04410 ------------------------------
04420 RESPART  .OR $600
04430 ------------------------------
04440 REGFETCH
04450 ; IN:  X=USB REGISTER
04460 ; OUT: A=USB DATA
04470          STX USBSEL
04480          LDA USBDTA
04490          RTS
04500 ------------------------------
04510 REGSTORE
04520 ; IN:  A=USB DATA
04530 ;      X=USB REGISTER
04540          STX USBSEL
04550          STA USBDTA
04560          RTS
04570 ------------------------------
04580 PAUSE
04590 ; IN:  A=NUMBER OF 1/50 SEC
04600          TAX
04610 .1       LDA VCOUNT
04620          BNE .1
04630          DEX
04640          BNE .1
04650          RTS
04660 ------------------------------
04670 ;
04680 GETJOYPAD
04690 ;
04700          LDA #03
04710          JSR PROCESS
04720          AND #01
04730          BEQ .2  ; NO DATA
04740 ;
04750          LDX #$10
04760          JSR REGFETCH
04770          STA TRIGGER
04780          LDX #$11
04790          JSR REGFETCH
04800          STA HORIZ
04810          LDX #$12
04820          JSR REGFETCH
04830          STA VERTIC
04840 ;
04850 .2       RTS
04860 ------------------------------
04870 PROCESS
04880 ; IN:  A=USB COMMAND
04890 ; OUT: A=RETURNCODE
04900          PHA
04910          LDA #01
04920          LDX #INTSTAT
04930          JSR REGSTORE
04940 ;
04950          PLA
04960          LDX #CTL
04970          JSR REGSTORE
04980 ;
04990 .1       LDX #INTSTAT
05000          JSR REGFETCH
05010          AND #$01
05020          BEQ .1
05030 ;
05040          LDX #PKSTAT
05050          JMP REGFETCH
05070 ------------------------------
05080 USB2ATA
05090          LDA #$0F
05100          STA STICK0
05110          LDA #1
05120          STA STRIG0
05130 ;
05140          LDA TRIGGER
05150          BEQ GETSTICK
05160          LDA #0
05170          STA STRIG0
05180 ;
05190 GETSTICK
05200          LDA HORIZ
05210          EOR #$80 ; NO VALUE?
05220          BEQ .10
05230          LDA STICK0
05240          LDX HORIZ
05250          BPL .1
05260          AND #$07 ; RIGHT
05270          BNE .2
05280 .1       AND #$0B ; LEFT
05290 .2       STA STICK0
05300 .10
05310          LDA VERTIC
05320          EOR #$80 ; NO VALUE?
05330          BEQ .20
05340          LDA STICK0
05350          LDX VERTIC
05360          BPL .11
05370          AND #$0D ; DOWN
05380          BNE .12
05390 .11      AND #$0E ; UP
05400 .12      STA STICK0
05410 .20      RTS
05420 ------------------------------
05430 JOYVBI
05440 ;        LDA STICK0
05450 ;        EOR #$0F
05460 ;        BNE .1      ; NORMAL STICK USED
05470          JSR GETJOYPAD
05480          JSR USB2ATA
05490 .1       JMP XITVBV
05500 ------------------------------
05510 TRIGGER  .HX 00
05520 HORIZ    .HX 00
05530 VERTIC   .HX 00
05540 ------------------------------
05550          .OR $2E0
05560          .DA WAITJOYPAD
05570 ------------------------------

```
  
  
