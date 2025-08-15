---
title: Sector Copy
---
# CompyShop Sector Copy Source Code  
  
  
![](attachments/atari000.png)  
  
## Disk Image  
- [biboasm2.atr](attachments/biboasm2.atr)  
  
## SECTOR.ASM  
  
```
00010          .LI OFF
00020          .OR $2F00
00030          .OF "D1:SCOPY.COM"
00040 ------------------------------
00050 *********************
00060 ** SECTORCOPY MAIN **
00070 *********************
00080 ------------------------------
00090 S        SEI       STARTROUTINE
00100          LDA #0    Schiebt Pro-
00110          TAY       gramm unter
00120          STY $D40E das Betriebs
00130          STA $F0   System
00140          STA $F2
00150          LDA #$E0
00160          STA $F1
00170          LDA #$30  E000 -> 3000
00180          STA $F3
00190 .1       LDA ($F0),Y
00200          STA ($F2),Y
00210          INY
00220          BNE .1    Zeichensatz
00230          INC $F3   nach $3000
00240          INC $F1
00250          LDA $F1
00260          CMP #$E4  bis E400
00270          BNE .1
00280          LDA $D301
00290          AND #$FE  OS aus
00300          ORA #2    Basic aus
00310          STA $D301
00320          LDY #0
00330          LDA #$F0
00340          STA $F1
00350          LDA #$30  3000 -> F000
00360          STA $F3
00370 .2       LDA ($F2),Y
00380          STA ($F0),Y
00390          INY
00400          BNE .2
00410          INC $F3   Programm
00420          INC $F1   unter OS
00430          LDA $F1   schieben
00440          BNE .2
00450          LDY #ENRES-RESET
00460 .3       LDA RESET,Y
00470          STA $100,Y
00480          DEY      System-Reset
00490          BPL .3   Routine nach
00500          INY      $100 kopieren
00510          STY $244
00520          STY $C
00530          INY
00540          STY $9
00550          STY $D
00560          JMP $100 Zum Programm
00570 ------------------------------
00580 RESET    SEI      System-Reset
00590          STA $D40F
00600          LDA #0
00610          TAY
00620 .1       STA $D400,Y Hardware-
00630          STA $D000,Y  Register
00640          STA $D200,Y  loeschen
00650          INY
00660          BNE .1
00670          LDA $D301
00680          AND #$FE    OS aus
00690          ORA #$FC
00700          STA $D301
00710          LDA #$22    Bildschirm
00720          STA $D400   normal
00730          LDA #$F0    $F000=
00740          STA $D409   CHRBASE
00750          LDA #2
00760          STA $D401   CHACTL
00770          LDA #3
00780          STA $D20F   SIO-Status
00790          LDA #$40
00800          STA $D40E   NMIEN
00810          JSR CLRTI   Timeout-
00820 ;               Vector loeschen
00830          JMP SCOPY   START
00840 ENRES
00850 ------------------------------
00860          .OR $F400
00870          .TA $3400
00880 *
00890          .IN "D:COPY1.ASM
00900          .IN "D:COPY2.ASM
00910          .IN "D:DSKSYS.ASM
00920 ------------------------------
00930 DISPLY   .BL $F0
00940 ;
00950 DSBUF    .BL $50
00960 ------------------------------
00970 END ; Ende des Sector-Copiers
00980 ------------------------------
00990          .OR $FFFA
01000          .TA $3FFA
01010 *
01020          .DA PNMI  NMI-Vector
01030          .HX 0000  Reset-Vector
01040 ;          wird nicht benoetigt
01050          .DA RETIRQ IRQ-Vector
01060 ------------------------------
01070          .OR $2E0  File Start
01080          .DA S
01090 ------------------------------
```
  
## COPY1.ASM  
  
