# Atari USB Keyboard Driver  
  
first BETA Version, 15.9.2004  
  
```
01000          .LI OFF
01010 **************************
01020 ** 6502 USB DEVELOPMENT **
01030 ** (C) 2004 BY ABBUC    **
01040 ** REGINALGRUPPE FFM    **
01050 ** KEYBOARD DRIVER FOR  **
01060 ** USB SL811HS          **
01070 ** VERSION 0.1b20040910 **
01080 **************************
01090 ;
01100          .OR $3500
01110          .OF "D:USBKEY.COM"
01120 ;
01130 ; SL811 MEMORY ADDRESSES
01140 ; CHANGE ACCORDING TO YOUR
01150 ; CONFIGURATION
01160 USBSEL   = $D500
01170 USBDTA   = $D501
01180 ;
01190 VCOUNT   = $D40B
01200 ;
01210 ; USB REGISTER SL811
01220 ;
01230 CTL      = $00 ; USBA HOST CTL
01240 BUFADR   = $01 ; BUFFER ADDRESS
01250 BUFLEN   = $02 ; BUFFER LEN
01260 PIDEP    = $03 ; HOST PID
01270 PKSTAT   = $03 ; PAKET STATUS
01280 FNADDR   = $04 ; USB ADDR (WO)
01290 MCNTRL   = $05 ; MAIN CONTROL
01300 CDTASET  = $0E
01310 SOFCNT   = $0F ; CNTRL 2 REG
01320 SOFLOW   = $0E ; SOF LOW
01330 INTSTAT  = $0D ; IRQ STATUS
01340 ;
01350 ; USB CONSTANTS
01360 ;
01370 ; INTENA AND INTSTAT MASKS
01380 EP0DONE  = $01
01390 EP1DONE  = $02
01400 EP2DONE  = $04
01410 EP3DONE  = $08
01420 DMADONE  = $10
01430 SOFRECV  = $20
01440 USBRSET  = $40
01450 DMASTAT  = $80
01460 ;
01470 ; ENDPOINT CONTROL REG
01480 EPC0     = $00 ; ENDPOINT 0
01490 EPC1     = $10 ; ENDPOINT 1
01500 EPC2     = $20 ; ENDPOINT 2
01510 EPC3     = $30 ; ENDPOINT 3
01520 ;
01530 ; ENDPOINT REGISTER OFFSET
01540 ;
01550 EPC      = $00 ; CONTROL
01560 EPBA     = $01 ; BASE ADDRESS
01570 EPBL     = $02 ; BASE LENGTH
01580 EPPS     = $03 ; PACKET STATUS
01590 EPTC     = $04 ; TRANSFERCOUNT
01600 ;
01610 ; PID VALUES
01620 ;
01630 SOFPID   = $05 ; SOF PID
01640 INPID    = $90 ; PACKET ID
01650 SETPID   = $D0 ; SET ADDRESS REQ
01660 ;
01670 ; SET ADDRESS PACKET
01680 ;
01690 SETADDR  .HX 0005010000000000
01700 ;
01710 ; SET CONFIG PACKET
01720 ;
01730 SETCONF  .HX 0009010000000000
01740 ;
01750 ; ATARI MEMORY LOCATIONS
01760 CH       = $2FC
01770 SETVBV   = $E45C
01780 XITVBV   = $E462
01790 ;
01795 ; non resident init part
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
02030 ;
02040 ;
02050          LDX #INTSTAT
02060          JSR REGFETCH
02070          AND #USBRSET
02080          RTS
02090 ------------------------------
02100 CLEARIRQ
02110          LDA #$FF
02120          LDX #INTSTAT
02130          JMP REGSTORE
02140 ------------------------------
02150 SPEED
02160 ; OUT: A=0 LOW SPEED DEVICE
02170 ;      A!=0 HIGH SPEED DEVICE
02180 ;           OR ERROR
02190 ;
02200          JSR USBRESET
02210          JSR CLEARIRQ
02220          LDA #10
02230          JSR PAUSE
02240          JSR QUERYUSBRESET
02250          BEQ .1 ; NO RESET
02260          JSR CLEARIRQ
02270          LDA #$FF
02280          RTS
02290 ;
02300 .1       LDX #INTSTAT
02310          JSR REGFETCH
02320          AND #DMASTAT
02330          BNE .2
02340 ;
02350 ; LOW SPEED
02360 ;
02370          LDA #$AE
02380          LDX #SOFCNT
02390          JSR REGSTORE
02400 ;
02410          LDA #$E0
02420          LDX #CDTASET
02430          JSR REGSTORE
02440 ;
02450          LDA #$05
02460          LDX #MCNTRL
02470          JSR REGSTORE
02480 ;
02490          JSR SETUPUSB
02500          LDA #$00
02510 ;
02520 ; FULL SPEED OR ERROR
02530 ;
02540 .2
02550          RTS
02560 ------------------------------
02570 SETUPUSB
02580          LDA #$50
02590          LDX #EPC0+EPPS
02600          JSR REGSTORE
02610 ;
02620          LDA #$00
02630          LDX #EPC0+EPTC
02640          JSR REGSTORE
02650 ;
02660          LDA #$01
02670          LDX #EPC0
02680          JSR REGSTORE
02690 ;
02700          LDA #25
02710          JSR PAUSE
02720 ;
02730          JSR CLEARIRQ
02740          RTS
02750 ------------------------------
02760 INITKEYB
02770          LDA #08
02780          LDX #MCNTRL
02790          JSR REGSTORE
02800 ;
02810          LDA #10
02820          JSR PAUSE
02830 ;
02840          LDA #$21
02850          LDX #MCNTRL
02860          JSR REGSTORE
02870 ;
02880          LDA #$10    ; $10 ADDR
02890          LDX #BUFADR ; DATABUF
02900          JSR REGSTORE
02910 ;
02920          LDA #$8     ; 8 BYTE
02930          LDX #BUFLEN ; DATABUF
02940          JSR REGSTORE
02950 ;
02960          LDA #$E0    ; 1MS EOP
02970          LDX #SOFLOW
02980          JSR REGSTORE
02990 ;
03000          LDA #$EE
03010          LDX #SOFCNT
03020          JSR REGSTORE
03030 ;
03040 ; SET BUFFER FOR SETUP-ADDRESS
03050 ; REQUEST = 1
03060 ;
03070          LDY #8
03080 .1       TYA
03090          CLC
03100          ADC #$F  ; BUF ADDR
03110          TAX
03120          LDA SETADDR-1,Y
03130          JSR REGSTORE
03140          DEY
03150          BNE .1
03160 ;
03170          LDA #00     ; WE USE
03180          LDX #FNADDR ; ADDR 0
03190          JSR REGSTORE
03200 ;
03210          LDA #SETPID
03220          LDX #PIDEP
03230          JSR REGSTORE
03240 ;
03250 .2       LDA #07
03260          JSR PROCESS
03270          AND #04
03280          BNE .2
03290 ;
03300          LDA #INPID
03310          LDX #PIDEP
03320          JSR REGSTORE
03330 ;
03340          LDA #03
03350          JSR PROCESS
03360 ;
03370 ; SELECT CONFIGURATION 1
03380 ;
03390          LDY #8
03400 .3       TYA
03410          CLC
03420          ADC #$F
03430          TAX
03440          LDA SETCONF-1,Y
03450          JSR REGSTORE
03460          DEY
03470          BNE .3
03480 ;
03490          LDA #01
03500          LDX #FNADDR ; NEW ADDR
03510          JSR REGSTORE
03520 ;
03530          LDA #SETPID
03540          LDX #PIDEP
03550          JSR REGSTORE
03560 ;
03570 .4       LDA #07
03580          JSR PROCESS
03590          AND #04
03600          BNE .4
03610 ;
03620          LDA #INPID
03630          LDX #PIDEP
03640          JSR REGSTORE
03650 ;
03660          LDA #03
03670          JSR PROCESS
03680 ;
03690          LDA #INPID
03700          ORA #01
03710          LDX #PIDEP
03720          JSR REGSTORE
03730 ;
03740          RTS
03750 ------------------------------
03760 ; Print String with OS
02770 ; @ is end marker.
03860 ------------------------------
03870 * Atari specific
03880 *
03890 PRINT    PLA         Return Adresse
03900          STA $D0     vom Stack
03910          PLA         holen und als
03920          STA $D1     pointer speichern
03930 *
03940 INCP     INC $D0     Pointer
03950          BNE .1      Hochzaeh-
03960          INC $D1     len
03970 .1       LDX #0      Zeichen aus
03980          LDA ($D0,X) Ram lesen
03990          CMP #'@     Ende?
04000          BEQ ENDPR   ja==>
04010          JSR PUTCHAR Zeichen ausgeben
04020          JMP INCP    zurueck in schleife
04030 *
04040 ENDPR    LDA $D1     Pointer als
04050          PHA         neue Return
04060          LDA $D0     Adresse aufs
04070          PHA         Stack legen
04080          RTS         Programm hinter
04090 *            Text fortfuehren!
04100 ------------------------------
04110 PUTCHAR  TAX         Druck
04120          LDA $E407   Zeichen
04130          PHA         mit
04140          LDA $E406   Stack
04150          PHA         Methode
04160          TXA
04170          RTS         JUMP
04180 ------------------------------
04190 WAITKEYBOARD
04200          JSR PRINT
04210          .HX 9B
04220          .AS "ATARI USB KEYBOARD DRIVER"
04230          .HX 9B
04240          .AS "(c) 2004 ABBUC e.V."
04250          .HX 9B
04260          .AS "H. Reminder, T. Grasel, C. Strotmann"
04270          .HX 9B9B
04280          .AS "WAIT FOR DEVICE..."
04290          .HX 9B40
04300 .1       JSR SPEED
04310          CMP #0
04320          BNE .1
04330          JSR PRINT
04340          .AS "LOW SPEED DEVICE DETECTED!"
04350          .HX 9B40
04360 ;
04370          JSR INITKEYB
04380          JSR PRINT
04390          .AS "KEYBOARD INITILIZED."
04400          .HX 9B40
04410          LDX /KEYVBI
04420          LDY #KEYVBI
04430          LDA #7
04440          JSR SETVBV
04450          RTS
04460 ------------------------------
04470          .OR $600
04475 ; resident USB routine
04480 ------------------------------
04490 REGFETCH
04500 ; IN:  X=USB REGISTER
04510 ; OUT: A=USB DATA
04520          STX USBSEL
04530          LDA USBDTA
04540          RTS
04550 ------------------------------
04560 REGSTORE
04570 ; IN:  A=USB DATA
04580 ;      X=USB REGISTER
04590          STX USBSEL
04600          STA USBDTA
04610          RTS
04620 ------------------------------
04630 PAUSE
04640 ; IN:  A=NUMBER OF 1/50 SEC
04650          TAX
04660 .1       LDA VCOUNT
04670          BNE .1
04680          DEX
04690          BNE .1
04700          RTS
04710 ------------------------------
04720 ;
04730 GETKEY
04740          LDA #4
04750          JSR PAUSE
04760 ;
04770          LDA #03
04780          JSR PROCESS
04790          AND #01
04800          BEQ .2  ; NO KEY
04810 ;
04820          LDX #$10
04830          JSR REGFETCH
04840          STA MODIFIER
04850          LDX #$12
04860          JSR REGFETCH
04870 .2       RTS
04880 MODIFIER .HX 00
04890 ------------------------------
04900 PROCESS
04910 ; IN:  A=USB COMMAND
04920 ; OUT: A=RETURNCODE
04930          PHA
04940          LDA #01
04950          LDX #INTSTAT
04960          JSR REGSTORE
04970 ;
04980          PLA
04990          LDX #CTL
05000          JSR REGSTORE
05010 ;
05020 .1       LDX #INTSTAT
05030          JSR REGFETCH
05040          AND #$01
05050          BEQ .1
05060 ;
05070          LDX #PKSTAT
05080          JSR REGFETCH
05090          RTS
05100 ------------------------------
05110 USB2ATA     ; USB -> ATARI Keycode
05120          STA CH
05130          LDY #$3F
05140 .1       LDA KEYTAB,Y
05150          CMP CH
05160          BEQ .2
05170          DEY
05180          BPL .1
05190 .2       TYA
05200          LDX MODIFIER
05210          ORA MODTAB,X
05220          RTS
05230 ------------------------------
05240 KEYVBI     ; Poll USB
05250          LDX CH
05260          INX
05270          BNE .1
05280          JSR GETKEY
05290          BEQ .1
05300          JSR USB2ATA
05310          STA CH
05320 .1       JMP XITVBV
05330 ------------------------------
05340 ; KEYCODE TABLE
05350 KEYTAB   .HX 0F0D36FFFF0E284F
05360          .HX 12FF1318280C5251
05370          .HX 19FF06FFFF051B1C
05380          .HX 21FF202329221F1E
05390          .HX 2B2C3711FF10FF1B
05400          .HX 15FF081D2B171A14
05410          .HX 26FF27242A25FFFF
05420          .HX 090B07FFFF0A1604
05430 MODTAB   .HX 008040
05440 ------------------------------
05450          .OR $2E0
05460          .DA WAITKEYBOARD
05470 ------------------------------

```
  
-- Carsten Strotmann  
