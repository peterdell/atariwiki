---
title: Hercules Graphic Card inside the ARGS PBI-ISA Interface
---
# Driver for a PC Hercules Monochrome graphics card inside the ARGS PBI-ISA Interface  
  
## VBI Driver that copies the ATARI Screen RAM into the Hercules Card RAM  
```
00010          .LI OFF
00020 ******************************
00030 *                            *
00040 * PROGRAMM:HERCULES DRIVER   *
00050 * AUTOR   :CARSTEN STROTMANN *
00060 * DATUM   :27.05.94          *
00070 * VERSION :1.0               *
00080 * FUER    :A.R.G.S           *
00090 *                            *
00100 ******************************
00110 ;
00120 ADRL     =   $D540
00130 ADRH     =   $D541
00140 ADRS     =   $D520
00150 DATREG   =   $D521
00160 ;
00170 ADRLCTL  =   $D542
00180 ADRHCTL  =   $D543
00190 ADRSCTL  =   $D522
00200 DATCTL   =   $D523
00210 ;
00220 SAVMSC   =   $58
00230 ROWCRS   =   $54
00240 COLCRS   =   $55
00250 LMARGN   =   $52
00260 RMARGN   =   $53
00270 ADRESS   =   $3F
00280 BOTSCR   =   $2BF
00290 COLLEN   =   $26A
00300 MSCLEN   =   $268
00310 ;
00320 LPEG     =   52
00330 HPEG     =   60
00340 ;
00350 SETVBV   =   $E45C
00360 XITVBV   =   $E462
00370 ;
00380 ;
00390          .OR $7800
00400          .OF "D:HERC.COM"
00410 ;
00420 ; INIT DER INTERFACEKARTE
00430 ; PIAS 68B21
00440 ;
00450 IINIT
00460          LDA #56
00470          STA ADRLCTL
00480          STA ADRHCTL
00490          STA ADRSCTL
00500          STA DATCTL
00510 ;
00520          LDA #255
00530          STA ADRL
00540          STA ADRH
00550          STA ADRS
00560          STA DATREG
00570 ;
00580          LDA #60
00590          STA ADRLCTL
00600          STA ADRHCTL
00610          STA ADRSCTL
00620          STA DATCTL
00630 ;
00640 ; INIT HERCULESKARTE TEXTMODUS
00650 ;
00660 HINIT
00670          LDA #16 ; RESET
00680          STA ADRS
00690          NOP
00700          NOP
00710          LDA #0
00720          STA ADRS
00730 ;
00740          STA ADRS
00750          LDA #3
00760          STA ADRH
00770          LDA #0
00780          JSR AUSGIO
00790 ;
00800          LDA #184
00810          STA ADRL
00820          LDA #32
00830          JSR AUSGIO
00840 ;
00850          LDX #0
00860 .1
00870          CPX #16 ; TEXTREG.
00880          BEQ .2  ; SETZEN
00890          LDA #180
00900          STA ADRL
00910          TXA
00920          JSR AUSGIO
00930 ;
00940          LDA #181
00950          STA ADRL
00960          LDA TXTINI,X
00970          JSR AUSGIO
00980          INX
00990          BNE .1
01000 ;
01010 .2
01020          LDA #184
01030          STA ADRL
01040          LDA #8
01050          JSR AUSGIO
01060 ;
01070          LDA #$98
01080          STA MSCLEN
01090          LDA #03
01100          STA MSCLEN+1
01110 ;
01120 CINIT    LDA #80
01130          STA COLLEN
01140          LDA #COPY
01150          STA ADRESS
01160          LDA /COPY
01170          STA ADRESS+1
01180          JSR AUSGZ
01190 ;
01200 CLEAR
01210          LDA #CLRBUF
01220          STA ADRESS
01230          LDA /CLRBUF
01240          STA ADRESS+1
01250          JSR AUSGZ
01260          LDA ZEILE
01271          BEQ .1
01280          JMP CLEAR
01290 .1
01291          JSR AUSGZ
01300          JSR SCRINIT
01310 ;        RTS
01320 ;
01330 XINIT    LDX RMARGN
01340          INX
01350          STX COLLEN
01360 ;
01370          JMP VBIINIT
01380 ;
01390 ------------------------------
01400 TXTINI   .DA #97,#80,#82,#15,#25,#6,#25,#25
01410          .DA #2,#13,#5,#12,#0,#0,#0,#0
01420 ------------------------------
01430 COPY     .AT "††††»ÂÚ„ıÏÂÛ†‘ÚÂÈ‚ÂÚ†≠†®„©†±ππ¥†–ËÔÂÓÈÿ†”ÔÊÙ√ÚÂ˜†≠†√·ÚÛÙÂÓ†”ÙÚÔÙÌ·ÓÓ†††††††††††"
01440          .BL 80,0
01450 CLRBUF   .BL 80,0
01460 ------------------------------
01470          .OR $0600
01480 ; DATENAUSGABE AUF IO-SPEICHER
01490 ; DES PC (SEG. 0), WERT MUSS
01500 ; IM AKKU STEHEN
01510 AUSGIO
01520          STA DATREG
01530          LDA #LPEG
01540          STA ADRLCTL
01550          LDA #HPEG
01560          STA ADRLCTL
01570          RTS
01580 ------------------------------
01590 ; DATENAUSGABE AUF SPEICHER
01600 ; DES PC (SEG 1-15), WERT MUSS
01610 ; IM AKKU STEHEN
01620 AUSGABE
01630          STA DATREG
01640          LDA #LPEG
01650          STA ADRSCTL
01660          LDA #HPEG
01670          STA ADRSCTL
01680          RTS
01690 ------------------------------
01700 ; AUSGABE EINER ZEILE
01710 ; AUS DEM BILDSCHIRMSPEICHER
01720 AUSGZ
01730          LDA #11
01740          STA ADRS
01750          CLC
01760          LDA ZEILE
01770          ASL
01780          TAX
01790          LDA HZEILTAB+1,X
01800          STA ADRH
01810          STA ZADRH
01820          LDA HZEILTAB,X
01830          STA ADRL
01840          STA ZADRL
01850 .1
01860          LDY #0
01870 AUSGZ11
01880          STA ADRL
01890          LDA (ADRESS),Y
01900          PHA
01910          AND #$7F
01920          TAX
01930          LDA INTTAB,X
01940          JSR AUSGABE
01950 ;
01960 ATTR
01970          INC ZADRL
01980          LDA ZADRL
01990          STA ADRL
02000          PLA
02010          AND #$80
02020          BEQ NORMAL
02030 INVERS
02040          LDA #112
02050          BNE ATTRIB
02060 NORMAL
02070          LDA #7
02080 ATTRIB
02090          JSR AUSGABE
02100 ;
02110          INY
02120          CPY COLLEN
02130          BEQ AUSGZEND
02140 ;
02150          INC ZADRL
02160          BEQ AUSGZ12
02170 ;
02180          LDA ZADRL
02190          BNE AUSGZ11
02200 AUSGZ12
02210          INC ZADRH
02220          LDA ZADRH
02230          STA ADRH
02240          LDA ZADRL
02250          BEQ AUSGZ11
02260 AUSGZEND
02270          DEC ZEILE
02280          SEC
02290          LDA ADRESS
02300          SBC COLLEN
02310          STA ADRESS
02320          BCS .1
02330          DEC ADRESS+1
02340 .1
02350          RTS
02360 ------------------------------
02370 HZEILTAB
02380          .DA $0000,$00A0,$0140,$01E0
02390          .DA $0280,$0320,$03C0,$0460
02400          .DA $0500,$05A0,$0640,$06E0
02410          .DA $0780,$0820,$08C0,$0960
02420          .DA $0A00,$0AA0,$0B40,$0BE0
02430          .DA $0C80,$0D20,$0DC0,$0E60
02440          .DA $0F00
02450 ------------------------------
02460 ZEILE    .HX 18
02470 ZADRL    .HX 00
02480 ZADRH    .HX 00
02490 ------------------------------
02500 VBI
02510          JSR AUSGZ
02520          JSR AUSGZ
02530 ;        JSR AUSGZ
02540          LDA ZEILE
02550          BPL .1
02560          JSR AUSGZ
02570          JSR SCRINIT
02580 .1
02590          JMP XITVBV
02600 ------------------------------
02610 SCRINIT
02620          LDA BOTSCR
02630          STA ZEILE
02640          DEC ZEILE
02650          CLC
02660          LDA SAVMSC
02670          ADC MSCLEN
02680          STA ADRESS
02690          LDA SAVMSC+1
02700          ADC MSCLEN+1
02710          STA ADRESS+1
02720          RTS
02730 ------------------------------
02740 VBIINIT
02750          LDA #7
02760          LDY #VBI
02770          LDX /VBI
02780          JSR SETVBV
02790 ;
02800          RTS
02810 ------------------------------
02820          .OR $0400
02830 INTTAB
02840          .HX 202122232425
02850          .HX 262728292A2B
02860          .HX 2C2D2E2F3031
02870          .HX 323334353637
02880          .HX 38393A3B3C3D
02890          .HX 3E3F40414243
02900          .HX 444546474849
02910          .HX 4A4B4C4D4E4F
02920          .HX 505152535455
02930          .HX 565758595A5B
02940          .HX 5C5D5E5F03C3
02950          .HX DED9B4BF2F5C
02960          .HX B0FEB1F67FC4
02970          .HX 5F0105DAC4C5
02980          .HX 02DCDBC2C1DD
02990          .HX C0EE18191A1B
03000          .HX 606162636465
03010          .HX 666768696A6B
03020          .HX 6C6D6E6F7071
03030          .HX 727374757677
03040          .HX 78797A7B7C7D7E7F
03050 ------------------------------
03060          .OR $2E0
03070          .DA IINIT
03080 ------------------------------

```
  