```
00010 ------------------------------
00020 ***********
00030 ** COPY1 **
00040 ***********
00050 ------------------------------
00060 ;
00070 ; ZERO-PAGE VARIABLEN FESTLEGEN
00080 ; DA KEIN BETRIEBSSYSTEM MEHR
00090 ; VORHANDEN IST, KOENNEN FAST
00100 ; ALLE ADRESSEN BENUTZT WERDEN
00110 ;
00120 SOURC    = $70
00130 SOUST    = $72
00140 DESTN    = $71
00150 DESST    = $73
00160 FORMT    = $74
00170 RETRY    = $75
00180 RAMDSK   = $76
00190 BYT1     = $7A / $7B
00200 EQUAL    = $7C
00210 DENS     = $7D
00220 CFIRST   = $7E
00230 SPFLAG   = $7F
00240 *
00250 SPTBL    = $1C - $1F
00260 RSECA    = $60 / $61
00270 RSECB    = $62 / $63
00280 RSECC    = $64 / $65
00290 *
00300 BANKS    = $66
00310 BANKNR   = $67
00320 MAXBANK  = $68
00330 SPBYT    = $69
00340 HIMEM    = $6A
00350 *
00360 SLEFT    = $37
00370 SROW     = $38
00380 SSKIP    = $39
00390 FBYT     = $3A
00400 DLEFT    = $3B
00410 DROW     = $3C
00420 DSKIP    = $3D
00430 FINC     = $3E
00440 FFIRST   = $3F
00450 *
00460 DUNIT    = $21
00470 DCOMND   = $22
00480 DSTATS   = $23
00490 DBUFLO   = $24
00500 DBUFHI   = $25
00510 DTIM     = $26
00520 DBYTLO   = $28
00530 DBYTHI   = $29
00540 DSECLO   = $2A
00550 DSECHI   = $2B
00560 ;
00570 PORTB    = $D301
00580 TSTBYT   = $4000
00590 ;
00600 ; AB LOMEM KOENNEN DATEN
00610 ; ABGELEGT WERDEN
00620 ;
00630 LOMEM    = $400
00640 ------------------------------
00650 ;
00660 ; DIE DISPLAY-LIST DES
00670 ; SECTOR-KOPIERERS
00680 ;
00690 DLIST  .HX 70707046
00700        .DA LINE
00710        .HX 47
00720        .DA HTEX
00730        .HX 40061046
00740        .DA LINE
00750        .HX 7042
00760        .DA DISPLY
00770        .HX 30023070027050
00780        .HX 02702002702002702046
00790        .DA LINE
00800        .HX 46
00810 RWLINE .DA SETUP
00820        .HX 1046
00830        .DA LINE
00840        .HX 41
00850        .DA DLIST
00860 ------------------------------
00870 ;
00880 ; TEXTE IM BILDSCHIRMFORMAT
00890 ;
00900 HTEX   .AT "   sectorcopy \^Q\^N\^T   "
00910        .AT -" \^Hp	 \^P\^V\^O\^X\^W  e\^Nreuss "
00920 LINE   .AT "--------------------"
00930 SETUP  .AT -"     einstellen "
00940 FMATIN .AT -"     formatieren   "
00950 INSOUR .AT -"  original diskette"
00960 INDEST .AT -"    ziel diskette  "
00970 INBOTH .AT -" disketten einlegen"
00980 DSKERR .AT -"  disk fehler \^C  "
00990 READIN .AT -"     sector         "
01000 ------------------------------
01010 ;
01020 ; START DES SEKTOR-KOPIERERS
01030 ;
01040 SCOPY    LDX #$FF
01050          TXS
01060          SEI
01070          LDA #DLIST DISPLAY-
01080          STA $D402  LIST SETZEN
01090          LDA /DLIST
01100          STA $D403
01110          LDY #4
01120 .1       LDA COLTB,Y   FARBEN
01130          STA $D016,Y   SETZEN
01140          DEY
01150          BPL .1
01160          STY RAMDSK
01170          LDA /SETUP
01180          STA RWLINE+1
01190          JSR CLRSCR  BILDSCHIRM
01200          LDX #4        LOESCHEN
01210          STX RETRY
01220          LDA #$28    HIGH-SPEED
01230 .2       STA SPTBL-1,X TABELLE
01240          DEX           AUF
01250          BNE .2        STANDARD
01260          STX FORMT
01270 ;
01280 ; TESTEN OB EINE RAMDISK VOR-
01290 ; HANDEN IST UND WIE GROSS
01300 ; DIESE IST
01310 ;
01320          LDX #$80  KLEINE
01330 .3       LDA $D40B VERZOEGERUNG
01340          BNE .3
01350          DEX
01360          BPL .3
01370          STX TSTBYT
01380          DEX
01390          STX PORTB
01400          LDY #$F     16 BANKS
01410          STY MAXBANK
01420 .4       LDY MAXBANK
01430          JSR SWITCH  DATEN IN
01440          STY TSTBYT  BANKS
01450          DEC MAXBANK SCHREIBEN
01460          BPL .4
01470          LDA #$FE
01480          STA PORTB
01490 *
01500          LDY #0
01510          STY BYT1
01520          STY MAXBANK
01530 *
01540          LDA TSTBYT  RAMDISK
01550          CMP #$FF    VORHANDEN?
01560          BNE MTEST
01570 *
01580 .5       LDY MAXBANK
01590          CPY #$10
01600          BCS .6
01610          JSR SWITCH  DATEN AUS
01620          LDA TSTBYT  RAMDISK
01630          CMP BYT1    AUSLESEN
01640          BMI .6      UND DABEI
01650          STA BYT1    MAXIMALE
01660          INC MAXBANK ANZAHL DER
01670          JMP .5      BANKS
01680 .6       LDA #$FE   FESTSTELLEN
01690          STA PORTB
01700          BNE MTEST
01710 *
01720 SWITCH   LDA PORTB  BANK
01730          AND #$23   EINSCHALTEN
01740          ORA BANKTB,Y
01750          STA PORTB
01760          RTS
01770 ------------------------------
01780 ;
01790 ; RAMDISK BANK-TABELLE
01800 ; FUER COMPY-SHOP RAMDISK UND
01810 ; 130 XE RAMDISK
01820 ;
01830 BANKTB   .HX CCC8C4C08C888480
01840          .HX 4C4844400C080400
01850 ------------------------------
01860 MTEST
01870 *         64K -> 00
01880 *        128K -> 04
01890 *        192K -> 08
01900 *        320K -> 10
01910 ------------------------------
01920 ;
01930 ; TEST OB EINE CARTRIDGE IM
01940 ; RECHNER STECKT
01950 ;
01960 NO64K    LDA #$80
01970          LDY $8000
01980          INC $8000
01990          CPY $8000   16K ?
02000          BEQ CHRAM
02010          LDA #$A0
02020          LDY $A000
02030          INC $A000
02040          CPY $A000   8K ?
02050          BEQ CHRAM
02060          LDA #$C0
02070 CHRAM    STA HIMEM
02080 ------------------------------
02090 ;
02100 ; TESTEN WIEVIELE LAUFWERKE
02110 ; ANGESCHLOSSEN SIND UND OB
02120 ; DIESE LAUFWERKE HIGH-SPEED
02130 ; FAEHIG SIND
02140 ;
02150          LDA #1     AB DRIVE 1
02160          JSR HSCHK  TESTEN
02170          BCC .1
02180          JMP SCOPY  KEINE DISK
02190 .1       STY SOUST  STATUS
02200          LDA DUNIT
02210          STA SOURC  ORIGINAL
02220          ORA #$10   IN ATASCII
02230          STA SDNR
02240          LDX #$40   KLEINE
02250          LDY #0     ZEIT-
02260 .2       DEY        VEZOEGERUNG
02270          BNE .2
02280          DEX
02290          BNE .2
02300          LDX DUNIT  DRIVE
02310          INX        +1
02320          TXA
02330          JSR HSCHK  TESTEN
02340          BCS .3
02350          LDA DUNIT
02360          BNE .4
02370 .3       LDA SOURC  ORIG=ZIEL
02380          LDY SOUST
02390 .4       STA DESTN
02400          STY DESST
02410          ORA #$10   IN ATASCII
02420          STA DDNR
02430 ;
02440 ; MENU-BILDSCHIRM AUFBAUEN
02450 ;
02460 START    JSR CLRSCR
02470          LDY #8
02480          JSR TXTOUT
02490          .AT "Original Laufwerk.... D"
02500 SDNR     .AT "1"
02510          .HX EA
02520          LDY #48
02530          JSR TXTOUT
02540          .AT "Ziel Laufwerk........ D"
02550 DDNR     .AT "1"
02560          .HX EA
02570 ;
02580 STA2     LDX #SETUP
02590          STX RWLINE
02600          LDY #120
02610          JSR CLRSC1
02620 ;
02630          LDY #94
02640          JSR TXTOUT
02650          .AT "Speicher: "
02660          .HX EA
02670          LDA HIMEM   =C0/A0/80
02680          AND #$60
02690          LSR         :8
02700          LSR
02710          LSR         =18/14/10
02720          LDX MAXBANK
02730          CPX #4      4 BANKS
02740          BCC .1
02750          CLC
02760          ADC #12
02770 .1       CPX #8      8 BANKS
02780          BCC .2
02790          CLC
02800          ADC #12
02810 .2       CPX #$10    16 BANKS
02820          BCC .3
02830          CLC
02840          ADC #12
02850 .3       TAX
02860          LDA #4      SPEICHER-
02870          STA BYT1    GROESSE
02880 .4       LDA MEMTB,X ANZEIGEN
02890          STA DISPLY,Y
02900          INY
02910          INX
02920          DEC BYT1
02930          BNE .4
02940 *
02950          LDA RAMDSK  DATEN IN
02960          BNE BEF0    RAMDISK ?
02970          LDY #125
02980          JSR TXTOUT
02990          .AT "\M^Yœ–‘…œŒ\^Y"
03000          .AT ".Von Ramdisk schreiben"
03010          .HX EA
03020          JMP BEF1
03030 BEF0     LDA SOURC   ORIG=ZIEL?
03040          CMP DESTN
03050          BEQ BEF1
03060          LDY #125
03070          JSR TXTOUT
03080          .AT "\M^Yœ–‘…œŒ\^Y"
03090          .AT ".Laufwerke austauschen"
03100          .HX EA
03110 BEF1     LDY #165
03120          JSR TXTOUT
03130          .AT "\M^Y”≈Ã≈√‘\^Y"
03140          .AT ".....Formatieren: "
03150          .HX EA
03160          LDA FORMT   FORMATFLAG
03170          BEQ BEF2
03180          JSR TXTOUT
03190          .AT "NEIN"
03200          .HX EA
03210          BEQ TXCOP
03220 BEF2     JSR TXTOUT
03230          .AT " JA "
03240          .HX EA
03250 TXCOP    LDY #205
03260          JSR TXTOUT
03270          .AT "\M^Y”‘¡“‘\^Y"
03280          .AT "......Diskette kopieren"
03290          .HX EA
03300 ;
03310 GETBEF   JSR GETKEY
03320          CMP #5      SELECT ?
03330          BEQ FORMAT
03340          CMP #6      START ?
03350          BEQ GOCOPY
03360          LDA RAMDSK  DATEN IN
03370          BEQ WFRD    RAMDISK ?
03380 ;
03390 EXCHAN   LDY SOURC   OPTION-
03400          LDX DESTN   TASTE
03410          STY DESTN
03420          STX SOURC   ORIGINAL
03430          TYA         UND ZIEL
03440          ORA #$10    TAUSCHEN
03450          STA DDNR
03460          TXA
03470          ORA #$10
03480          STA SDNR
03490          LDY SOUST
03500          LDX DESST
03510          STY DESST
03520          STX SOUST
03530          JMP START
03540 ;
03550 WFRD     LDY #203   VON RAMDISK
03560          STY DLEFT  SCHREIBEN
03570          LDX #$FF
03580          STX CFIRST
03590          INX
03600          STX DROW
03610          STX DSKIP
03620          STX EQUAL
03630          STX FFIRST
03640          LDY #120
03650          JSR CLRSC1
03660          LDY #120  ALTE ANZEIGE
03670 WFR1     LDA DSBUF,X    SETZEN
03680          STA DISPLY,Y
03690          INX
03700          INY
03710          CPY #200
03720          BNE WFR1
03730          LDA #$37
03740          STA DISPLY+201
03750          JMP WRITER  ZUR
03760 ;               SCHREIBROUTINE
03770 ;
03780 FORMAT   LDA FORMT  FORMATFLAG
03790          EOR #$FF   INVERTIEREN
03800          STA FORMT
03810          JMP STA2
03820 ;
03830 GOCOPY   LDA SOURC  START COPY
03840          EOR DESTN
03850          STA EQUAL  ORG=ZIEL
03860 *
03870          LDY #6
03880          LDA #0
03890          STA SPFLAG  POINTER
03900          STA FFIRST  LOESCHEN
03910 .1       STA SLEFT,Y
03920          DEY
03930          BPL .1
03940          STY CFIRST
03950          LDA #163    SCREEN-
03960          STA SLEFT   POSITIONEN
03970          LDA #203    DER BALKEN
03980          STA DLEFT   SETZEN
03990          LDY #120
04000          JSR CLRSC1
04010          LDA #$32
04020          STA DISPLY+161
04030          LDA #$37
04040          STA DISPLY+201
04050          STA RETRY
04060          LDX #1      SEKTOR 1
04070          STX RSECA
04080          DEX
04090          STX RSECA+1
04100 ;
04110 BEGIN    LDA EQUAL   ORG=ZIEL?
04120          BEQ .2
04130          LDX #INBOTH "BEIDE DSK
04140          LDA #$20     EINLEGEN"
04150 .1       STX RWLINE
04160          LDA #$20    AUF TASTE
04170          JSR HITRET  WARTEN
04180          CMP #6      START ?
04190          BEQ .3
04200          JMP STA2    ZUM MENU
04210 .2       LDX #INSOUR "ORIGINAL
04220          BNE .1       EINLEGEN"
04230 .3       LDA CFIRST  1.DURCH-
04240          BMI .4         GANG ?
04250          JMP COP3
04260 .4       LDA #$53    STATUS...
04270          STA DCOMND
04280          LDA #4      4 BYTES
04290          STA DBYTLO
04300          LDA #$40    READ
04310          STA DSTATS
04320          JSR SETBUF
04330          LDY SOURC
04340          JSR MOVSLO  SIO....
04350          LDY #133    SCRPOS
04360          JSR TXTOUT
04370          .AT "Density:  "
04380          .HX EA
04390          LDA LOMEM   STATUSBYTE
04400          AND #$A0
04410          STA DENS    MERKEN
04420          AND #$80    MEDIUM ?
04430          BNE MEDIUM
04440          LDA #5     INCREMENT
04450          STA FINC   FUER BALKEN
04460          LDA LOMEM
04470          AND #$20    DOUBLE ?
04480          BNE DOUBLE
04490          STA DENS
04500          JSR TXTOUT
04510          .AT "SINGLE"
04520          .HX EA
04530          JMP COPZD
04540 ;
04550 MEDIUM   LDX #8
04560          STX FINC
04570          JSR TXTOUT
04580          .AT "MEDIUM"
04590          .HX EA
04600          BEQ COPZD
04610 ;
04620 DOUBLE   JSR TXTOUT
04630          .AT "DOUBLE"
04640          .HX EA
04650 ;
04660 ; BEI SPEEDY 1050 KANN MIT
04670 ; 2 LAUFWERKEN DIE ZIELDISK
04680 ; FORMATIERT WERDEN, WENN DAS
04690 ; ORIGINAL EINGELESEN WIRD
04700 ;
04710 COPZD    LDA EQUAL
04720          BEQ COP3    ORG=ZIEL
04730          LDA FORMT
04740          BNE COP3    NO FORMAT
04750          BIT DESST
04760          BPL COP3    NO SPEEDY
04770          JSR SETDEN  DENSITY
04780          SEC          SETZEN
04790          JSR SETVER  VERIFY AUS
04800          TYA
04810          BMI COP3
04820 JCOP     LDA #$20    COMMAND 20
04830          STA DCOMND AUTO-FORMAT
04840          LDA #0
04850          STA DSTATS
04860          LDY DESTN
00518          JSR MOVSLO  SIO...
04880          TYA
04890          BPL FFOK
04900          JSR ERROR   FEHLER
04910          BCC JCOP    VERSUCH?
04920          JMP STA2    NEUSTART
04930 ;
04940 FFOK     INC FFIRST  1.DURCHG.
04950 COP3     LDA RSECA   START-
04960          STA RSECC   SEKTOR
04970          LDA RSECA+1 MERKEN
04980          STA RSECC+1
04990          LDY SOURC   ORG-DRIVE
05000          STY DUNIT
05010          BIT SPFLAG  HI-SPEED
05020          BPL .1
05030          LDA #$28    SLOW
05040          STA SPTBL-1,Y
05050 .1       JSR SETBUF  BUFFER
05060 .2       LDX SLEFT     SETZEN
05070          LDY SROW
05080          LDA SSKIP
05090          JSR DFUEL   BALKEN
05100          STA SSKIP    AKTUALI-
05110          STY SROW      SIEREN
05120          STX SLEFT
05130 .3       LDX #READIN "LESE -"
05140          STX RWLINE
05150          LDA #$40    GETBYTES
05160          STA DSTATS
05170          LDA RSECA   SEKTOR #
05180          STA DSECLO
05190          LDA RSECA+1
05200          STA DSECHI
05210          LDA #$52    READ
05220          STA DCOMND
05230          JSR SETLEN  LAENGE
05240          JSR MASTER  SIO...
05250          BCC .5
05260          BIT SPFLAG  ERROR?
05270          BPL .4
05280          JSR ERROR
05290          CMP #6      START ?
05300          BEQ .3
05310          CMP #5      SELECT ?
05320          BEQ .5
05330          JMP STA2    NEUSTART
05340 ;
05350 .4       LDY DUNIT
05360          LDA SPTBL-1,Y
05370          STA SPBYT
05380          LDA #$28
05390          STA SPTBL-1,Y
05400          DEC SPFLAG
05410          BNE .3
05420 .5       JSR ENDCHK  ENDE ?
05430          BCC .2
05440 ;
05450 ; DATEN SCHREIBEN
05460 ;
05470 WRITER   LDA RSECA   START-
05480          STA RSECB    SEKTOR
05490          LDA RSECA+1
05500          STA RSECB+1
05510          LDA EQUAL   ORG=ZIEL?
05520          BNE COPW1
05530          LDX #INDEST "ZIEL
05540          STX RWLINE   EINLEGEN"
05550          LDA #$20
05560          JSR HITRET  TASTE...
05570          CMP #5      OPTION ?
05580          BCC .1      VERIFY:
05590          LSR         SELECT=EIN
05600          JSR SETVER   START=AUS
05610          JMP COPW1
05620 .1       JMP STA2    NEUSTART
05630 ;
05640 COPW1    LDA RSECC   START-
05650          STA RSECA    SEKTOR
05660          LDA RSECC+1
05670          STA RSECA+1
05680          LDA DESTN   ZIELDRIVE
05690          STA DUNIT
05700          BIT SPFLAG  SLOW ?
05710          BPL .1
05720          LDY SOURC
05730          LDA SPBYT
05740          STA SPTBL-1,Y
05750 .1       LDA CFIRST  1.DURCHG.?
05760          BPL NOFORM
05770          LDA FFIRST  FORMAT OK?
05780          BNE NOFORM
05790          LDA FORMT   NO FORMAT
05800          BNE NOFORM
05810 .2       LDX #FMATIN "FORMAT.."
05820          STX RWLINE
05830          LDA DESST
05840          BPL .3
05850          JSR SETDEN  DENSITY
05860 .3       LDA #$80      SETZEN
05870          STA DBYTLO  $80 BYTES
05880          LDA #$22    COMMAND 22
05890          BIT DENS    MEDIUM ?
05900          BMI .5
05910          LDA DENS    DOUBLE ?
05920          BEQ .4
05930          ASL DBYTLO  $100 BYTES
05940 .4       LDA #$21    COMMAND 21
05950 .5       STA DCOMND
05960          LDA #$D5    $D500
05970          STA DBUFHI  BUFFER
05980          LDA #$40
05990          STA DSTATS  STATUS
06000          LDY DESTN
06010          JSR MOVSLO  SIO...
06020          TYA
06030          BPL NOFORM  FORMAT OK
06040          JSR ERROR
06050          BCC .2      WEITER
06060          JMP STA2    NEUSTART
06070 ;
06080 NOFORM   LDA #$50    PUTBYTE
06090          STA DCOMND
06100          INC CFIRST  1.DURCHG.
06110          JSR SETBUF  BUFFER
06120 .1       LDX #READIN "LESE-"
06130          STX RWLINE
06140          LDA #$80
06150          STA DSTATS  STATUS
06160          LDA RSECA
06170          STA DSECLO
06180          LDA RSECA+1
06190          STA DSECHI  SEKTOR #
06200          JSR SETLEN  LAENGE
06210          JSR EMPTY   SEKTOR
06220          BCS .2         LEER ?
06230          JSR MASTER  SIO...
06240          BCC .2      ERROR ?
06250          JSR ERROR
06260          BCC .1      WEITER
06270          JMP STA2    NEUSTART
06280 ;
06290 .2       LDX DLEFT
06300          LDY DROW
06310          LDA DSKIP
06320          JSR DFUEL   BALKEN
06330          STA DSKIP   AKTUALI-
06340          STY DROW    SIEREN
06350          STX DLEFT
06360          JSR ENDCHK  ENDE ?
06370          BCC .1
06380          PHP
06390          LDA DESST
06400          BPL .3
06410          LDA #$51    COMMAND 51
06420          STA DCOMND  MOTOR STOP
06430          LDA #0
06440          STA DSTATS
06450          LDY DESTN
06460          JSR MOVSLO  SIO...
06470 .3       PLP
06480          BEQ DONE    DISK ENDE
06490          LDA RSECB
06500          STA RSECA   ENDSEKTOR
06510          LDA RSECB+1  MERKEN
06520          STA RSECA+1
06530          LDA EQUAL   ORG=ZIEL?
06540          BNE .4
06550          JMP BEGIN
06560 .4       JMP COP3    WEITER...
06570 ------------------------------

```
  
