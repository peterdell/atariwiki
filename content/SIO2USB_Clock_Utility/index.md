# SIO2USB Clock Utility  
  
General Information  
  
Author: Carsten Strotmann   
Assembler: Bibo-Assembler   
Published: 19.4.2008   
Download: [http://home.arcor.de/grasel/restarte.htm](http://home.arcor.de/grasel/restarte.htm)   
  
Download: [S2UTIME.ATR](attachments/S2UTIME.ATR)  
  
A small utility to read the data and time out of the SIO2USB Device and set the internal Clock in Sparta DOS.  
  
Tested with  
  
- BW-DOS 1.30  
- Sparta DOS 3.3a (X33A.DOS)  
- Sparta DOS 3.2d (X32D.DOS)  
- Real DOS 1.0a build 24 [http://www.tcpipexpress.com/realdos.html](http://www.tcpipexpress.com/realdos.html)  
- SpartaDOS X 4.41 [http://trub.atari8.info/index.php?ref=sdx_upgrade_en](http://trub.atari8.info/index.php?ref=sdx_upgrade_en)  
  
and with  
  
- Atari ROM E: Handler  
- Sparta DOS X 4.41 XEP80 Handler  
- Sparta DOS X 4.41 64 Char Handler (CON64)  
- Sparta DOS X 4.41 Quick E: Handler  
  
just load S2UTIME.COM. On BW-DOS you first need to load the Clock Driver "CLOCK ON"  
  
```
01000          .LI OFF
01010 **********************
01020 **                  **
01030 ** SPARTA DOS TIME  **
01040 **   UTILITY FOR    **
01050 **     SIO2USB      **
01060 ** (C) 2008 ABBUC   **
01070 ** LICENSE: GPLv3   **
01080 **                  **
01090 ** P: C. Strotmann  **
01100 ** H: T. Grasel     **
01110 **    H. Reminder   **
01120 **    E. Puetz      **
01130 **                  **
01140 ** VERSION 1.00     **
01150 **                  **
01160 **********************
01170          .LI OFF
01180 ;
01190 DOSVEC = $0A
01200 ZPF0   = $F0
01210 ZPF1   = ZPF0+1
01220 INITAD = $2E2
01230 DDEVIC = $300
01240 HATABS = $31A
01250 SDBASE = $700
01260 SDKRNL = $703
01270 SDDEV  = $761
01280 SDDATE = $77B
01290 SDTIME = SDDATE+3
01300 PORTB  = $D301
01310 EDITRV = $E400
01320 SIOV   = $E459
01330 VSETTD = $FFC3
01340 ------------------------------
01350          .OR $5000
01360          .OF D:S2UTIME.COM
01370 ------------------------------
01380 RETURN    RTS
01390 ------------------------------
01400 START
01410          JSR COUTINIT
01420          JSR BANNER
01430          JSR GETTIME
01440          BMI SIOERROR
01450          JSR TESTDATA
01460          JSR DETECTDOS
01470          JMP EXIT
01480 ------------------------------
01490 ERRORMSG
01500          JSR PRINT
01510          .HX FD ; Beep
01520          .AS "Error: "
01530          .HX EA
01540          RTS
01550 ------------------------------
01560 SIOERROR
01570          JSR ERRORMSG
01580          JSR PRINT
01590          .AS "during SIO Communication"
01600          .HX EA
01610          JMP EEXIT
01620 ------------------------------
01630 DATAERROR
01640          JSR ERRORMSG
01650          JSR PRINT
01660          .AS "wrong or incomplete data recieved"
01670          .HX EA
01680          JMP EEXIT
01690 ------------------------------
01700 EEXIT
01710          JSR PRINT
01720          .HX 9B
01730          .AS "Date/Time not set!"
01740          .HX 9BEA
01750          JMP TODOS
01760 ------------------------------
01770 BANNER
01780          JSR PRINT
01790          .AS "SIO2USB DATE/TIME UTILITY v1.0"
01800          .HX 9B
01810          .AS "(C) 2008 ABBUC/RAF"
01820          .HX 9BEA
01830          RTS
01840 ------------------------------
01850 DETECTDOS
01860          LDY #0
01870          LDA SDBASE,Y
01880          CMP #'S
01890          BNE ISREAL
01900          INY
01910          INY
01920          INY
01930          LDA SDBASE,Y
01940          CMP #'B
01950          BEQ BEWEDOS
01960 ; IS ORIGINAL SPARTADOS
01970          JSR PRINT
01980          .AS "Sparta DOS"
01990          .HX EA
02000          JSR DETECTED
02010          JMP SETTIME
02020 BEWEDOS
02030          JSR PRINT
02040          .AS "BW-DOS"
02050          .HX EA
02060          JSR DETECTED
02070          JSR PRINT
02080          .HX 9BEA
02090          JMP SETTIMEBW
02100 ISREAL
02110          CMP #'R
02120          BNE NOSPARTA
02130          JSR PRINT
02140          .AS "REALDOS"
02150          .HX EA
02160          JSR DETECTED
02170          JMP SETTIME
02180 NOSPARTA
02190          JSR PRINT
02200          .AS "No SPARTA compatible DOS"
02210          .HX EA
02220          JSR DETECTED
02230          LDA #$9B
02240          JSR COUT
02250          JMP EEXIT
02260 ------------------------------
02270 DETECTED
02280          JSR PRINT
02290          .AS " detected"
02300          .HX EA
02310          RTS
02320 ------------------------------
02330 COUTINIT
02340          LDY #$1E
02350 .1       LDA HATABS,Y
02360          CMP #'E
02370          BEQ .3
02380          DEY
02390          DEY
02400          DEY
02410          BPL .1
02420          JMP .2
02430 .3       LDA HATABS+1,Y
02440          STA ZPF0
02450          LDA HATABS+2,Y
02460          STA ZPF1
02470          LDY #7
02480          LDA (ZPF0),Y
02490          STA COUT2+1
02500          DEY
02510          LDA (ZPF0),Y
02520          STA COUT1+1
02530 .2       RTS
02540 ------------------------------
02550 COUT
02560          TAX
02570 COUT2    LDA #$F2
02580          PHA
02590 COUT1    LDA #$AF
02600          PHA
02610          TXA
02620          RTS
02630 ------------------------------
02640 PRINT
02650          PLA
02660          STA ZPF0
02670          PLA
02680          STA ZPF1
02690 .1       INC ZPF0
02700          BNE .2
02710          INC ZPF1
02720 .2       LDX #0
02730          LDA (ZPF0,X)
02740          CMP #$EA
02750          BEQ .3
02760          JSR COUT
02770          JMP .1
02780 .3       JMP (ZPF0)
02790 ------------------------------
02800 ISXL
02810          LDY #$1B
02820          LDA (DOSVEC),Y
02830          CMP #$FF
02840          BEQ .1
02850          JSR PRINT
02860          .AS " under ROM (XL/XE)"
02870          .HX 9BEA
02880          CLC
02890          RTS
02900 .1       JSR PRINT
02910          .AS " in main RAM"
02920          .HX 9BEA
02930          SEC
02940          RTS
02950 ------------------------------
02960 GETTIME
02970          LDX #$0B
02980 .1       LDA READRTC,X
02990          STA DDEVIC,X
03000          DEX
03010          BPL .1
03020          JMP SIOV
03030 ------------------------------
03040 TESTDATA
03050          LDA BUF
03060          CMP #6
03070          BNE .3
03080          LDA BUF+7
03090          CMP #$FF
03100          BEQ .2
03110 .3       JMP DATAERROR
03120 ; CONVERT BCD -> DEC
03130 .2       LDX #5
03140 .1       LDA BUF+1,X
03150          AND #$F0
03160          LSR
03170          LSR
03180          STA ZPF0
03190          LSR
03200          ADC ZPF0
03210          SBC BUF+1,X
03220          EOR #$FF
03230          STA BUF+1,X
03240          DEX
03250          BPL .1
03260 ;
03270          LDX #2
03280          LDY #$0F
03290 .4       LDA BUF+4,X
03300          STA (DOSVEC),Y
03310          DEY
03320          DEX
03330          BPL .4
03340 ;
03350          LDY #$10
03360          LDA BUF+3
03370          STA (DOSVEC),Y
03380          INY
03390          LDA BUF+2
03400          STA (DOSVEC),Y
03410          INY
03420          LDA BUF+1
03430          STA (DOSVEC),Y
03440          RTS
03450 ------------------------------
03460 SETTIME
03470          JSR ISXL
03480          LDA PORTB
03490          PHA
03500          AND #$FE
03510          STA PORTB
03520          JSR VSETTD
03530          PLA
03540          STA PORTB
03550          RTS
03560 ------------------------------
03570 SETTIMEBW
03580          JMP ($708)
03590 ; FALLTHROUGH
03600 ------------------------------
03610 EXIT
03620          JSR PRINT
03630          .AS "Date/Time set"
03640          .HX 9BEA
03650 ; FALLTHROUGH
03660 ------------------------------
03670 TODOS
03680          JMP (DOSVEC)
03690 ------------------------------
03700 READRTC
03710          .HX 71000240
03720          .DA BUF
03730          .HX 07008000
03740 ------------------------------
03750 BUF      .HX 00000000
03760          .HX 00000000
03770 ------------------------------
03780          .OR INITAD
03790          .DA START
03800 ------------------------------
```
  
---
Stefan Haubenthal | 22.04.2008 at 03:13 PM  
Short optimization:  
  
01900 INY 01910 INY 01920 INY 01930 LDA SDBASE,Y  
  
01900 LDA SDKRNL,Y  
  
---
Carsten Strotmann | 25.04.2008 at 03:30 PM  
  
Hello Stefan,  
  
thanks for the patch. Sometimes I don't see the forrest because of the trees ;)  
  
I'll change this in the next version (on VCFe in Munich this weekend). Also, the structure of the source can be optimized.  
  
Also, I would like to detect the different configurations of SpartaDOS X (banked, osram, none)  