## BASIC Driver for Hercules Card  
```
00010          .LI OFF
00020 ******************************
00030 *                            *
00040 * PROGRAMM:HERCULES DRIVER   *
00050 * AUTOR   :CARSTEN STROTMANN *
00060 * DATUM   :27.05.94          *
00070 * VERSION :1.0               *
00080 * FUER    :BASIC             *
00090 *                            *
00100 ******************************
00110 ;
00120 ADRL     =   $D540
00130 ADRH     =   $D541
00140 ADRS     =   $D520
00150 DATREG   =   $D521
00160 ;
00170 ADRLCTL  =   $D542
00180 ADRHCTL  =   $D543
00190 ADRSCTL  =   $D522
00200 DATCTL   =   $D523
00210 ;
00220 ADRESS   =   $3F
00230 ;
00240 LPEG     =   52
00250 HPEG     =   60
00260 ;
00270 ;
00280          .OR $0600
00290          .OF "D:HINIT.OBJ"
00300 ;
00310 ; INIT DER INTERFACEKARTE
00320 ; PIAS 68B21
00330 ;
00340 BINIT
00350          PLA     ; BASIC PARAM.
00360          CMP #1
00370          BEQ .1
00380          RTS
00390 .1
00400          PLA
00410          STA ADRESS+1
00420          PLA
00430          STA ADRESS
00440 ; ADRESSE DER TABELLE
00450 ; BERECHNEN
00460          CLC
00470          LDA ADRESS
00480          ADC #$BD
00490          STA ADRESS
00500          BCC IINIT
00510          INC ADRESS+1
00520 IINIT
00530          LDA #56
00540          STA ADRLCTL
00550          STA ADRHCTL
00560          STA ADRSCTL
00570          STA DATCTL
00580 ;
00590          LDA #255
00600          STA ADRL
00610          STA ADRH
00620          STA ADRS
00630          STA DATREG
00640 ;
00650          LDA #60
00660          STA ADRLCTL
00670          STA ADRHCTL
00680          STA ADRSCTL
00690          STA DATCTL
00700 ;
00710 ; INIT HERCULESKARTE TEXTMODUS
00720 ;
00730 HINIT
00740          LDA #16 ; RESET
00750          STA ADRS
00760          NOP
00770          NOP
00780          LDA #0
00790          STA ADRS
00800 ;
00810          STA ADRS
00820          LDA #3
00830          STA ADRH
00840          LDA #0
00850          STA DATREG
00860          LDA #LPEG
00870          STA ADRLCTL
00880          LDA #HPEG
00890          STA ADRLCTL
00900 ;
00910          LDA #184
00920          STA ADRL
00930          LDA #32
00940          STA DATREG
00950          LDA #LPEG
00960          STA ADRLCTL
00970          LDA #HPEG
00980          STA ADRLCTL
00990 ;
01000          LDY #0
01010 .1
01020          CPY #16 ; TEXTREG.
01030          BEQ .2  ; SETZEN
01040          LDA #180
01050          STA ADRL
01060          TYA
01070          STA DATREG
01080          LDA #LPEG
01090          STA ADRLCTL
01100          LDA #HPEG
01110          STA ADRLCTL
01120 ;
01130          LDA #181
01140          STA ADRL
01150          LDA (ADRESS),Y
01160          STA DATREG
01170          LDA #LPEG
01180          STA ADRLCTL
01190          LDA #HPEG
01200          STA ADRLCTL
01210          INY
01220          BNE .1
01230 ;
01240 .2
01250          LDA #184
01260          STA ADRL
01270          LDA #8
01280          STA DATREG
01290          LDA #LPEG
01300          STA ADRLCTL
01310          LDA #HPEG
01320          STA ADRLCTL
01330 ;
01340          RTS
01350 ;
01360 ------------------------------
01370 TXTINI   .DA #97,#80,#82,#15,#25,#6,#25,#25
01380          .DA #2,#13,#5,#12,#0,#0,#0,#0
01390 ------------------------------
```
  
## Init Hercules Driver from Turbo-Basic  
```
1 DIM HI$(205),HP$(218),H$(80)
2 HINIT=ADR(HI$)
3 HPRINT=ADR(HP$)
4 HSTRING=ADR(H$)
5 OPEN #1,4,0,"D:HINIT.OBJ"
6 BGET #1,ADR(HI$),6
7 BGET #1,ADR(HI$),205
8 CLOSE #1
9 X=USR(HINIT,HINIT)
10 OPEN #1,4,0,"D:HPRINT.OBJ"
11 BGET #1,ADR(HP$),6
12 BGET #1,ADR(HP$),218
13 CLOSE #1
14 H$="                                      "
15 FOR U=0 TO 25
16   X=USR(HPRINT,HPRINT,0,U,40,HSTRING)
17   X=USR(HPRINT,HPRINT,40,U,40,HSTRING)
18 NEXT U
```