## COPY2.ASM  
  
```
00010 ------------------------------
00020 ** COPY2 **
00030 ------------------------------
00040 ;
00050 ; LAUFWERKS-DENSITY EINSTELLEN
00060 ; MEDIUM MUSS BEI AUTO-FORMAT
00070 ; GESETZT WERDEN.
00080 ;
00090 SETDEN   LDA DENS
00100          BEQ .2
00110          BPL .1
00120          LDX #SETMD  MEDIUM
00130          LDY /SETMD
00140          BNE .3
00150 .1       LDX #SETDD  DOUBLE
00160          LDY /SETDD
00170          BNE .3
00180 .2       LDX #SETSD  SINGLE
00190          LDY /SETSD
00200 .3       STX DBUFLO
00210          STY DBUFHI
00220          LDA #$4F    COMMAND 4F
00230          STA DCOMND
00240          LDA #$C     12 BYTES
00250          STA DBYTLO
00260          LDA #$80    SENDEN
00270          STA DSTATS
00280          LDY DESTN   DRIVE
00290          JMP MOVSLO  SIO...
00300 ------------------------------
00310 ;
00320 ; FORMAT-VERIFY EIN- ODER
00330 ; AUSSCHALTEN
00340 ;
00350 SETVER   LDA #$10
00360          BCS .1
00370          ORA #$20    SEKTOR LOW
00380 .1       STA DSECLO
00390          LDA #0
00400          STA DSTATS  STATUS
00410          LDA #$44    COMMAND 44
00420          STA DCOMND
00430          LDY DESTN   DRIVE
00440          JMP MOVSLO  SIO...
00450 ------------------------------
00460 ;
00470 ; KOPIEREN BEENDET
00480 ;
00490 DONE     LDY #120
00500          LDX #0       DISPLAY
00510 .1       LDA DISPLY,Y  RETTEN
00520          STA DSBUF,X
00530          INX
00540          INY
00550          CPY #200
00560          BNE .1
00570          LDA CFIRST  ANZ.
00580          STA RAMDSK  DURCHG.
00590 ;
00600 ; ENDE-SOUND
00610 ;
00620          LDA #0
00630          STA $D208   AUDCTL
00640          LDY #$EF
00650 .2       STY $D201   AUDC1
00660          STY BYT1
00670          JSR LLL
00680          LDY BYT1
00690          DEY
00700          CPY #$DF
00710          BNE .2
00720          JMP STA2    NEUSTART
00730 ;
00740 LLL      LDX #$8
00750 .1       STX $D200   AUDF1
00760          LDY #$0
00770 .2       DEY
00780          BNE .2
00790          INX
00800          CPX #$50
00810          BNE .1
00820          RTS
00830 ------------------------------
00840 ;
00850 ; DATENLAENGE SETZEN
00860 ; SEKTORNUMMER AUSGEBEN
00870 ;
00880 SETLEN   LDA #$80
00890          STA DBYTLO  $80 BYTES
00900          LDA #0
00910          STA DBYTHI
00920          LDY #30
00930          LDA DSECHI
00940          JSR HXOUT   SEKTOR HI
00950          LDA DSECLO
00960          JSR HEXOUT  SEKTOR LO
00970          LDA DENS
00980          CMP #$20    DOUBLE ?
00990          BNE .2
01000          LDA DSECHI
01010          BNE .1
01020          LDA DSECLO
01030          CMP #4      SEKTOR <4
01040          BCC .2
01050 .1       ASL DBYTLO  $100 BYTES
01060          ROL DBYTHI
01070 .2       RTS
01080 ------------------------------
01090 ;
01100 ; SIO-AUFRUFEN / 2 VERSUCHE
01110 ;
01120 MASTER   LDA #2      2 VERSUCHE
01130          STA BYT1
01140          LDA DSTATS  STATUS
01150          STA BYT1+1    MERKEN
01160 .1       JSR US
01170          BPL .2      KEIN ERROR
01180          LDA BYT1+1  STATUS
01190          STA DSTATS   ZURUECK
01200          DEC BYT1    LETZTER
01210          BNE .1       VERSUCH?
01220          STY DSTATS
01230          SEC
01240          RTS      FEHLER
01250 .2       CLC
01260          RTS      KEIN FEHLER
01270 ------------------------------
01280 ;
01290 ; KOMMANDO IN NORMALER UEBER-
01300 ; TRAGUNGSRATE SENDEN
01310 ;
01320 MOVSLO   STY DUNIT
01330          LDA SPTBL-1,Y
01340          PHA
01350          LDA #$28
01360          STA SPTBL-1,Y
01370          JSR MASTER
01380          LDX DUNIT
01390          PLA
01400          STA SPTBL-1,X
01410          RTS
01420 ------------------------------
01430 ENDCHK   BIT DENS    MEDIUM?
01440          BPL .1
01450          LDA RSECA
01460          CMP #$10
01470          BNE .2      SEKTOR
01480          LDA RSECA+1    $410
01490          CMP #4      ERREICHT?
01500          BNE .2
01510          SEC
01520          RTS
01530 .1       LDA RSECA   SEKTOR
01540          CMP #$D0       $2D0
01550          BNE .2      ERREICHT?
01560          LDA RSECA+1
01570          CMP #2
01580          BNE .2
01590          SEC
01600          RTS
01610 .2       INC RSECA   SEKTOR+1
01620          BNE .3
01630          INC RSECA+1
01640 .3       LDA DBUFLO  BUFFER
01650          CLC          +LAENGE=
01660          ADC DBYTLO   BUFFER
01670          STA DBUFLO
01680          LDA DBUFHI
01690          ADC DBYTHI
01700          STA DBUFHI
01710          BIT BANKS   DATEN IN
01720          BMI SAVBNK  RAMDISK?
01730          TAY
01740          INY         $F000?
01750          CPY #$F1
01760          BEQ .6
01770          CPY #$D1    $D000?
01780          BEQ .5
01790          CPY HIMEM   MEMTOP?
01800          BNE .4
01810          LDA #$C0    BUFFER=
01820          STA DBUFHI    $C000
01830          LDA #0
01840          STA DBUFLO
01850 .4       CLC
01860          BCC ENDC3
01870 .5       LDA #0      BUFFER=
01880          STA DBUFLO    $D800
01890          LDA #$D8
01900          STA DBUFHI
01910          CLC
01920          BCC ENDC3
01930 ;
01940 .6       LDA MAXBANK ENDE
01950          BNE SWBANK   RAMDISK?
01960 ENDRAM   SEC
01970 ENDC3    LDA #$FF
01980          RTS
01990 ------------------------------
02000 ;
02010 ; BANK EINSCHALTEN/BUFFER=$4000
02020 ;
02030 SWBANK   LDY #$FF
02040          STY BANKS
02050          INY
02060          STY BANKNR
02070 SWB0     LDA PORTB
02080          AND #$23
02090          ORA BANKTB,Y
02100          STA PORTB
02110          LDA #0      BUFFER=
02120          STA DBUFLO     $4000
02130          LDA #$40
02140          STA DBUFHI
02150          CLC
02160          BCC ENDC3
02170 ------------------------------
02180 SAVBNK   CMP #$80    ENDE
02190          BCC ENDC3   RAMBANK?
02200          INC BANKNR  BANK+1
02210          LDY BANKNR
02220          CPY MAXBANK ENDE
02230          BEQ ENDRAM   RAMDISK?
02240          BNE SWB0
02250 ------------------------------
02260 ;
02270 ; DISKBUFFER AUF LOMEM SETZEN
02280 ; RAMBANKS ABSCHALTEN
02290 ;
02300 SETBUF   LDA #LOMEM
02310          STA DBUFLO
02320          LDA /LOMEM
02330          STA DBUFHI
02340          LDA #0
02350          STA BANKS
02360          LDA PORTB   CPU
02370          ORA #$10     ZUGRIFF
02380          STA PORTB     AUS
02390          RTS
02400 ------------------------------
02410 ;
02420 ; FEHLERMELDUNG UND FEHLERNUM-
02430 ; MER AUSGEBEN/AUF TASTE WARTEN
02440 ;
02450 ERROR    LDX #DSKERR "FEHLER.."
02460          STX RWLINE
02470          LDY #15     POS.15
02480          LDA DSTATS  NUMMER
02490          JSR HEXOUT
02500          LDA #$80
02510          JSR HITRET  TASTE ?
02520          BEQ .1
02530          SEC
02540          RTS
02550 .1       CLC
02560          RTS
02570 ------------------------------
02580 ;
02590 ; HEXZAHL IM ACCU UMWANDELN
02600 ; UND IN TEXTZEILE EINSETZEN
02610 ;
02620 HEXOUT   PHA         HIGH
02630          LSR          NIBBLE
02640          LSR
02650          LSR
02660          LSR
02670          JSR HXOUT
02680          PLA         LOW
02690          AND #$F      NIBBLE
02700 HXOUT    CMP #$A
02710          BCC .1
02720          ADC #6
02730 .1       ADC #$D0
02740          STA DSKERR,Y
02750          INY
02760          RTS
02770 ------------------------------
02780 ;
02790 ; BALKENPOSITION AKTUALISIEREN
02800 ;
02810 DFUEL    STY FBYT
02820          TAY
02830          INY        EIN SCHRITT
02840          CPY FINC     WEITER?
02850          BCC .2
02860          LDY FBYT
02870          INY
02880          CPY #4
02890          BCC .1
02900          INX
02910          LDY #0
02920 .1       LDA FTAB,Y ZEICHEN
02930          STA DISPLY,X  SETZEN
02940          LDA #0
02950          RTS
02960 .2       TYA
02970          LDY FBYT
02980          RTS
02990 ------------------------------
03000 ;
03010 ; BALKEN SETZT SICH AUS GRAFIK-
03020 ; ZEICHEN ZUSAMMEN " \^V \^Y \M^B \240  "
03030 ;
03040 FTAB     .HX 5659C280
03050 ;
03060 ;
03070 ;
03080 COLTB    .HX FA8A10CA10
03090 ;
03100 ; TEXTE DER SPEICHERGROESSE
03110 ; 16K / 8K / OHNE CARTRIDGE
03120 ;
03130 MEMTB .AT "40k 48k 56k "  64K
03140       .AT "104k112k120k"  128K
03150       .AT "168k176k184k"  192K
03160       .AT "296k304k312k"  320K
03170 ------------------------------
03180 ;
03190 ; LAUFWERK KONFIGURATIONSDATEN
03200 ; SINGLE/DOUBLE/MEDIUM-DENSITY
03210 ;
03220 SETSD    .HX 2800001200000080
03230          .HX FF000000
03240 SETDD    .HX 2800001200040100
03250          .HX FF000000
03260 SETMD    .HX 2800001A00040080
03270          .HX FF000000
03280 ------------------------------
03290 ;
03300 ; TESTEN OB ALLE BYTES IM
03310 ; BUFFER NULL SIND
03320 ;
03330 EMPTY    LDA FORMT   FORMATFLG
03340          BNE EMP2
03350          LDA DBUFLO  ADRESSE
03360          STA EMPVEC+1
03370          LDA DBUFHI
03380          STA EMPVEC+2
03390          LDY #0
03400 EMPVEC   LDA $AAAA,Y
03410          BNE EMP2
03420          INY
03430          CPY DBYTLO  ALLE BYTES
03440          BNE EMPVEC  GETESTET?
03450          SEC
03460          RTS
03470 EMP2     CLC
03480          RTS
03490 ------------------------------
03500 ;
03510 ; TEXT AN POSITION IM Y-REG.
03520 ; AUSGEBEN / ENDKENNUNG = $EA
03530 ;
03540 TXTOUT   PLA       TEXTADRESSE
03550          STA $43    VOM STACK
03560          PLA
03570          STA $44
03580 .1       INC $43   ADRESSE+1
03590          BNE .2
03600          INC $44
03610 .2       LDX #0
03620          LDA ($43,X)
03630          CMP #$EA  TEXT ENDE?
03640          BEQ .3
03650          STA DISPLY,Y
03660          INY
03670          BNE .1
03680 .3       JMP ($43) ZURUECK
03690 ------------------------------
03700 ;
03710 ; BILSCHIRM LOESCHEN
03720 ;
03730 CLRSCR   LDY #0
03740 CLRSC1   LDA #0
03750 .1       STA DISPLY,Y
03760          INY
03770          CPY #$F0  LAENGE $F0
03780          BNE .1
03790          RTS
03800 ------------------------------
03810 ;
03820 ; TON AUSGEBEN UND AUF TASTE
03830 ; WARTEN
03840 ;
03850 HITRET   STA $D200   AUDF1
03860          LDY #$EF
03870 .1       LDX #$FF
03880 .2       STX $D40A
03890          DEX
03900          BNE .2
03910          DEY
03920          STY $D201   AUDC1
03930          CPY #$E0
03940          BNE .1
03950          JSR GETKEY  TASTE?
03960          RTS
03970 ------------------------------
03980 ;
03990 ; AUF EINE FUNKTIONSTASTE
04000 ; WARTEN
04010 ;
04020 GETKEY   LDA $D01F
04030          CMP #7      KEINE
04040          BNE GETKEY   TASTE?
04050          LDX #0
04060 .1       DEX         ZEITVERZ.
04070          STX $D40A
04080          BNE .1
04090 .2       LDA $D01F   TASTE
04100          CMP #7      ENTPRELLEN
04110          BEQ .2
04120          LDY #$40
04130 .3       STA $D40A
04140          STY $D01F
04150          DEY
04160          BNE .3
04170          STY $4D
04180          RTS         ACCU=TASTE
04190 ------------------------------

```
  
