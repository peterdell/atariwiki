---
title: BaseHIDDriver
---
# Base USB HID Driver  
  
This driver includes the basic functions to access an USB HID Device. This Driver will include the device dependent code.  
  
```
01000            .LI OFF
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
01140            .OR $7000
01150            .OF "D:RUMBPAD2.COM" <--- change this name
01160 ;
01170 ; SL811 MEMORY ADDRESSES
01180 ; CHANGE ACCORDING TO YOUR
01190 ; CONFIGURATION
01200 USBSEL    = $D500
01210 USBDTA    = $D501
01220 ;
01230 ; USB REGISTER SL811
01240 ;
01250 CTL       = $00 ; USBA HOST CTL
01260 BUFADR    = $01 ; BUFFER ADDRESS
01270 BUFLEN    = $02 ; BUFFER LEN
01280 PIDEP     = $03 ; HOST PID
01290 PKSTAT    = $03 ; PAKET STATUS
01300 FNADDR    = $04 ; USB ADDR (WO)
01310 MCNTRL    = $05 ; MAIN CONTROL
01320 CDTASET   = $0E
01330 SOFCNT    = $0F ; CNTRL 2 REG
01340 SOFLOW    = $0E ; SOF LOW
01350 INTSTAT   = $0D ; IRQ STATUS
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
01500 EPC0    = $00 ; ENDPOINT 0
01510 EPC1    = $10 ; ENDPOINT 1
01520 EPC2    = $20 ; ENDPOINT 2
01530 EPC3    = $30 ; ENDPOINT 3
01540 ;
01550 ; ENDPOINT REGISTER OFFSET
01560 ;
01570 EPC       = $00 ; CONTROL
01580 EPBA    = $01 ; BASE ADDRESS
01590 EPBL    = $02 ; BASE LENGTH
01600 EPPS    = $03 ; PACKET STATUS
01610 EPTC    = $04 ; TRANSFERCOUNT
01620 ;
01630 ; PID VALUES
01640 ;
01650 SOFPID    = $05 ; SOF PID
01660 INPID  = $90 ; PACKET ID
01670 SETPID    = $D0 ; SET ADDRESS REQ
01680 ;
01690 ; SET ADDRESS PACKET
01700 ;
01710 SETADDR  .HX 0005010000000000
01720 ;
01730 ; SET CONFIG PACKET
01740 ;
01750 SETCONF  .HX 0009010000000000
01760 ;
01770 SETVBV    = $E45C
01780 XITVBV    = $E462
01790 VCOUNT    = $D40B
01800 CONSOL    = $D01F
01810 ;
01820 ------------------------------
01830 USBRESET
01840            LDA #$AE ; SET SOF
01850            LDX #SOFCNT ; HIGH COUNT
01860            JSR REGSTORE
01870 ;
01880            LDA #$08    ; RESET USB
01890            LDX #MCNTRL ; FULLSPEED
01900            JSR REGSTORE
01910 ;
01920            LDA #$10
01930            JSR PAUSE
01940 ;
01950            LDA #00
01960            LDX #MCNTRL
01970            JMP REGSTORE
01980 ;
02000 ------------------------------
02010 QUERYUSBRESET
02020 ; OUT: A=0 NO USB RESET
02030 ;  A!=0 USBRESET
02040 ;
02050            LDX #INTSTAT
02060            JSR REGFETCH
02070            AND #USBRSET
02080            RTS
02090 ------------------------------
02100 CLEARIRQ
02110            LDA #$FF
02120            LDX #INTSTAT
02130            JMP REGSTORE
02140 ------------------------------
02150 SPEED
02160 ; OUT: A=0 LOW SPEED DEVICE
02170 ;     A!=0 HIGH SPEED DEVICE
02180 ;           OR ERROR
02190 ;
02200            JSR USBRESET
02210            JSR CLEARIRQ
02220            LDA #10
02230            JSR PAUSE
02240            JSR QUERYUSBRESET
02250            BEQ .1 ; NO RESET
02260            JSR CLEARIRQ
02270            LDA #$FF
02280            RTS
02290 ;
02300 .1         LDX #INTSTAT
02310            JSR REGFETCH
02320            AND #DMASTAT
02330            BNE .2
02340 ;
02350 ; LOW SPEED
02360 ;
02370            LDA #$AE
02380            LDX #SOFCNT
02390            JSR REGSTORE
02400 ;
02410            LDA #$E0
02420            LDX #CDTASET
02430            JSR REGSTORE
02440 ;
02450            LDA #$05
02460            LDX #MCNTRL
02470            JSR REGSTORE
02480 ;
02490            JSR SETUPUSB
02500            LDA #$00
02510 ;
02520 ; FULL SPEED OR ERROR
02530 ;
02540 .2
02550            RTS
02560 ------------------------------
02570 SETUPUSB
02580            LDA #$50
02590            LDX #EPC0+EPPS
02600            JSR REGSTORE
02610 ;
02620            LDA #$00
02630            LDX #EPC0+EPTC
02640            JSR REGSTORE
02650 ;
02660            LDA #$01
02670            LDX #EPC0
02680            JSR REGSTORE
02690 ;
02700            LDA #25
02710            JSR PAUSE
02720 ;
02730            JMP CLEARIRQ
02750 ------------------------------
02760 INITDEVICE
02770            LDA #08
02780            LDX #MCNTRL
02790            JSR REGSTORE
02800 ;
02810            LDA #14
02820            JSR PAUSE
02830 ;
02840            LDA #$21
02850            LDX #MCNTRL
02860            JSR REGSTORE
02870 ;
02880            LDA #$10    ; $10 ADDR
02890            LDX #BUFADR ; DATABUF
02900            JSR REGSTORE
02910 ;
02920            LDA #$8      ; 8 BYTE
02930            LDX #BUFLEN ; DATABUF
02940            JSR REGSTORE
02950 ;
02960            LDA #$E0    ; 1MS EOP
02970            LDX #SOFLOW
02980            JSR REGSTORE
02990 ;
03000            LDA #$EE
03010            LDX #SOFCNT
03020            JSR REGSTORE
03030 ;
03040 ; SET BUFFER FOR SETUP-ADDRESS
03050 ; REQUEST = 1
03060 ;
03070            LDY #8
03080 .1         TYA
03090            CLC
03100            ADC #$F  ; BUF ADDR
03110            TAX
03120            LDA SETADDR-1,Y
03130            JSR REGSTORE
03140            DEY
03150            BNE .1
03160 ;
03170            LDA #00      ; WE USE
03180            LDX #FNADDR ; ADDR 0
03190            JSR REGSTORE
03200 ;
03210            LDA #SETPID
03220            LDX #PIDEP
03230            JSR REGSTORE
03240 ;
03250 .2         LDA #07
03260            JSR PROCESS
03270            AND #04
03280            BNE .2
03290 ;
03300            LDA #20
03310            JSR PAUSE
03320 ;
03330            LDA #INPID
03340            LDX #PIDEP
03350            JSR REGSTORE
03360 ;
03370            LDA #03
03380            JSR PROCESS
03390 ;
03400 ; SELECT CONFIGURATION 1
03410 ;
03420            LDY #8
03430 .3         TYA
03440            CLC
03450            ADC #$F
03460            TAX
03470            LDA SETCONF-1,Y
03480            JSR REGSTORE
03490            DEY
03500            BNE .3
03510 ;
03520            LDA #01
03530            LDX #FNADDR ; NEW ADDR
03540            JSR REGSTORE
03550 ;
03560            LDA #SETPID
03570            LDX #PIDEP
03580            JSR REGSTORE
03590 ;
03600 .4         LDA #07
03610            JSR PROCESS
03620            AND #04
03630 ;
03640            BNE .4
03650 ;
03660            LDA #INPID
03670            LDX #PIDEP
03680            JSR REGSTORE
03690 ;
03700            LDA #03
03710            JSR PROCESS
03720 ;
03730            LDA #INPID
03740            ORA #01
03750            LDX #PIDEP
03760            JMP REGSTORE
03770 ;
03790 ------------------------------
03800 ; PRINT INLINE STRING
03810 ; END MARKER '@'
03820 ;
03830 PRINT  PLA            get Return address
03840            STA $D0      from Stack
03850            PLA            and store
03860            STA $D1      as pointer
03870 ;
03880 INCP    INC $D0     increase
03890            BNE .1     pointer
03900            INC $D1
03910 .1         LDX #0     read Char from RAM
03920            LDA ($D0,X)
03930            CMP #'@      End?
03940            BEQ ENDPR  yes==>
03950            JSR PUTCHAR Print Char
03960            JMP INCP    back to loop
03970 ;
03980 ENDPR  LDA $D1      store pointer
03990            PHA      as new
04000            LDA $D0  return address
04010            PHA      on stack
04020            RTS      continue pgm
04030 ;             after text
04040 ------------------------------
04050 PUTCHAR  TAX          Print char
04060            LDA $E407  with OS
04070            PHA            Routine
04080            LDA $E406
04090            PHA
04100            TXA
04110            RTS            JUMP
04120 ------------------------------
04130 CR         LDA #$9B
04140            JMP PUTCHAR
04150 ------------------------------
04160 WAITDEVICE
04170            JSR PRINT
04180            .HX 9B
04190            .AS "ATARI USB HID DRIVER"
04200            .HX 9B
04210            .AS "Version 2.0 / GNU License"
04220            .HX 9B
04230            .AS "(c) 2004 ABBUC e.V."
04240            .HX 9B
04250            .AS "H. Reminder, T. Grasel, C. Strotmann"
04260            .HX 9B9B40
04270            JSR PRINTDEVICE
04280            JSR CR
04290            JSR PRINTVERSION
04300            JSR CR
04310            JSR PRINTCOPY
04320            JSR CR
04330            JSR CR
04350            JSR PRINT
04360            .AS "WAIT FOR DEVICE, [START] TO SKIP..."
04370            .HX 9B40
04380 .1         JSR SPEED
04390            BEQ .2
04400 ; QUERY CONSOL KEYS
04410            LDA CONSOL
04420            AND #1 ; START KEY
04430            BEQ .3 ; SKIP USB
04440            BNE .1
04450 ;
04460 .2         JSR PRINT
04470            .AS "LOW SPEED DEVICE DETECTED!"
04480            .HX 9B40
04490 ;
04500            JSR INITDEVICE
04510            JSR PRINT
04520            .AS "JOYSTICK INITILIZED."
04530            .HX 9B40
04540            LDX /VBI
04550            LDY #VBI
04560            LDA #7
04570            JSR SETVBV
04580            RTS
04590 ;
04600 .3         JSR PRINT
04610            .AS "USB detection skipped,"
04620            .HX 9B
04630            .AS "no USB Driver installed!"
04640            .HX 9B40
04650            RTS
04660 ------------------------------
04670 RESPART  .OR $600
04680 ------------------------------
04690 REGFETCH
04700 ; IN:  X=USB REGISTER
04710 ; OUT: A=USB DATA
04720            STX USBSEL
04730            LDA USBDTA
04740            RTS
04750 ------------------------------
04760 REGSTORE
04770 ; IN:  A=USB DATA
04780 ;     X=USB REGISTER
04790            STX USBSEL
04800            STA USBDTA
04810            RTS
04820 ------------------------------
04830 PAUSE
04840 ; IN:  A=NUMBER OF 1/50 SEC
04850            TAX
04860 .1         LDA VCOUNT
04870            BNE .1
04880            DEX
04890            BNE .1
04900            RTS
04910 ------------------------------
04920 PROCESS
04930 ; IN:  A=USB COMMAND
04940 ; OUT: A=RETURNCODE
04950            PHA
04960            LDA #01
04970            LDX #INTSTAT
04980            JSR REGSTORE
04990 ;
05000            PLA
05010            LDX #CTL
05020            JSR REGSTORE
05030 ;
05040 .1         LDX #INTSTAT
05050            JSR REGFETCH
05060            AND #$01
05070            BEQ .1
05080 ;
05090            LDX #PKSTAT
05100            JMP REGFETCH
05120 ------------------------------
05130 DEVICE    .IN "D:RUMBPAD2.SRC" <--- change this include for device dependent code
05140 ------------------------------
05150            .OR $2E0
05160            .DA WAITDEVICE
05170 ------------------------------

```