## DSKSYS.ASM  
  
```
00010 ------------------------------
00020 ************
00030 ** DSKSYS **
00040 ************
00050 ------------------------------
00060 ;
00070 ; LAUFWERK TESTEN OB HIGH-SPEED
00080 ; MOEGLICH IST
00090 ;
00100 HSCHK    STA DUNIT   DRIVE NR.
00110          LDA #$3F    COMMAND 3F
00120          STA DCOMND
00130          LDX #0
00140          INX
00150          STX DBYTLO  1 BYTE
00160          LDA #$40
00170          STA DSTATS  GETBYTE
00180          JSR SETBUF  BUF.=LOMEM
00190          JSR US      SIO...
00200          TYA         OK
00210          BPL .2
00220          CMP #$8B    NO DRIVE?
00230          BEQ .1
00240          INC DUNIT   DRIVE+1
00250          LDA DUNIT
00260          CMP #5      DRIVE5?
00270          BCC HSCHK   WEITER...
00280          SEC
00290          RTS
00300 .1       LDY #0
00310          CLC
00320          RTS
00330 ;
00340 .2       LDA LOMEM   HIGH-SPEED
00350          LDY DUNIT
00360          STA SPTBL-1,Y  MERKEN
00370          LDY #$FF
00380          CLC
00390          RTS
00400 ------------------------------
00410 ;
00420 ; UNIVERSELLE SIO-ROUTINE
00430 ;
00440 US       LDY DUNIT   DRIVE NR.
00450          TYA
00460          ORA #$30
00470          STA $23A
00480          LDA DCOMND  KOMMANDO
00490          STA $23B
00500          LDA DSECLO  SEKTOR LO
00510          STA $23C
00520          LDA DSECHI  SEKTOR HI
00530          STA $23D
00540          LDA SPTBL-1,Y SPEED IN
00550          STA $D204      AUDF3
00560          LDA #0
00570          STA $D206   AUDF6
00580          TSX         STACK
00590          STX $318     RETTEN
00600 ;
00610 IO11     LDA RETRY  VERSUCHE
00620          STA $36      SETZEN
00630 IO12     LDA #0
00640          STA $30
00650          STA $319
00660          LDA #$3A
00670          STA $32    BUFFER $23A
00680          LDA #2
00690          STA $33
00700          LDA #4
00710          STA $34
00720          LDA #$34   COMMAND=
00730          STA $D303      LOW
00740          JSR SEND1  COM. SENDEN
00750          LDA DBUFLO
00760          STA $32    BUFFER
00770          LDA DBUFHI   SETZEN
00780          STA $33
00790          LDA DBYTLO LAENGE
00800          STA $34
00810          BIT DSTATS
00820          BPL IO2    SENDEN?
00830          JSR SEND1
00840 IO2      DEC $319
00850          JSR SETTI1 TIMEOUT
00860          BIT DSTATS     SETZEN
00870          BVC IO3    EMPFANGEN?
00880          JSR GET1
00890 IO3      LDA #$A0
00900          STA $D207  SOUND AUS
00910          LDA $10
00920          STA $D20E
00930          JSR CLRTI  TIMEOUT
00940          LDY $30       LOESCHEN
00950          STY DSTATS STATUS
00960          RTS
00970 ------------------------------
00980 SEND1    LDX #$80
00990 .1       DEX
01000          BNE .1
01010          LDA #$23   FUNKTION=
01020          JSR POKEY      SENDEN
01030          LDY #0
01040          LDA ($32),Y
01050          STA $31
01060          STA $D20D  BYTE SENDEN
01070 .2       INY
01080          CPY $34    ENDE?
01090          BEQ SENOUT
01100          LDA ($32),Y  BUFFER
01110          JSR PUTBYT    SENDEN
01120          JSR CHKSUM
01130          JMP .2      WEITER...
01140 ;
01150 SENOUT   LDA $31     CHECKSUMME
01160          JSR PUTBYT     SENDEN
01170 .1       LDA $D20E
01180          AND #8
01190          BNE .1
01200          LDX #0
01210          LDY #3      TIMEOUT
01220          JSR STOUT     SETZEN
01230          LDA #$C0    IRQ-STATUS
01240          STA $D20E     SETZEN
01250          JMP RECEIV  WARTEN...
01260 ------------------------------
01270 GET1     LDA #0      CHECKSUMME
01280          STA $31      LOESCHEN
01290          LDY #0
01300 .1       JSR GETBYT  DATENBLOCK
01310          STA ($32),Y  EMPFANGEN
01320          JSR CHKSUM
01330          INY
01340          CPY $34
01350          BNE .1
01360          JSR GETBYT  CHECKSUMME
01370          CMP $31
01380          BNE ERR8A   ERROR
01390          RTS
01400 ;
01410 ERR8A    LDA #$8A    FEHLER
01420 ERRO1    STA $30      AUSGEBEN
01430          LDX $318
01440          TXS
01450          BIT $319    RETRY?
01460          BMI .1
01470          DEC $36
01480          BEQ .1
01490          JMP IO12    WEITER
01500 .1       JMP IO3     ENDE
01510 ------------------------------
01520 ;
01530 ; TIME-OUT SETZEN UND AUF
01540 ; RUECKMELDUNG WARTEN
01550 ;
01560 SETTI1   LDX DCOMND  COMMAND
01570          CPX #$50     =FORMAT
01580          BCS SETTI2
01590          LDX #10     CA.1 MIN.
01600          BNE SETTI3
01610 SETTI2   LDX #1
01620 SETTI3   LDY #$60    CA.7 MIN
01630          JSR STOUT   TIMEOUT
01640 *                      SETZEN
01650 RECEIV   LDA #$13    LESEN
01660          JSR POKEY
01670          LDA #$3C
01680          STA $D303   AUF BYTE
01690          JSR GETBYT   WARTEN
01700          CMP #$41    "A"
01710          BEQ CLRTI
01720          CMP #$43    "C"
01730          BEQ CLRTI
01740          CMP #$45    "E"
01750          BEQ ERR90
01760          LDA #$8B    "N"
01770          BNE ERRO1   FEHLER 139
01780 ERR90    LDA #$90    FEHLER 144
01790          STA $30
01800 *
01810 CLRTI    LDY #0      TIME-OUT
01820          LDX #0       LOESCHEN
01830 STOUT    LDA #ERR8A  TIMER 1
01840          STA $226      VEKTOR
01850          LDA /ERR8A    SETZEN
01860          STA $227
01870 *
01880          TXA
01890          LDX #3
01900 .1       STA $D40A
01910          DEX
01920          BNE .1      TIMER 1
01930          STA $219      WERT
01940          STY $218      SETZEN
01950          RTS
01960 ------------------------------
01970 CHKSUM   CLC       CHECKSUMME
01980          ADC $31     ADDIEREN
01990          ADC #0
02000          STA $31
02010          RTS
02020 ------------------------------
02030 ;
02040 ; BYTE VOM LAUFWERK EMPFANGEN
02050 ;
02060 GETBYT   LDA $D20E   BYTE DA?
02070          AND #$20
02080          BNE GETBYT
02090          LDA #$DF    CLEAR
02100          STA $D20E   IRQ-FLAG
02110          LDA #$F8
02120          STA $D20E
02130          LDA $D20F
02140          STA $D20A   I/O-ERROR
02150          BPL JERR
02160          AND #$20
02170          BEQ JERR
02180          LDA $D20D   BYTE IN A
02190          RTS
02200 JERR     JMP ERR8A
02210 ------------------------------
02220 ;
02230 ; BYTE AN LAUFWERK SENDEN
02240 ;
02250 PUTBYT   PHA
02260 PUT1     LDA $D20E  POKEY
02270          AND #$10     BEREIT?
02280          BNE PUT1
02290          LDA #$EF   IRQ-FLAG
02300          STA $D20E    SETZEN
02310          LDA #$F8
02320          STA $D20E
02330          PLA
02340          STA $D20D  BYTE SENDEN
02350          RTS
02360 ------------------------------
02370 ;
02380 ; POKEY FUER EIN- UND AUSGABE
02390 ; VORBEREITEN
02400 ;
02410 POKEY    STA $D20F  SKCTL
02420          STA $D20A
02430          LDA #$28
02440          STA $D208  AUDCTL
02450          LDA #$A8
02460          STA $D207  SOUNDREG.
02470          LDA #$F8
02480          STA $D20E  IRQ-ENABLE
02490          RTS
02500 ------------------------------
02510 ************
02520 ** SYSTEM **
02530 ************
02540 ------------------------------
02550 ;
02560 ; DA KEIN BETRIEBSSYSTEM VOR-
02570 ; HANDEN IST, MUESSEN DIE
02580 ; INTERRUPTS SELBST BEHANDELT
02590 ; WERDEN.
02600 ; NMI-ROUTINE:
02610 ;
02620 PNMI     PHA
02630          LDA $D40F  RESET
02640          AND #$20   (OLDRUNNER)
02650          BEQ .1
02660          JMP $100   ZUM COPY
02670 ;
02680 .1       TXA        REGISTER
02690          PHA         RETTEN
02700          TYA
02710          PHA
02720          STA $D40F  NMI-STATUS
02730 ;
02740 ; TIMER 1 AUF NULL UEBERPRUEFEN
02750 ; WENN ABGELAUFEN IN TIMER-
02760 ; ROUTINE SPRINGEN
02770 ;
02780 NMIVEC   LDY $218
02790          BNE .1
02800          LDY $219
02810          BEQ .2     TIMER 1=0
02820          DEC $219
02830 .1       DEC $218   TIMER -1
02840          BNE .2
02850          LDY $219
02860          BNE .2
02870          JSR NMIIND TIMEOUT...
02880 .2       LDA #8
02890          STA $D01F
02900          PLA        REGISTER
02910          TAY         ZURUECK
02920          PLA
02930          TAX
02940          PLA
02950          RTI        NMI ENDE
02960 ------------------------------
02970 NMIIND   JMP ($226) TIMER1 VEC.
02980 ------------------------------
02990 ;
03000 ; IRQ-VECTOR
03010 ;
03020 RETIRQ   PHA
03030          LDA $D20E  IRQ-FLAG
03040          EOR #$FF    LOESCHEN
03050          STA $D20E
03060          LDA #0
03070          STA $D20E
03080          PLA
03090          RTI        IRQ ENDE
03100 ------------------------------
```
