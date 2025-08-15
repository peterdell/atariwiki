---
title: Speedy 1050 Backup
---
# Speedy 1050 Backup  
  
[atari001.png](attachments/atari001.png)  
  
## Disk Image  
- [biboass3.atr](attachments/biboass3.atr)  
  
## Source  
  
- [BACKUP.pdf](attachments/BACKUP.pdf)  
  
### BACKUP.ASM  
```
00010          .LI ON
00020 ------------------------------
00030 ;  SPEEDY BACKUP V 1.1 
00040 ; (P) THOMAS NIEHAUS -TABS-
00050 ; (C) 1986/87 COMPY-SHOP
00060 ;     --BIBO-ASSEMBLER
00070 ;       TOOLDISK 2 - 1987
00080 ------------------------------
00090          .LI OFF
00100          .OR $400
00110          .OF "D:BACKUP.COM"
00120          .DF "D:HS.DAT
00130 ------------------------------
00140          .OR $2500
00150 ------------------------------
00160 ;VERSCH
00170 ;IST EINE EINFACHE VERSCHIE-
00180 ;ROUTINE. DA DAS HAUPTPROGRAMM
00190 ;IN EINEM SPEICHERBEREICH LIEGT
00200 ;WO SICH NORMALERWEISE DAS DOS
00210 ;BEFINDET, MUESSEN WIR DAS
00220 ;PROGRAMM VOR DEM START IM
00230 ;SPEICHER VERSCHIEBEN.
00240 ------------------------------
00250 VERSCH   LDA #$10
00260          STA $F0
00270          STA $F2
00280          LDA #$06
00290          STA $F1
00300          LDA #$26
00310          STA $F3
00320          LDX #$14
00330          LDY #$00
00340 .1       LDA ($F2),Y
00350          STA ($F0),Y
00360          INY
00370          BNE .1
00380          INC $F1
00390          INC $F3
00400          DEX
00410          BNE .1
00420          JMP $610
00430 ------------------------------
00440          .OR $610
00450          .TA $2610
00460 ------------------------------
00470          .IN "D:EQUATES.ASM
00480          .IN "D:MENU.ASM
00490          .IN "D:COPY.ASM
00500          .IN "D:INIT.ASM
00510          .IN "D:DRIVE.ASM
00520 ------------------------------
00530          .OR $2E0
00540          .DA $2500
00550 ------------------------------
00560 ;ERKLAERUNGEN:
00570 ;DAS PROGRAMM KANN NUR VON DER
00580 ;DISKETTE AUF DIE DISKETTE
00590 ;ASSEMBLIERT WERDEN. EIN
00600 ;ARBEITEN MIT DER RAMDISK IST
00610 ;EBENFALLS MOEGLICH. ALLE
00620 ;INCLUDE DATEIEN (ZEILEN 150-
00630 ;190) MUESSEN DANN VON D:
00640 ;AUF DIE RAMDISK NUMMER GE-
00650 ;AENDERT WERDEN (ZB. D8:)!
00660 ;AUCH DIE DATENDATEI US.DAT
00670 ;MUSS DANN AUF D8:US.DAT GE-
00680 ;AENDERT WERDEN!
00690 ------------------------------
00700 ;HS.DAT
00710 ;IST EINE REINE DATENDATEI.
00720 ;SIE ENTHAELLT DIE HIGH-SPEED
00730 ;ROUTINE.
00740 ------------------------------
00750 ;EQUATES.ASM
00760 ;ENTHAELLT ALLE VOM PROGRAMM
00770 ;BENOETIGTEN SYSTEM ADRESSEN
00780 ------------------------------
00790 ;MENU.ASM
00800 ;IST DAS HAUPTMENU DES BACKUP
00810 ;PROGRAMMES. ALLE EINSTELLUNGEN
00820 ;KOENNEN VON HIER AUS VORGE-
00830 ;NOMMEN WERDEN.
00840 ------------------------------
00850 ;COPY.ASM
00860 ;ENTHAELLT IST DAS EIGENTLICHE
00870 ;KOPIERPROGRAMM. HIER SIND ALLE
00880 ;WICHTIGEN PROGRAMMTEILE ENT-
00890 ;HALTEN.
00900 ------------------------------
00910 ;INIT.ASM
00920 ;INITIALISIERT DAS KOMPLETTE
00930 ;SYSTEM.
00940 ------------------------------
00950 ;DRIVE.ASM
00960 ;BEINHALTET DIE ROUTINE, DIE
00970 ;ZUM LAUFWERK GESCHICKT WIRD.
00980 ------------------------------
00990 ;DAS FERTIG ASSEMBLIERTE PRO-
01000 ;GRAMM KANN NUR VOM DOS AUS
01010 ;GESTARTET WERDEN!
01020 ;EIN PROGRAMMSTART VOM BIBO-
01030 ;ASSEMBLER HER IST NICHT
01040 ;MOEGLICH.
01050 ------------------------------
01060 ;AENDERN SIE DAS PROGRAMM NACH
01070 ;IHREN WUENSCHEN ODER BEDUERF-
01080 ;NISSEN! VIELLEICHT IST KOENNEN
01090 ;SIE ES SOGAR VERBESSERN!
01100 ;MELDEN SIE SICH DANN BEI UNS!
01110 ;
01120 ;COMPY-SHOP 0208-497169
01130 ;
01140 ;            VIEL SPASS
01150 ------------------------------
```
  
### EQUATES.ASM  
  
```
00010 ------------------------------
00020              .LI ON
00030 ;"†≈—’¡‘≈”†"
00040              .LI OFF
00050 ------------------------------
00060 ; DATE :     18 / 09 / 1986
00070 ------------------------------
00080 ; ATARI  EQUATES :
00090 ------------------------------
00100 SAV1     = $C0   2 B.
00110 DRVSEL   = SAV1+2 1 B.
00120 SAV2     = SAV1+3 2 B.
00130 MAXSAV   = SAV1+5 2 B.
00140 CBUF     = $1000
00150 LOMEM    = $1A00
00160 HIMEM    = $2E6
00170 M1       = SAV1+7 1 B.
00180 M2       = SAV1+8 1 B.
00190 DLEN     = SAV1+9 2 B.
00200 TRACKNUM = SAV1+11 1 B.
00210 LTRACK   = SAV1+12 1 B.
00220 STRACK   = SAV1+13 1 B.
00230 HLEN     = SAV1+14 1 B.
00240 FORKEN   = SAV1+15 1 B.
00250 MAXDRV   = 2
00260 FDRV     = SAV1+16 1 B.
00270 BEGIN    = $8000
00280 FDCSTAT  = SAV1+17 1 B.
00290 DISPLAY  = SAV1+18 2 B.
00300 SLOC     = SAV1+20 2 B.
00310 DLOC     = SAV1+22 2 B.
00320 ------------------------------
00330 ;DRIVE ROUTINE POINTER
00340 ;DRIVE EQUATES :
00350 ------------------------------
00360 BUF      = $90
00370 XSAV     = BUF+2
00380 YSAV     = BUF+3
00390 HEADBUF  = $8800
00400 SECBUF   = $8C00 SECTOR BUFF
00410 RDHEAD   = $FF7E
00420 RDHD1    = $FF81
00430 X2WAIT   = $FF1B
00440 TRACK0   = $FF1E
00450 CSEC     = BUF+4
00460 TSEC     = BUF+5
00470 ------------------------------
00480 ;RDSEC1  = $FF66
00490 ;Y=0,(IND) = $19 BUFFER.
00500 ;(SECLEN)= $14 SEI $80
00510 ;SECTOR  = $0E
00520 ------------------------------
00530 SENDC    = $FF5A
00540 SENDA    = $FF57
00550 TRACKPO  = $FF21
00560 CONRES   = $FF2A
00570 MOTON    = $FF09
00580 CLRTRA   = $FFAE
00590 SDBTS    = $FF54
00600 SENDE    = $FF5D
00610 SDRDDP   = $FF15
00620 TSTWRP   = $FF6F
00630 MOTOFF   = $FF0F
00640 ------------------------------
```
  
### MENU.ASM  
  
```
00010 ------------------------------
00020          .LION
00030 ;"†Õ≈Œ’†"
00040          .LIOFF
00050 ------------------------------
00060 ;    STAND: 18/11/86'
00070 ------------------------------
00080 BASE     = $58    DISPLAY START
00090 HSCROLL  = $D404
00100 MAXSCROL = 145
00110 ------------------------------
00120 MENUEST  JSR RAMDISKINIT
00130          JSR OEFFNE
00140          JSR RDCAP
00150          JMP COPYST
00160 OEFFNE   JSR TEXTOUT
00170          .HX 7D9B
00180          .AS '   SPEEDY 1050 BACKUP INITIALIZER'
00190          .HX 9B9BEA
00200          RTS
00210 ------------------------------
00220 RDCAP    JSR TEXTOUT
00230          .AS 'RAM - SIZE : '
00240          .HX EA
00250          LDA RAMDISKFLG
00260          BEQ .1   NO RAMDISK LOCATED
00270          CMP #$10
00280          BEQ .2
00290          CMP #8
00300          BEQ .3
00310          CMP #4
00320          BEQ .4
00330          LDA #0
00340          STA RAMDISKFLG
00350 .1       JSR TEXTOUT
00360          .DA "MAX. 64 K BYTES",#$9B,#$EA
00370          RTS
00380 .2       JSR TEXTOUT
00390          .DA "320 K BYTES",#$9B,#$EA
00400          RTS
00410 .3       JSR TEXTOUT
00420          .DA "192 K BYTES",#$9B,#$EA
00430          RTS
00440 .4       JSR TEXTOUT
00450          .DA "128 K BYTES",#$9B,#$EA
00460          RTS
00470 ------------------------------
00480 VPX      .HX 0F
00490 HSCNT    .HX 00
00500 NOSCROL  .HX 00
00510 DEFVBI   .DA $E462
00520 ------------------------------
00530 ;"Õ≈Œ’≈†ƒ…”–Ã¡Ÿ†Ã…”‘"
00540 ------------------------------
00550 MENUDL   LDA #DL
00560          STA $230
00570          LDA /DL
00580          STA $231
00590          LDA #14
00600          STA $2C5
00610          LDA #2
00620          STA $2C6
00630          LDA $D6AE
00640          CMP #$A9
00650          BNE .1
00660          JSR $D6AE
00670          LDA $224
00680          STA DEFVBI
00690          LDA $225
00700          STA DEFVBI+1
00710 ------------------------------
00720 ;"…Œ…‘†…ÕÆ†÷¬…†§≤≤≤Æ§≤≤≥"
00730 ------------------------------
00740 .1       LDA #0
00750          STA $D40E
00760          LDA #VBI
00770          STA $222
00780          LDA /VBI
00790          STA $223
00800          LDA #DVBI
00810          STA $224
00820          LDA /DVBI
00830          STA $225
00840          LDA #$40
00850          STA $D40E
00860          RTS
00870 ------------------------------
00880 DVBI     LDX #$18
00890 .1       LDA $3CF,X
00900          AND #$7F
00910          STA CLK,X
00920          DEX
00930          BPL .1
00940          JMP (DEFVBI)
00950 ------------------------------
00960 VBI      LDA HSCNT
00970          CMP #MAXSCROL
00980          BCC .0
00990          LDA NOSCROL
01000          BMI .2
01010          LDA #TXTSP
01020          STA HSLMS
01030          LDA /TXTSP
01040          STA HSLMS+1
01050          LDA #MAXSCROL-44
01060          STA HSCNT
01070          LDA #$FF
01080          STA NOSCROL
01090 ------------------------------
01100 .0       LDX VPX
01110          DEX
01120          CPX #$C
01130          BCC .1
01140          STX HSCROLL
01150          STX VPX
01160          JMP $E45F
01170 .1       LDA #$F
01180          STA HSCROLL
01190          STA VPX
01200          INC HSCNT
01210          INC HSLMS
01220          BNE .2
01230          INC HSLMS+1
01240 .2       JMP $E45F
01250 ------------------------------
01260 ;"¡†Ω†”‘¡‘’”"
01270 ;"ÿ†Ω†”≈√‘œ“"
01280 ;"Ÿ†Ω†‘“¡√À"
01290 ------------------------------
01300 CLRBASE  LDA #19
01310          STA VAL
01320 .1       LDY TRACKNUM
01330          LDX VAL
01340          JSR CALC
01350          LDA #0
01360          STA (DISPLAY),Y
01370          DEC VAL
01380          BNE .1
01390          RTS
01400 PUTBASE  CPX #20
01410          BCS RTN1
01420          CPY #40
01430          BCS RTN1
01440          PHA
01450          JSR CALC
01460          LDA (DISPLAY),Y
01470          BEQ D
01480          PLA
01490          ORA #$80
01500          STA (DISPLAY),Y
01510 RTN1     RTS
01520 ------------------------------
01530 D        PLA
01540          STA (DISPLAY),Y
01550          RTS
01560 ------------------------------
01570 CALC     LDA #0
01580          STA $1
01590          DEX
01600          TXA
01610          ASL
01620          ASL
01630          ASL
01640          STA $0
01650          ASL
01660          ROL $1
01670          ASL
01680          ROL $1
01690          ADC $0
01700          BCC .1
01710          INC $1
01720          CLC
01730 .1       ADC BASE
01740          STA DISPLAY
01750          LDA $1
01760          ADC BASE+1
01770          STA DISPLAY+1
01780          RTS
01790 ------------------------------
01800 DL       .HX 707046
01810          .DA TXT1
01820          .HX 1000020002021042
01830 LMS      .DA $9C40
01840          .HX 020202020202
01850          .HX 020202020202
01860          .HX 020202020202
01870 ZDL      .HX 00
01880          .HX 52      ;H SCROLL
01890 HSLMS    .DA TXT2
01900          .HX 0046
01910          .DA MESSAGE
01920          .HX 41
01930          .DA DL
01940 MESSAGE  .AT '               '
01950          .AT '        '
01960 TXT1     .AT ' SPEEDY BACKUP V1.1'
01970          .AT '    '
01980          .AT '       TRACK    '
01990          .AT '   STATUS            '
02000          .AT '          1         2         3         '
02010          .AT '0123456789012345678901234567890123456789'
02020 TXTSP    .AT '                    '
02030          .AT '                    '
02040 TXT2     .AT '     COPYRIGHT BY  COMPY'
02050          .AT ' - SHOP MH  10 / 86  '
02060          .AT ' ***  '
02070          .AT ' -SPEEDY BACKUP V1.1 -'
02080          .AT '     BY    '
02090          .AT -'  TAPS  '
02100          .AT ' ,THOMAS NIEHAUS '
02110          .AT '(p)      '
02120 CLK      .AT '                    '
02130          .AT '                             '
02140          .AT '                    '
02150 MSOURCE
02160          .AT 'INSERT SOURCE,PLEASE'
02170 MDEST
02180          .AT ' INSERT DESTINATION '
02190 ------------------------------
02200 RAMDISKINIT
02210          LDA $D301
02220          STA PB
02230          LDA #$23
02240          STA $D301
02250          LDA #0
02260          STA $4000
02270          LDA PB
02280          STA $D301
02290          LDA #$23
02300          STA $4000
02310          STA $D301
02320          LDA $4000
02330          CMP #$23
02340          BEQ .2      NO RAMD.!
02350          LDY #0
02360          LDX #0
02370 .1       LDA $D301
02380          AND #$23
02390          ORA RDTAB,Y
02400          STA $D301
02410          LDA RDTAB1,X
02420          STA $4000
02430          INX
02440          INY
02450          INY
02460          INY
02470          INY
02480          CPX #4
02490          BCC .1
02500          LDA $D301
02510          AND #$23
02520          ORA #$CC
02530          STA $D301
02540          LDA $4000
02550          BCS .3      =JMP
02560 .2       LDA #0
02570 .3       STA RAMDISKFLG
02580          LDA PB
02590          STA $D301
02600          RTS
02610 ------------------------------
02620 RAMDISKFLG .HX 00
02630 PB       .HX 00
02640 RDTAB    .HX CCC8C4C0
02650          .HX 8C888480
02660          .HX 4C484440
02670          .HX 0C080400
02680 RDTAB1   .HX 100C0804
02690 ------------------------------
02700 ;"“¡Õƒ…”À‘“≈…¬≈“†‘≈”‘≈Œ"
02710 ;  
02720 ;"–¡“¡Õ≈‘≈“Ã…”‘≈†ƒ≈“†“¡Õƒ…”À†∫"
02730 ;
02740 RDSKPAR0 .DA $140
02750          .DA $A000
02760 ------------------------------
02770 ;"≈…Œ”–“’Œ«†–¡“¡Õ≈‘≈“†∫"
02780 ;X= LO ,Y = HI
02790 ;ACCU BIT0=0 READ
02800 ;ACCU BIT0=1 WRITE
02810 ------------------------------
02820 ;"“≈…»≈Œ∆œÃ«≈†ƒ≈“†≈Ã≈Õ≈Œ‘≈†∫"
02830 ;1.Sector No. Lo
02840 ;2.Sector No. Hi
02850 ;3.Buffer Adr. Lo
02860 ;4.Buffer Adr. Hi
02870 ;"“’≈√ÀÀ≈»“†∫"
02880 ;Y=$01 ERFOLGREICH
02890 ;Y=$FF FEHLER
02900 ------------------------------
02910 LFLG     .HX 00
02920 BANK     .HX 00
02930 LSEC     .HX 00
02940 HSEC     .HX 00
02950 ------------------------------
02960 ;"Œœ‘≈†∫"
02970 ;"√Ω∞†Ωæ†“¡Õƒ…”À÷≈“◊¡Ã‘’Œ«†Õ…‘†ÕÔˆÂÚ†°"
02980 ;"√Ω±†Ωæ†’≈¬≈“«…¬‘†ÿ¨Ÿ†Ω†¬’∆∆≈“¨†¬¡ŒÀ†…”‘†¬≈“≈…‘”†¡À‘…÷…≈“‘"
02990 ------------------------------
03000 RDSKVER  PHP
03010          AND #$7F
03020          STA LFLG
03030 ------------------------------
03040 ;"¡’∆†”‘¡√À†Ã…≈«‘† ≈‘⁄‘†”≈√‘œ“†ŒœÆ†Ãœ†œ¬≈Œ"
03050 ;"∆’≈“†±≤∏†”≈√‘œ“≈Œ†Ã…≈«‘†ƒ≈“†¬≈“≈…√»†ƒ≈“†”≈√‘œ“Œ’ÕÕ≈“Œ†⁄◊…”√»≈Œ"
03060 ------------------------------
03070 ;"a) 0-2047 fuer 256 KB Bank"
03080 ;"b) 0-1023 fuer 128 KB Bank"
03090 ;"c) 0- 511 fuer  64 KB Bank"
03100 ;"d) 0- ... fuer den linearen Speicher"
03110 ------------------------------
03120          LDA RDSKPAR0
03130          STA LSEC
03140          LDA RDSKPAR0+1
03150          STA HSEC
03160 ------------------------------
03170 ;"‘≈”‘†…∆†”≈√‘œ“†æΩ†§±¥∞"
03180 ------------------------------
03190          LDA HSEC
03200          BEQ .1
03210          CMP #2
03220          BCS .2
03230          LDA LSEC
03240          CMP #$40
03250          BCS .2
03260 .1       LDA LFLG
03270          ORA #$80
03280          STA LFLG
03290          BNE .3
03300 .2       LDA LSEC
03310          SEC
03320          SBC #$40
03330          STA LSEC
03340          LDA HSEC
03350          SBC #1
03360          STA HSEC
03370 ------------------------------
03380 ;"¬≈Õ≈“À’Œ«†∫"
03390 ;ACCU =MINUS  HEISST RAMDISK IM LINEAREN SPEICHER
03400 ;ACCU =PLUS  RAMDISK IN BANK LOGIK
03410 ;"Œœ◊†√¡Ã√’Ã¡‘≈†Õ≈Õœ“Ÿ†–œ”…‘…œŒ†¡Œƒ†¬¡ŒÀ": BANK = SECTOR/128
03420 ------------------------------
03430 .3       LDA HSEC
03440          STA BANK
03450          LDA LSEC
03460          ASL
03470          ROL BANK
03480 ------------------------------
03490 ;"–œ”ÆΩ†”≈√‘œ“†™†±≤∏"
03500 ------------------------------
03510          LDA #0
03520          LSR HSEC
03530          ROR LSEC
03540          ROR
03550          STA DLOC
03560          LDA LSEC
03570          LDX LFLG  ;TEST OF BANKED RAMDISK,MINUS SET = LINEAR MEMORY
03580          BPL .5
03590          TAX       ;SAVE HIGH BYTE OF CALCULATE POSITION
03600          LDA DLOC  ;GET LO BYTE AND ADD BOUNDARY
03610          CLC
03620          ADC #LOMEM
03630          STA DLOC
03640          TXA
03650          ADC /LOMEM
03660          STA DLOC+1
03670          BNE .6      =JMP
03680 .5       AND #$3F  ;HIGHER BIT'S DO NOT BUILD THE ADRESS
03690          CLC
03700          ADC #$40  ;BANK BASIS= $4000
03710          STA DLOC+1
03720 ------------------------------
03730 ;"«≈‘†”‘œ“≈†¬’∆∆≈“†∆“œÕ†”‘¡√À"
03740 ------------------------------
03750 .6       LDA RDSKPAR0+2
03760          STA SLOC
03770          LDA RDSKPAR0+3
03780          STA SLOC+1
03790 ------------------------------
03800 ;NOW, BANK NO. AND LOC HAS TOC CHECKED, IF AN ERROR OCCURED,
03810 ;THE MINUS FLAG WILL BE SET AND THE OPERATION IS ABORTED.
03820 ------------------------------
03830          LDA LFLG
03840          BPL .7
03850          LDA DLOC+1
03860          CMP HIMEM
03870          BCS ERR
03880          BCC .8      =JMP
03890 .7       LDA BANK   ; CHECK,IF CALCULATED BANK IS
03900          CMP RAMDISKFLG ; IN COMPUTER'S RAMDISK-SIZE
03910          BCS ERR
03920          LDA DLOC+1  ; CHECK, IF THERE'S A BANK OVERFLOW ERROR
03930          CMP #$80    ; NORMALLY,THIS ERROR CANNOT
03940          BCS ERR  ; OCCUR,BUT PERHAPS THERE'S A MISTAKE IN THIS PROGRAMM
03950 ------------------------------
03960 ;ALL CALCULATED PARAMETER'S WERE OKAY.LET'S MOVE
03970 ;THE MEMORY BLOCK !
03980 ;CAUTION: NO INTERRUPT IS DISABLED DURING BANK OPERATION !
03990 ------------------------------
04000 .8       LDX BANK
04010          LDA $D301
04020          AND #$23
04030          ORA RDTAB,X
04040          STA BANK
04050          LDA LFLG  TEST FOR RDSK
04060          BPL .9
04070          LDX $D301
04080          STX BANK
04090 .9       PLP    ; GET CARRY BACK AND TEST, IF DATA SHOULD BE MOVED
04100          BCS NOMOV
04110          AND #1  ;ACCU=1 WRITE
04120          BEQ SVD301
04130          LDA $D301  ;SAVE $D301 's  VALUE TO SWITCH
04140          STA .21+1  ; THE BANKS
04150 ;
04160          LDY #$7F
04170 .20      LDA (SLOC),Y
04180          LDX BANK  ;ENABLE BANK
04190          STX $D301
04200          STA (DLOC),Y
04210 .21      LDX #$FF
04220          STX $D301
04230          DEY
04240          BPL .20
04250          LDY #1  ;OKAY, 128 BYTES TRANSFERRED.
04260          RTS
04270 ------------------------------
04280 ;THE ERROR,THAT HAS BEEN OCCURED, IS MARKED WITH Y=FF
04290 ;AND SET MINUS FLAG !
04300 ------------------------------
04310 ERR      PLP     ; REGET PH WITH CARRY
04320          LDY #$FF
04330          RTS
04340 ------------------------------
04350 ; THIS PART IS ADVANCED READ FOR RAMDISK !
04360 ------------------------------
04370 SVD301   LDA $D301  ;SAVE $D301 's  VALUE TO SWITCH
04380          STA .22+1  ; THE BANKS
04390          LDY #$7F
04400 .21      LDX BANK  ;ENABLE BANK
04410          STX $D301
04420          LDA (DLOC),Y
04430 .22      LDX #$FF
04440          STX $D301
04450          STA (SLOC),Y
04460          DEY
04470          BPL .21
04480          LDY #1   ;OKAY, 128 BYTES TRANSFERRED.
04490          RTS
04500 NOMOV    LDA BANK
04510          STA $D301
04520          LDX DLOC
04530          LDY DLOC+1
04540          LDA #1
04550          RTS
04560 ------------------------------
04570 ;HERE'S THE 'SPEEDY DRIVES' ROUTINE
04580 ------------------------------
04590 SPEEDYD  JSR TEXTOUT
04600          .AS '    SPEEDY  DRIVES :'
04610          .HX EA
04620          LDA #1
04630          STA DRVSEL
04640 TSTDRVL  LDA DRVSEL
04650          JSR SELDRV
04660          BCS .2
04670          PHA
04680          JSR TEXTOUT
04690          .DA " D",#$EA
04700          PLA
04710          CLC
04720          ADC #$30
04730          JSR EOUT
04740          INC DRVSEL
04750          JMP TSTDRVL
04760 .2       LDA #$9B
04770          JMP EOUT
04780 ------------------------------
04790 ;RAMDISK STATUS MESSAGE (IF R.D. PRESENT)
04800 ------------------------------
04810 RDSKSTAT .HX 00
04820 ------------------------------
04830 RDSTAT   LDA RAMDISKFLG
04840          BEQ .1
04850          JSR TEXTOUT
04860          .AS '    RAMDISK STATUS : '
04870          .HX EA
04880          LDA RDSKSTAT
04890          BEQ .2
04900          JSR TEXTOUT
04910          .DA "USED",#$9B,#$EA
04920 .1       RTS
04930 ------------------------------
04940 .2       JSR TEXTOUT
04950          .DA "FREE",#$9B,#$EA
04960          RTS
04970 ------------------------------
04980 ;"Õ≈Œ’≈†∆’Œ√‘…œŒ”†¡∆‘≈“†Õ¡…Œ†Õ≈Œ’≈"
04990 ------------------------------
05000 MAXPAR   = 6
05010 ------------------------------
05020 MENUE    JSR OPENSCR
05030          LDA $230
05040          STA DISPLAY
05050          LDA $231
05060          STA DISPLAY+1
05070          LDY #$1C
05080          LDA #$10
05090          STA (DISPLAY),Y
05100          INY
05110          LDA #1    ; DLIST JUMP
05120          STA (DISPLAY),Y
05130          INY
05140          LDA #ZDL
05150          STA (DISPLAY),Y
05160          INY
05170          LDA /ZDL
05180          STA (DISPLAY),Y
05190          LDA #0
05200          STA $52
05210          JSR TEXTOUT
05220          .HX 7D9B
05230          .AS '      *** SPEEDY PARAMETER MENUE ***'
05240          .HX 9B9B9B
05250 ------------------------------
05260          .DA "  1: VERIFY WRITES",#$9B
05270          .DA "  2: R/W RETRIES",#$9B
05280          .DA "  3: R/W BY DISK CHANGE",#$9B
05290          .DA "  4: TRACK ANALYZING MODE",#$9B
05300          .DA "  5: SOURCE DRIVE",#$9B
05310          .AS "  6: DESTINATION DRIVE"
05320          .HX 9B9B9B
05330 ------------------------------
05340          .DA "†√’““≈Œ‘†»¡“ƒ◊¡“≈†–¡“¡Õ≈‘≈“†∫†",#$9B,#$EA
05350 ------------------------------
05360          JSR RDCAP
05370          JSR RDSTAT
05380          JSR SPEEDYD
05390 ------------------------------
05400 ;"–¡“¡Õ≈‘≈“†¡’”«≈¬≈Œ"
05410 ------------------------------
05420          LDA #2
05430          STA $52
05440          LDA NOSCROL
05450          CMP #$FF
05460          BNE NOLAUF
05470          JSR SETSC   ; SETZE LAUFBAND IN BEWEGUNG !
05480 ------------------------------
05490 ;"Œ’Œ†–¡“¡Õ≈‘≈“†÷œŒ†À≈Ÿ¬œ¡“ƒ†”≈‘⁄≈Œ"
05500 ------------------------------
05510 NOLAUF   LDA #0
05520          STA VAL
05530 .2       LDA VAL    ; HOLE TABELLEN POSITION
05540          JSR PARSET
05550          INC VAL
05560          LDA VAL
05570          CMP #MAXPAR  ;6
05580          BCC .2
05590 MENUEKEY JSR GETKEY
05600          CMP #27     ESCAPE ?
05610          BEQ .27
05620          SEC
05630          SBC #$31
05640          BMI MENUEKEY
05650          CMP #MAXPAR  ;6
05660          BCS MENUEKEY
05670          TAY
05680          ASL
05690          TAX
05700          LDA VECTAB+1,X
05710          PHA
05720          LDA VECTAB,X
05730          PHA
05740          TYA
05750          RTS
05760 ------------------------------
05770 .27      JMP BIGST
05780 ------------------------------
05790 VECTAB   .DA FUNC1-1
05800          .DA FUNC2-1
05810          .DA FUNC3-1
05820          .DA FUNC4-1
05830          .DA FUNC5-1
05840          .DA FUNC6-1
05850 ------------------------------
05860 FUNC1    PHA
05870          LDA PVERIFY  ;VERIFY ON/OFF
05880          EOR #$80
05890          STA PVERIFY
05900          PLA
05910          JSR PARSET
05920          JMP MENUEKEY
05930 ------------------------------
05940 FUNC2    PHA
05950          INC PRETRY  ; RERIES
05960          LDA PRETRY
05970          CMP #5  ;MAX 5 RETRIES
05980          BCC .1
05990          LDA #0
06000          STA PRETRY
06010 .1       PLA
06020          JSR PARSET
06030          JMP MENUEKEY
06040 ------------------------------
06050 FUNC3    PHA
06060          LDA PCHANGE ; AUTOMATIC COPY
06070          EOR #$80
06080          STA PCHANGE
06090          PLA
06100          JSR PARSET
06110          JMP MENUEKEY
06120 ------------------------------
06130 FUNC4    JMP MENUEKEY  ; TRACK ANALYSING MODE SELECT :
06140 ------------------------------
06150 FUNC5    PHA     ; CHANGE SOURCE DRIVE
06160          INC PSOURCE
06170          LDA PSOURCE
06180          JSR SELDRV
06190          BCC .1
06200          LDA #1
06210          STA PSOURCE
06220 .1       PLA
06230          JSR PARSET
06240          JMP MENUEKEY
06250 ------------------------------
06260 FUNC6    PHA    ;CHANGE DESTINATION DRIVE
06270          INC PDEST
06280          LDA PDEST
06290          JSR SELDRV
06300          BCC .1
06310          LDA #1
06320          STA PDEST
06330 .1       PLA
06340          JSR PARSET
06350          JMP MENUEKEY
06360 ------------------------------
06370 ;"”≈‘⁄‘†ƒ≈Œ†–¡“¡Õ≈‘≈“†¡’∆†ƒ≈Œ†¬…Ãƒ”√»…“Õ"
06380 ------------------------------
06390 PARSET   STA VAL  ;TABELLEN POSITION
06400          TAX    ;  IN DEN INDEX
06410          LDY MTAB,X  ; NUN HOLE DIE VERTICAL POSITION AUS DER TABELLE
06420          LDA MTAB2,X  ; HOLE DAS FLAG
06430          LSR     ; SETZE ES IN CARRY
06440          LDX VAL  ; NUN LADE DEN PARAMETER IN DEN ACCU
06450          LDA PVERIFY,X
06460 ;        JMP HMENUE  ; AN SCHIRM AUSGEBEN
06470 ------------------------------
06480 ;"‘»…”†“œ’‘…Œ≈†–’‘”†‘»≈†–¡“¡Õ≈‘≈“”†”‘¡‘’”†œŒ‘œ†«“Æ∞†”√“≈≈Œ"
06490 ;CARRY = 0 AND :
06500 ; ACCU = 0  <=> "NOT AVIABLE"
06510 ; ACCU = 1-$7F  <=> "YES"
06520 ; ACCU = $80-$FF  <=> "NO"
06530 ;
06540 ; CARRY = 1 AND :
06550 ;  ACCU = HEXNUMBER
06560 ;
06570 ;Y REGISTER <=> VERTICAL POSITION
06580 ------------------------------
06590 HMENUE   STY $54  ; SET VERTICAL POSITION
06600          LDY #26  ; HORIZONTAL POSITION
06610          STY $55
06620          BCS .3
06630          TAY     ; REFRESH CPU FLAG'S
06640          BEQ .2
06650          BPL .1
06660          JSR TEXTOUT
06670          .AS 'NO           '
06680          .HX EA
06690          RTS
06700 .1       JSR TEXTOUT
06710          .AS 'YES          '
06720          .HX EA
06730          RTS
06740 .2       JSR TEXTOUT
06750          .DA "NOT AVAILABLE",#$EA
06760          RTS
06770 ------------------------------
06780 .3       JMP PHEXOUT
06790 ------------------------------
06800 ;"≈Ã≈Õ≈Œ‘”†œ∆†–¡“¡Õ≈‘≈“†Ã…”‘†∫"
06810 ------------------------------
06820 PVERIFY  .HX 01
06830 PRETRY   .HX 03
06840 PCHANGE  .HX 81
06850 PTRKAN   .HX 00
06860 PSOURCE  .HX 01
06870 PDEST    .HX 01
06880 VAL      .HX 00
06890 MTAB     .HX 040506070809
06900 MTAB2    .HX 000100000101
06910 ------------------------------
06920 SETSC    LDA #$F
06930          STA VPX
06940          LDA #0
06950          STA HSCNT
06960          STA NOSCROL
06970          LDA #TXT2
06980          STA HSLMS
06990          LDA /TXT2
07000          STA HSLMS+1
07010          RTS

```
  
### COPY.ASM  
  
```
00010 ------------------------------
00020          .LION
00030 ;"†√œ–Ÿ†"
00040          .LIOFF
00050 ------------------------------
00060 ;  STAND :  05/11/86'
00070 ------------------------------
00080 ;DRIVE INITIALISATION: SCHICKE
00090 ;COPY ROUTINE NACH $8000
00100 ------------------------------
00110 COPYST   JSR LOCSPEEDY
00120          JSR DRVINIT
00130          JSR TEXTOUT
00140          .AS 'STATUS OK. PRESS <RETURN> '
00150          .HX EA
00160          JSR RETURN
00170 ------------------------------
00180 BIGST    LDA #BIGST
00190          STA $C
00200          LDA /BIGST
00210          STA $D
00220          LDX #$FF
00230          TXS
00240          LDX #20
00250          LDA #0
00260 .1       STA MESSAGE,X
00270          DEX
00280          BPL .1
00290          JSR OPENSCR
00300          JSR SETSC
00310          JSR MENUDL  LABEL "S"
00320          JSR TEXTOUT
00330          .BL 7,$9B
00340          .DA "          (C)  COPY DISK",#$9B
00350          .DA "          (M)    MENUE",#$9B,#$EA
00360 ------------------------------
00370          LDA RDSKSTAT ; IST DIE KOMPLETTE DISKETTE IN DIE RAMDISK GEGANGEN ?
00380          BEQ PH1
00390          JSR TEXTOUT
00400          .DA "          (W)  WRITE FROM",#$9B
00410          .DA "                RAMDISK",#$9B,#$EA
00420 ------------------------------
00430 PH1      JSR GETKEY
00440          CMP #'C
00450          BEQ PH2
00460          CMP #'M
00470          BNE .1
00480          JMP MENUE
00490 .1       CMP #'W
00500          BNE PH1
00510          LDA RDSKSTAT ; IST DIE KOMPLETTE DISKETTE IN DIE RAMDISK GEGANGEN ?
00520          BEQ PH1
00530 ------------------------------
00540 ;SCHREIBE AUS RAMDISK
00550 ------------------------------
00560          LDA #$7D
00570          STA TANDEM
00580          JSR EOUT    ; CLEAR SCREEN
00590          LDA #0
00600          STA RSEC
00610          STA RSEC+1
00620          STA STRACK
00630          LDA #40
00640          STA TRACKNUM
00650          JSR DEST
00660          LDA PDEST
00670          JSR BACKUP
00680          JMP COPYEND
00690 ------------------------------
00700 TANDEM   .HX 00
00710 ------------------------------
00720 ;COPY MIT 1 ODER 2 LAUFWERKEN
00730 ------------------------------
00740 PH2      LDA PSOURCE
00750          CMP PDEST
00760          BNE .1
00770          JMP PH3
00780 .1       LDA #0
00790          STA TANDEM  ; COPY MIT 2 LAUFWERKEN
00800          JSR TEXTOUT
00810          .HX 7D9B9B9B9B9B
00820          .DA "INSERT DISKS, PLEASE   AND HIT RETURN",#$9B,#$EA
00830          JSR RETURNG
00840          LDA #$7D
00850          JSR EOUT
00860          JMP SDRV
00870 ------------------------------
00880 PH3      LDA #1
00890          STA TANDEM
00900          JSR OPENSCR
00910          JSR MENUDL
00920          JSR SOURCE
00930 ------------------------------
00940 ;COPY TEIL 1: DATEN EINLESEN
00950 ;DAS TRACK 0 KOMMANDO WIRD
00960 ;BENUTZT, UM EINE KOPF-POSI-
00970 ;TIONIERUNG ZU VERMEIDEN
00980 ------------------------------
00990 SDRV     LDA PSOURCE ;SOURCE DRIVE
01000          LDX #TRK00  ;SPRUNG VECTOR AUF
01010          LDY /TRK00  ;TRACK 0 EINSPRUNG SETZEN
01020          CLC         ;CARRY = 1 BEDEUTET DIREKTE RUECKMELDUNG VOM LAUFWERK
01030          JSR DRVJMP
01040          LDA #0      ;TRACKREGISTER AUF 0
01050          STA TRACKNUM
01060          STA LTRACK
01070          STA STRACK
01080          STA RSEC
01090          STA RSEC+1
01100 ------------------------------
01110 ; NOTE: TRACKNUM IST DAS
01120 ; AKTUELLE TRACK REGISTER
01130 ; LTRACK UND STRACK MARKIEREN
01140 ; LOWER UND HIGHER TRACK
01150 ; RAMDISKFLG KENNZEICHNET DIE
01160 ; VERWENDETE RAMDISK.
01170 ; RAMDISKFLG=0 BEZEICHNET KEINE         RAMDISK
01180 ; IN DAS RAMDISKFLG SOLLTE KEIN         WERT GELADEN WERDEN, DA
01190 ; SONST DER RECHNER ABSTUERZEN          KOENNTE!
01200 ; UNTER 'RDSKPAR0' SIND DIE PARA        METER WIE FOLGT ABGELEGT:
01210 ;       
01220 ; RDSKPAR0+0/+1 =RAMDISKSECTOR
01230 ; RDSKPAR0+2/+3 =BUFFER.
01240 ------------------------------
01250 L991     JSR ESCCHECK
01260 L88      LDX #SIOT2
01270          LDY /SIOT2
01280          JSR SIOINIT0
01290          JSR ESCCHECK
01300 ------------------------------
01310 ; SIOT2=COM $54 => READ TRACK +         ANALYSIS FUNCTION.
01320 ; MIT:
01330 ; 30A=XSAV, 30B = TRACKNUM              CONSTAT= STATUS OF OPERATION
01340 ------------------------------
01350          LDA TRACKNUM ;XSAV= $30A IST NICHT NOETIG
01360          STA $30B     ;WEIL ES DURCH KOMMANDO $54 GESETZT WIRD
01370          LDA PSOURCE  ;SOURCE DRIVE
01380          STA $301
01390          JSR MAINSIO
01400          BPL .77     ;FEHLER BEI DER AUSFUEHRUNG?
01410          JSR OPENSCR
01420          JSR TEXTOUT
01430          .HX 9B9B9B9B
01440          .AS -' FATAL DRIVE ERROR, PLEASE REBOOT '
01450          .HX EA
01460          LDA #$FF
01470          STA $244
01480          .HX 02
01490 ------------------------------
01500 .77      LDA CONSTAT
01510          BEQ .78
01520          JSR TEXTOUT
01530          .HX 7D9B9B9B9B9B
01540          .DA " DRIVE DOOR NOT CLOSED, <RETURN>",#$9B,#$EA
01550          JSR RETURNG
01560          JMP BIGST
01570 ------------------------------
01580 .78      LDA #0      ;RAMDISK IST MIT DATEN GEFUELLT
01590          STA RDSKSTAT ;SO WIRD ES NICHT GEBRAUCHT
01600 ;
01610          LDX #SIO2TAB ;INIT SIO READ COMMAND
01620          LDY /SIO2TAB
01630          JSR SIOINIT0
01640          LDA PSOURCE  ;SOURCE DRIVE
01650          STA $301
01660          LDA #HEADERWA ;SETZE ARBEITS BUFFER AUF HEADER WORK AREA
01670          STA RDSKPAR0+2
01680          STA $304
01690          LDA /HEADERWA
01700          STA RDSKPAR0+3
01710          STA $305
01720 ------------------------------
01730          LDA #0
01740 .1       PHA
01750          JSR MAINSIO ;UEBERTRAGE DEN LAUFWERKS HEADER BUFFER
01760          LDA #$40    ;ZUM COMPUTER HEADER BUFFER WORK AREA
01770          STA $303    ;REINIT SIO READ STATUS
01780          JSR ADDBUF  ;INCREMENT BUFFER UND SECTOR MIT $80
01790          PLA
01800          TAX
01810          INX
01820          TXA
01830          CPX #3      ;3 PAGES EMPFANGEN?
01840          BCC .1      ;NEIN
01850 ------------------------------
01860 ; DER HEADERBUFFER DES LAUFWERKS        IST JETZT IM COMPUTER ZUR
01870 ; FREIEN AUSWERTUNG. ES SIND ALL        ERDINGS NOCH ALLE DATEN IN
01880 ; DIE RAMDISK ZU SICHERN.
01890 ------------------------------
01900          CLC         ;CARRY=0 - BILDSCHIRM NEU AUFBAUEN
01910          JSR SETPAR0
01920 ;
01930          JSR SPR     ;TEXT "READING"
01940 ------------------------------
01950 ; EINGELESENE HEADERINFO'S              WEITER IN RAMDISK UEBERTRAGEN
01960 ------------------------------
01970          LDA TRACKNUM
01980          ASL
01990          TAY
02000          LDA RSEC
02010          STA RDSKPAR0
02020          STA TRACKTAB,Y ;START SECTOR DER RAMDISK
02030          LDA RSEC+1  ;IN TABELLE EINTRAGEN
02040          STA RDSKPAR0+1
02050          STA TRACKTAB+1,Y
02060 ------------------------------
02070          LDA #3
02080 .2       PHA
02090          LDA #1      ;ACCU=1 - SCHREIBE DATEN IN RAMDISK
02100          CLC
02110          JSR RDSKVER ; RAMDISKVERWALTUNG.
02120          BMI RDERR
02130          JSR ADDBUFR ; INCREMENT PARAMETER
02140          PLA
02150          TAX
02160          DEX
02170          TXA
02180          BNE .2
02190 ------------------------------
02200          LDA FORKEN  ;FORMAT
02210          BEQ INCTRK  ;FORKEN = 0 BEDEUTET UNFORMATIERT
02220          LDA DLEN    ;DATENLAENGE
02230          ORA DLEN+1
02240          BEQ INCTRK
02250 ------------------------------
02260          LDA PSOURCE ;SOURCE DRIVE
02270          JSR LOADREC
02280          BCS RDERR
02290          JMP INCTRK
02300 RDERR    JSR CLRBASE
02310          LDA PSOURCE ;SOURCE DRIVE MOTOR STOPPEN
02320          JSR DEST
02330          LDA PDEST   ;DESTINATION DRIVE
02340          JSR BACKUP
02350          LDA #0
02360          STA RSEC
02370          STA RSEC+1
02380          INC TRACKNUM
02390          LDA TRACKNUM
02400          STA STRACK
02410          JSR SOURCE
02420          JMP L991
02430 INCTRK   INC TRACKNUM
02440          LDA TRACKNUM
02450          CMP #40
02460          BCS SHIT
02470          JMP L88
02480 ------------------------------
02490 SHIT     LDA #$FF    ;RAMDISK USED FLAG SETZEN
02500          STA RDSKSTAT
02510          JSR DEST
02520          LDA PDEST
02530          JSR BACKUP
02540 ------------------------------
02550 COPYEND  LDA PDEST
02560          LDX #MOTOFF
02570          LDY /MOTOFF
02580          SEC
02590          JSR DRVJMP
02600 ------------------------------
02610          LDX #20
02620 .1       LDA MCOPYTERM,X
02630          STA MESSAGE,X
02640          DEX
02650          BPL .1
02660          JSR RETURN
02670          JMP BIGST
02680 ------------------------------
02690 MCOPYTERM
02700      .AT '  COPY TERMINATED   '
02710 ------------------------------
02720 ; BUFFER ZURUECKSCHREIBEN !
02730 ------------------------------
02740 SRCDRV   .HX 00
02750 ------------------------------
02760 ; BACKUP FUNCTION:
02770 ; ---------------
02780 ; INCLUDES :
02790 ; DATA TRANSFER
02800 ; FORMATING / REFORMATING
02810 ; TRACK POSITIONING
02820 ; ERROR MESSAGES
02830 ------------------------------
02840 BACKUP   STA SRCDRV
02850          LDA TRACKNUM ;TRACK NUMMER
02860          STA LTRACK   ;IN VARIABLE SCHREIBEN
02870          LDA STRACK
02880          STA TRACKNUM
02890 .80      LDA TRACKNUM ;SETZE TRACK START SECTOR
02900          ASL          ;IM RAMDISK HANDLER
02910          TAY
02920          LDA TRACKTAB,Y
02930          STA RSEC
02940          LDA TRACKTAB+1,Y
02950          STA RSEC+1
02960 ------------------------------
02970 ; LESE 3 HEADER INFO SEKTOREN
02980 ; AUS DER RAMDISK IN DIE
02990 ; HEADER WORK AREA
03000 ------------------------------
03010          JSR SETSECR
03020          LDA #HEADERWA
03030          STA RDSKPAR0+2
03040          LDA /HEADERWA
03050          STA RDSKPAR0+3
03060          JSR ESCCHECK
03070          LDA #3
03080 .2       PHA
03090          LDA #0      ;ACCU=1 READ
03100          CLC
03110          JSR RDSKVER ;RAMDISKVERWALTUNG
03120 ------------------------------
03130 ;NOTE :
03140 ;NACH AUFRUF DER RDSVER FUNK-
03150 ;TION KANN EIN FEHLER AUFTRETEN
03160 ;DIESER FEHLER ENSTEHT DURCH
03170 ;DISK READ!
03180 ------------------------------
03190          JSR ADDBUFR ;INCREMENT PARAMETER
03200          PLA
03210          TAX
03220          DEX
03230          TXA
03240          BNE .2
03250          SEC         ;SETPAR0 OHNE BILDSCHIRM AUFBAU
03260          JSR SETPAR0
03270          JSR SPW     ;TEXT "WRITING"
03280 ------------------------------
03290          LDA FORKEN  ;TESTE FORMAT
03300          BNE .1      ;FORMATIERT!
03310 ------------------------------
03320 ;PROGRAMM NACHSCHREIBEN
03330 ------------------------------
03340          LDX #SIOT6  ;REFORMAT TRACK
03350          LDY /SIOT6
03360          JSR SIOINIT0
03370          LDA SRCDRV
03380          STA $301
03390          LDA TRACKNUM
03400          STA $30B
03410          JSR MAINSIO
03420          JMP .4
03430 ------------------------------
03440 ;TRACKNUMBER AT $30B
03450 ------------------------------
03460 .1       LDX #SIOT   ;SIO WRITE COMMAND
03470          LDY /SIOT
03480          JSR SIOINIT0
03490          LDA SRCDRV
03500          STA $301
03510          LDA #HEADERWA ;SETZE WORK AREA
03520          STA $304
03530          STA RDSKPAR0+2
03540          LDA /HEADERWA
03550          STA $305
03560          STA RDSKPAR0+3
03570          LDA #HEADBUF
03580          STA $30A
03590          LDA /HEADBUF
03600          STA $30B
03610          LDA #3
03620 .20      PHA
03630          JSR MAINSIO
03640          LDA #$80    ;REINIT
03650          STA $303    ;WRITE
03660          JSR ADDBUF  ;CALC. BUF
03670          PLA
03680          TAX
03690          DEX
03700          TXA         ;3 SECTOREN
03710          BNE .20     ;UEBERTRAGEN?
03720 ------------------------------
03730 ; HEADER INFO KOPIERT
03740 ; TEST, OB DATEN IM BUFF=0
03750 ------------------------------
03760          LDA DLEN    ;MIT Z=0
03770          ORA DLEN+1  ;=>DLEN=0
03780          BEQ .4
03790          LDA SRCDRV
03800          JSR SAVREC
03810 .55      LDX #SIOT5  ;SCHREIBE TRACK FUNKTION
03820          LDY /SIOT5
03830          JSR SIOINIT0
03840          LDA SRCDRV  ;SELECT DRIVE
03850          STA $301
03860          LDA FORKEN
03870          STA $30A
03880          LDA TRACKNUM
03890          STA $30B
03900          JSR MAINSIO  ;FROM BUF
03910          JSR ERRSYS
03920          BCC .5
03930          LDA #0
03940          STA CONSTAT
03950 ------------------------------
03960 .5       LDA CONSTAT
03970          BNE .55
03980 .4       INC TRACKNUM
03990          LDA TRACKNUM
04000          CMP LTRACK  ; STRACK IST UM EIN BYTE ZU GROSS !
04010          BCC .92     ; DARUM SPRINGE ICH AUF BCC !
04020          DEC TRACKNUM
04030          RTS
04040 .92      JMP .80
04050 ------------------------------
04060 MFORM1   .AT ' FATAL WRITE ERROR  '
04070 MFORM2   .AT 'ILLEGAL FORMAT ERROR'
04080 MFORM3   .AT 'ERROR DURING WRITING'
04090 MFORM4   .AT '   VERIFY  ERROR    '
04100 ;
04110 WTAB     .DA MFORM1,MFORM2,MFORM3,MFORM4
04120 ------------------------------
04130 ERRSYS   LDX CONSTAT
04140          CLC
04150          BEQ .2
04160          DEX
04170          TXA
04180          ASL
04190          TAX
04200          LDA WTAB,X
04210          STA DISPLAY
04220          LDA WTAB+1,X
04230          STA DISPLAY+1
04240          LDY #20
04250 .1       LDA (DISPLAY),Y
04260          STA MESSAGE,Y
04270          DEY
04280          BPL .1
04290          JSR RETURNG
04300          LDA CONSTAT
04310          CMP #1
04320          CLC
04330          BEQ .2
04340          SEC
04350 .2       RTS
04360 ------------------------------
04370 ESCCHECK LDA $2FC
04380          CMP #$1C
04390          BEQ .1
04400          CMP #$FF
04410          RTS
04420 .1       LDA #$FF
04430          STA $2FC
04440          LDX #$FF
04450          TXS
04460          JMP BIGST
04470 ------------------------------
04480 MREAD
04490      .AT '      READING       '
04500 MWRITE
04510      .AT '      WRITING       '
04520 ------------------------------
04530 SPR      LDX #20
04540 .1       LDA MREAD,X
04550          STA MESSAGE,X
04560          DEX
04570          BPL .1
04580          RTS
04590 ------------------------------
04600 SPW      LDX #20
04610 .1       LDA MWRITE,X
04620          STA MESSAGE,X
04630          DEX
04640          BPL .1
04650          RTS
04660 ------------------------------
04670 SOURCE   LDA PDEST
04680          LDX #MOTOFF
04690          LDY /MOTOFF
04700          SEC         ;QUIT
04710          JSR DRVJMP
04720          LDA TANDEM
04730          BNE .3
04740          RTS
04750 .3       LDX #20
04760 .1       LDA MSOURCE,X
04770          STA MESSAGE,X
04780          DEX
04790          BPL .1
04800          LDA PCHANGE
04810          BPL .2
04820          JMP RETURNG
04830 .2       LDA PDEST
04840          LDX #DISKWAIT
04850          LDY /DISKWAIT
04860          SEC
04870          JSR DRVJMP
04880          JMP AUTOM
04890 ------------------------------
04900 STAT     LDA #0
04910          STA $D20A
04920          LDA $D20F
04930          AND #$10
04940          RTS
04950 ------------------------------
04960 AUTOM    JSR STAT
04970          BNE .1
04980 ------------------------------
04990          LDA $2FC
05000          CMP #$1C    ; ESCAPE
05010          BNE AUTOM
05020          LDA #$FF
05030          STA $2FC
05040          LDA #$34
05050          STA $D303
05060 .2       JSR STAT
05070          BEQ .2
05080          LDA #$3C
05090          STA $D303
05100          JMP BIGST
05110 .1       LDA #0
05120          LDX #20
05130 .3       STA MESSAGE,X
05140          DEX
05150          BPL .3
05160          LDX #0
05170 .4       STA $D40A
05180          DEX
05190          BNE .4
05200          RTS
05210 ------------------------------
05220 DEST     LDA PSOURCE
05230          LDX #MOTOFF
05240          LDY /MOTOFF
05250          SEC         ;QUIT
05260          JSR DRVJMP
05270          LDA TANDEM
05280          BNE .3
05290          RTS
05300 .3       LDX #20
05310 .1       LDA MDEST,X
05320          STA MESSAGE,X
05330          DEX
05340          BPL .1
05350          LDA PCHANGE
05360          BMI RETURNG
05370          LDA PDEST
05380          LDX #DISKWAIT
05390          LDY /DISKWAIT
05400          SEC
05410          JSR DRVJMP
05420          JMP AUTOM
05430 ------------------------------
05440 RETURNG  LDA #$FF
05450          STA $2FC
05460 .2       JSR ESCCHECK
05470          BCS .2
05480          JSR GETKEY
05490          CMP #$9B
05500          BNE .2
05510          LDX #20
05520 .3       LDA #0
05530          STA MESSAGE,X
05540          DEX
05550          BPL .3
05560          LDA #$9B
05570          RTS
05580 RETURN   JSR RETURNG
05590          JMP EOUT
05600 ------------------------------
05610 SORTDRV  LDY #1
05620          LDA #0
05630 .1       ORA DRIVES-1,Y
05640          INY
05650          CPY #MAXDRV+1
05660          BCC .1
05670          CMP #0
05680          BNE .2
05690          SEC
05700          RTS
05710 .2       LDX #0
05720          LDY #1
05730 .4       LDA DRIVES-1,Y
05740          BEQ .3
05750          TYA
05760          STA DRIVES,X
05770          INX
05780 .3       INY
05790          CPY #MAXDRV+1
05800          BCC .4
05810          STX FDRV
05820          CLC
05830          RTS
05840 ------------------------------
05850 SIOT7    .HX 0A31014F80
05860          .DA CONFIG
05870          .HX FFFF0C00
05880 CONFIG   .HX 28010012000000
05890          .HX 80FF000000
05900 ------------------------------
05910 SELDRV   CMP FDRV
05920          BCC .1
05930          BEQ .1
05940          SEC
05950          RTS
05960 .1       TAY
05970          LDA DRIVES-1,Y
05980          STA $301
05990          CLC
06000          RTS
06010 ------------------------------
06020 GETKEY   LDA $E425
06030          PHA
06040          LDA $E424
06050          PHA
06060          RTS
06070 ------------------------------
06080 ; SAV2 + $80 = BUFFER !
06090 ------------------------------
06100 ADDSEC   INC RSEC
06110          BNE .1
06120          INC RSEC+1
06130 .1       RTS
06140 ------------------------------
06150 CALCS    LDA DLEN    ;ERRECHNE
06160          STA M1      ;DIE AN-
06170          LDA DLEN+1  ;ZAHL DER
06180          STA M2      ;SEKTOREN
06190 ------------------------------
06200 ;(M1,M2)=(DLEN+0,+1) *(1/128)
06210 ;BEMERKUNG:M2 IST SIGNIFICANT!
06220 ------------------------------
06230          ASL M1
06240          ROL M2
06250          RTS
06260 ------------------------------
06270 SETSECBUF LDA #SECBUF
06280          STA $30A
06290          LDA /SECBUF
06300          STA $30B
06310          RTS
06320 ------------------------------
06330 ; DER HEADER BUFFER IST JETZT IN        DIE RAMDISK KOPIERT WORDEN
06340 ; DER HEADER STEHT JETZT ALSO           ZUR WEITEREN VERFUEGUNG OFFEN
06350 ; -HIER WIRD ES JETZT ALS SECTOR         BUFFER GENUTZT.
06360 ------------------------------
06370 LOADREC  PHA
06380          LDX #SIO2TAB ; INIT SIO READ COMMAND.
06390          LDY /SIO2TAB
06400          JSR SIOINIT0
06410          PLA
06420          STA $301
06430 ------------------------------
06440          JSR SETSECBUF ;SETZE COMPUTER POINTER AUF LAUFWERKS BUFFER
06450 ------------------------------
06460          JSR SETSECR   ;IN RAMDISK PARAMETERLISTE UEBERTRAGEN !
06470 ------------------------------
06480          JSR CALCS   ;ERECHNE DATENLAENGE AUS DER ANZAHL DER SEKTOREN
06490 ------------------------------
06500          LDA $D301   ;WERT $D301 SICHERN
06510          PHA
06520 .3       LDA #1      ;SCHREIBE RAMDISK
06530          SEC         ;GET BANK & BUFFER DATA ONLY
06540          JSR RDSKVER
06550          BMI LRERR
06560          STX $304
06570          STY $305
06580          JSR MAINSIO
06590 ------------------------------
06600          LDA #$40    ;READ
06610          STA $303    ;STATUS
06620          JSR INCBUF  ;CALC $30A,$30B
06630          JSR ADDSEC
06640          JSR SETSECR
06650 ------------------------------
06660          DEC M2
06670          BNE .3
06680          PLA
06690          STA $D301
06700          CLC
06710          RTS
06720 ------------------------------
06730 LRERR    PLA
06740          STA $D301
06750          SEC
06760          RTS
06770 ------------------------------
06780 SAVREC   PHA
06790          LDX #SIOT
06800          LDY /SIOT
06810          JSR SIOINIT0
06820          PLA
06830          STA $301
06840          JSR SETSECBUF
06850          JSR SETSECR
06860          JSR CALCS
06870 ------------------------------
06880          LDA $D301
06890          PHA
06900 .30      LDA #0      ;LESE RAMDISK
06910          SEC
06920          JSR RDSKVER
06930          STX $304
06940          STY $305
06950 ------------------------------
06960          JSR MAINSIO
06970          LDA #$80    ;RESTORE SIO
06980          STA $303    ;SCHREIBE STATUS
06990          JSR INCBUF
07000          JSR ADDSEC
07010          JSR SETSECR ;UEBERTRAGE VON RSEC IN DIE PARAMETER LISTE
07020 ------------------------------
07030          DEC M2
07040          BNE .30
07050          PLA
07060          STA $D301
07070          CLC
07080          RTS
07090 ------------------------------
07100 ;BEMERKUNG:
07110 ;DIE SETPAR0 ROUTINE LEGT JETZT        AUCH DIE STATI-WERTE AUF DAS
07120 ;DAS DISPLAY.
07130 ------------------------------
07140 PAR      .HX 00
07150 YS0      .HX 00
07160 YS1      .HX 00
07170 SET      LDA #HEADERWA
07180          STA DISPLAY
07190          LDA /HEADERWA
07200          STA DISPLAY+1
07210          RTS
07220 ------------------------------
07230 PSET     ORA PAR
07240          STA PAR
07250          RTS
07260 ------------------------------
07270 OTAB     .HX 00000000
07280 ------------------------------
07290 ; AN DIESER STELLE MUESSEN DIE          LAUFWERKSPARAMETER IN DEN
07300 ; HEADERBUFFER EINGEBLENDET             WERDEN.
07310 ;
07320 ; HEADBUF+ $17B IST DANN DIE BEL        EGUNG DER EINZELNEN BIT'S :
07330 ; 
07340 ; VERIFY         =>  BIT 7
07350 ; TRACKANALYZING =>  BIT 6
07360 ; RETRIES        =>  BIT 0,1,2.
07370 ------------------------------
07380 SETPAR0  PHP
07390          LDA PRETRY
07400          AND #7
07410          STA PAR
07420          LDA PVERIFY
07430          AND #$80
07440          JSR PSET
07450          LDA PTRKAN
07460          LSR
07470          AND #$40
07480          JSR PSET
07490          LDA PAR
07500          EOR #$F8
07510          STA PAR
07520          JSR SET
07530          LDY #$FF    ;TESTE
07540          LDA (DISPLAY),Y ;FORMAT
07550          STA FORKEN
07560          BNE .1
07570 ------------------------------
07580          PLP
07590          BCS .2
07600          LDA #1      ;BEI UNFORMATIERTEM TRACK
07610 .0       PHA         ;WIRD DAS '!' AUF DEM BILDSCHIRM AUSGEGEBEN
07620          TAX
07630          LDA #1
07640          LDY TRACKNUM
07650          JSR PUTBASE
07660          PLA
07670          TAX
07680          INX
07690          TXA
07700          CMP #19     ;DIESER ZAEHLER LAEUFT BIS
07710          BCC .0      ;SEKTOR 18 ERREICHT IST
07720 ------------------------------
07730          JMP NS
07740 .1       PLP         ;WRITE COMMAND?
07750 .2       BCS NW
07760          LDA #0
07770          STA YS0
07780          STA YS1
07790 L3S      JSR SET
07800          LDY YS0
07810          LDA (DISPLAY),Y ; ID STATUS
07820          PHA
07830          INY
07840          LDA (DISPLAY),Y
07850          PHA         ;TRACK
07860          INY
07870          INY
07880          LDA (DISPLAY),Y ;SECTOR
07890          PHA
07900          INC DISPLAY+1 ;GET SECTOR
07910          LDY YS1     ;STATUS
07920          LDA (DISPLAY),Y
07930          PHA
07940          LDX #3
07950 .4       PLA
07960          STA OTAB,X
07970          DEX
07980          BPL .4
07990 ------------------------------
08000 ; ALLE WICHTIGEN DATEN FUER             EINEN SEKTOR SIND JETZT
08010 ; IM LABEL OTAB VORHANDEN.
08020 ; Y=TRACK , X=SECTOR , A=STATUS
08030 ------------------------------
08040          LDA OTAB
08050          ORA OTAB+3
08060          BNE OK
08070          LDA #$A
08080          LDX OTAB+2
08090          LDY OTAB+1
08100          JSR PUTBASE
08110          JMP OK1
08120 OK       LSR
08130          LSR
08140          CLC
08150          ADC #$10
08160          LDX OTAB+2
08170          LDY OTAB+1
08180          JSR PUTBASE
08190 OK1      INC YS1
08200          LDA YS0
08210          CLC
08220          ADC #7
08230          STA YS0
08240          CMP FORKEN
08250          BCC L3S
08260 NS       JSR SET
08270          INC DISPLAY+1
08280          LDY #$7E    ;GET DATEN
08290          LDA (DISPLAY),Y ;LAENGE
08300          STA DLEN
08310          INY
08320          LDA (DISPLAY),Y
08330          STA DLEN+1
08340          RTS
08350 ------------------------------
08360 NW       LDY TRACKNUM
08370          LDX #19
08380          LDA #$80
08390          JSR PUTBASE
08400          JMP NS
08410 ------------------------------
08420 TEXTOUT  PLA
08430          STA $0
08440          PLA
08450          STA $1
08460 .2       LDY #1
08470          LDA ($0),Y
08480          INC $0
08490          BNE .3
08500          INC $1
08510 .3       CMP #$EA
08520          BEQ .4
08530          JSR EOUT
08540          JMP .2
08550 .4       JMP ($0)
08560 ------------------------------
08570 COMT0    .DA #$54,SDRV0
08580 COMT1    .DA #$55,SDRV1
08590 COMT2    .DA #$56,REFORM
08600 ------------------------------
08610 SIOT     .HX 0C31015080  COM50
08620          .DA BEGIN
08630          .HX FFFF80000080
08640 ------------------------------
08650 SIOT1    .HX 0A31014C01  COM4C
08660          .DA $8000
08670          .HX FFFF0000
08680 ------------------------------
08690 SIOT2    .HX 0A31015440  COM54
08700          .DA CONSTAT
08710          .HX FFFF0100
08720 ------------------------------
08730 SIOT3    .HX 0A31014180  COM41
08740          .DA $3000
08750          .HX FFFF0300
08760 ------------------------------
08770 SIOT5    .HX 0A31015540  COM55
08780          .DA CONSTAT
08790          .HX FFFF0100
08800 ------------------------------
08810 SIOT6    .HX 0A31015600  COM56
08820          .DA $3000
08830          .HX FFFF0000
08840 ------------------------------
08850 SIO2TAB  .HX 0C31015240  COM52
08860          .DA CBUF
08870          .HX FFFF8000
08880          .DA HEADBUF
08890 ------------------------------
08900 CONSTAT  .HX 00
08910 ------------------------------
08920 SIOINIT0 STX SAV1
08930          STY SAV1+1
08940          LDY #0
08950          LDA (SAV1),Y
08960          TAY
08970 .1       LDA (SAV1),Y
08980          STA $300-1,Y
08990          DEY
09000          BNE .1
09010          RTS
09020 ------------------------------
09030 DRVJMP   PHA         ;SAV DRIVE No
09040          PHP
09050          STX $30A    ;SETZE SPRUNG
09060          STY $30B    ;ADRESSE
09070          LDX #SIOT1
09080          LDY /SIOT1
09090          JSR SIOINIT0 ;INIT SIO
09100          PLP
09110          BCC .1
09120          LDA #$4D
09130          STA $302
09140 .1       PLA         ;GET DRIVE
09150          STA $301    ;SET No.
09160 ------------------------------
09170 MAINSIO  LDA #$40
09180          STA $10
09190          STA $D20E
09200          JMP $400
09210 ------------------------------
09220 ; COMMAND INITILIZE ROUTINE
09230 ------------------------------
09240 COMINIT  PHA         ;RETTE A
09250          TXA         ; X
09260          PHA         ; UND
09270          TYA         ; Y
09280          PHA         ;AUF STACK
09290          LDX #SIOT3  ;INIT SIO
09300          LDY /SIOT3  ;MIT
09310          JSR SIOINIT0 ;CMD $41
09320 ------------------------------
09330          PLA
09340          STA $305
09350          PLA
09360          STA $304
09370          PLA
09380          STA $301   ;DRV NO
09390          JSR MAINSIO
09400          LDA $301
09410          RTS
09420 ------------------------------
09430 ; BILDSCHIRM AUSGABE
09440 ------------------------------
09450 EOUT     TAY
09460          LDA $E407
09470          PHA
09480          LDA $E406
09490          PHA
09500          TYA
09510          RTS
09520 ------------------------------
09530 ; HEXOUT GIBT ZWEI HEXADEZIMAL
09540 ; ZAHLEN AUS. DAS BYTE MUSS IM
09550 ; ACCU STEHEN
09560 ------------------------------
09570 PHEXOUT  PHA         ;RETTE BYTE
09580          LSR         ;MULTIPLIZIERE
09590          LSR         ;DEN
09600          LSR         ;WERT
09610          LSR         ;4 MAL
09620          JSR HEXOUT0
09630          PLA
09640          AND #$F
09650 HEXOUT0  CMP #10     ;0-9?
09660          BCC .1      ;JA
09670          ADC #6      ;MUSS A-F
09680 .1       CLC
09690          ADC #$30    ;LESE ASCII
09700          JMP EOUT    ;AUSGABE
09710 ------------------------------
09720 ; INITIAL FLAG TELLS NOT TO
09730 ; PROGRAMM THE DRIVE ANY MORE
09740 ------------------------------
09750 ADDBUF   LDA $304
09760          EOR #$80
09770          STA $304
09780          BMI INCBUF
09790          INC $305
09800 INCBUF   LDA $30A
09810          EOR #$80
09820          STA $30A
09830          BMI .2
09840          INC $30B
09850 .2       RTS
09860 ------------------------------
09870 OPENSCR  JSR OPENE
09880          LDA #1
09890          STA $2F0
09900          JSR TEXTOUT
09910          .HX 7DEA
09920          RTS
09930 ------------------------------
09940 OPENE    LDA $E401
09950          PHA
09960          LDA $E400
09970          PHA
09980          RTS
09990 ------------------------------
10000 ; ADDBUFFER ROUTINE :
10010 ------------------------------
10020 ADDBUFR  LDA RDSKPAR0+2
10030          CLC
10040          ADC #$80
10050          STA RDSKPAR0+2
10060          BCC .1
10070          INC RDSKPAR0+3
10080 ------------------------------
10090 .1       INC RSEC
10100          BNE SETSECR
10110          INC RSEC+1
10120 ------------------------------
10130 SETSECR  LDA RSEC
10140          STA RDSKPAR0
10150          LDA RSEC+1
10160          STA RDSKPAR0+1
10170          RTS
10180 ------------------------------
10190 TRACKTAB .BL 80,0
10200 RSEC     .HX 0000
10210 ------------------------------
10220 HEADERWA .BL $180,0  ; HEADER WORK AREA
10230 ------------------------------
10240 ; $180 BYTES FREIER ARBEITSSPEICHER FUER DEN TRACK
10250 ------------------------------
10260 DRIVES   .HX 00000000

```
  
### INIT.ASM  
  
```
00010 ------------------------------
00020          .LION
00030 ;"†…Œ…‘†"
00040          .LIOFF
00050 ------------------------------
00060 ; STAND :  25/11/86
00070 ------------------------------
00080 DRVIX    RTS
00090 DRVINIT  LDA #1      ;DRIVE 1
00100          STA DRVSEL
00110 .2       LDA DRVSEL
00120          JSR SELDRV  ;CONVERT TO PHYSICAL DRIVE NUMBER
00130          BCS DRVIX   ;ERROR ?
00140          PHA         ;SAVE NO.
00150          LDX #0      ;KALTSTART
00160          LDY #$FF    ;AUF SELEKTIERTEM LAUFWERK
00170          SEC         ;X,Y CONTAINS JUMP ADR
00180          JSR DRVJMP  ;C=1 MEANS IMMIDEATE QUIT
00190 ------------------------------
00200          LDY #$57    ;JUST WAIT THAT DRIVE
00210          LDX #0      ;COMES UP
00220 .41      STA $D40A
00230          DEX
00240          BNE .41
00250          DEY
00260          BNE .41
00270          LDX #SIOT7  ;INITIALIZE SIO FOR COMMAND $4F.
00280          LDY /SIOT7  ;DRIVE CONFIGURATION TAB CONTAINS THE FOLLOWING
00290          JSR SIOINIT0 ;PARAMETER:
00300          PLA         ;SINGLE DENSITY / 40 TRACK
00310          PHA         ;18 SECTORS     / 128 BYTES PER SECTOR
00320          STA $301
00330          JSR MAINSIO ;EXECUTE COMMAND
00340 ------------------------------
00350 ;"‘“¡Œ”∆≈“≈†‘»≈†√œ–Ÿ†Õ¡√»…Œ≈†“œ’        ‘…Œ≈†‘œ†ƒ“…÷≈Æ"
00360 ------------------------------
00370          LDX #SIOT
00380          LDY /SIOT
00390          JSR SIOINIT0
00400          PLA
00410          PHA
00420          STA $301
00430          LDA #0
00440 .40      PHA
00450 .45      LDA #$80
00460          STA $303
00470          JSR MAINSIO
00480          BMI .45
00490          JSR ADDBUF
00500          PLA
00510          TAX
00520          INX
00530          TXA
00540          CMP #17  ; TEST IF 5 PAGES ARE SEND.
00550          BCC .40
00560 ------------------------------
00570 ; NOW WRITE THE COMMANDS INTO DRIVE'S COMMAND TABLE:
00580 ;
00590 ; COM. $54 DRIVE ANALYSIS READ
00600 ; COM. $55 DRIVE ANALYSIS WRITE
00610 ; COM. $56 REFORMAT TRACK
00620 ------------------------------
00630          PLA
00640          PHA
00650          LDX #COMT0
00660          LDY /COMT0  ; INIT :
00670          JSR COMINIT  ; SDRV0
00680          LDX #COMT1
00690          LDY /COMT1
00700          JSR COMINIT  ; SDRV1
00710          LDX #COMT2
00720          LDY /COMT2
00730          JSR COMINIT  ; REFORM
00740          PLA
00750          PHA
00760          LDX #ACTIVATE
00770          LDY /ACTIVATE
00780          SEC
00790          JSR DRVJMP
00800 ------------------------------
00810          JSR TEXTOUT
00820          .AS "DRIVE $"
00830          .HX EA
00840          PLA
00850          JSR PHEXOUT
00860          JSR TEXTOUT
00870          .DA " INITIALIZED",#$9B,#$9B,#$EA
00880          INC DRVSEL
00890          JMP .2
00900 ------------------------------
00910 LOCSPEEDY LDA #1
00920          STA DRVSEL  ;DRV = 1
00930          JSR TEXTOUT
00940          .HX 9B9BEA
00950 ------------------------------
00960 ;"Ãœ√¡‘≈†”–≈≈ƒŸ†ƒ“…÷≈"
00970 ------------------------------
00980          LDA BASE
00990          STA LMS
01000          LDA BASE+1
01010          STA LMS+1
01020 .1       LDX #SIOT1  ; INIT
01030          LDY /SIOT1  ; JMP COM.
01040          JSR SIOINIT0  ; TO SIO
01050          LDA #SENDC
01060          STA $30A
01070          LDA /SENDC
01080          STA $30B
01090          LDA #0      ; MIN.
01100          STA $306   ; TIMEOUT
01110          LDA DRVSEL
01120          STA $301
01130          JSR MAINSIO
01140          BPL .2
01160          LDA #0
01170          LDY DRVSEL
01180          STA DRIVES-1,Y
01190          BPL .3      =JMP
01200 ------------------------------
01210 .2       JSR TEXTOUT
01220          .AS "DRIVE $"
01230          .HX EA
01240          LDA DRVSEL
01250          JSR PHEXOUT
01260          JSR TEXTOUT
01270          .DA " IS SPEEDY ",#$9B,#$EA
01280          LDA #$10
01290          LDY DRVSEL
01300          STA DRIVES-1,Y
01310 ------------------------------
01320 .3       INC DRVSEL
01330          LDA DRVSEL
01340          CMP #MAXDRV+1  DRV=4
01350          BCC .1
01360 ------------------------------
01370          JSR SORTDRV
01380          BCC .5
01390          JSR TEXTOUT
01400          .DA "SORRY , NO SPEEDY LOCATED,",#$9B
01410          .DA "... CANNOUT CONTINUE",#$EA
01420 .99      JMP .99
01430 ------------------------------
01440 .5       JSR TEXTOUT
01450          .HX 9BEA
01460          RTS

```
  
### DRIVE.ASM  
  
```
00010 ------------------------------
00020          .LI ON
00030 ;"†ƒ“…÷≈†"
00040          .LI OFF
00050 ------------------------------
00060 ------------------------------
00070 ;FOLGENDE LAUFWERKSFUNKTIONEN
00080 ;SIND ENTHALTEN:
00090 ;1.EINLESEN DER SECTOR ID'S
00100 ;  EINES TRACK'S
00110 ;2.EINLESEN DER DATENFELDER
00120 ;3.TABELLIERUNG DER STATI
00130 ;4.FORMATIERUNG MITTELS
00140 ;  INTERLEAVING
00150 ;5.SCHREIBEN DER DATENFELDER
00160 ;  UND IHRER STATI
00170 ;
00180 ; STAND:  26/11/86'
00190 ------------------------------
00200          .OR $8000
00210 SDRV0    JSR SEM0
00220          LDA XSAV
00230          STZ STBUF   ; CLEAR DRIVE STATUS
00240          JSR TSTWRP
00250          AND #$80    ; KLAPPE OFFEN ?
00260          BNE .1      ; FEHLER !
00270          LDX #2      ; ANZAHL RETRYS
00280 .13      PHX
00290 ------------------------------
00300          JSR READH
00310          JSR CONRES
00320          JSR MOVE
00330 ------------------------------
00340 ;TEST AUF 18 HEADER
00350 ------------------------------
00360          PLX
00370          DEX
00380          BEQ .12
00390          LDA XSAV
00400          CMP #$7F    =18*7+1
00410          BNE .13
00420 ------------------------------
00430 .12      JSR RDSEC
00440 ------------------------------
00450          JMP SEM1
00460 ------------------------------
00470 ;STBUF=STATUS,DER ZUM COMPUTER         GEHT.
00480 ------------------------------
00490 .1       LDA #1
00500          STA STBUF
00510          JMP SEM1
00520 ------------------------------
00530 ;CRC ERROR IM DATENFELD ENTD.
00540 ------------------------------
00550 .2       JSR SPECVERI
00560          LDA #$80
00570          STA HEADBUF+$17D
00580          JMP SEM1
00590 ------------------------------
00600 STBUF    .HX 00
00610 ------------------------------
00620 ; MODUL SCHREIBEN :
00630 ------------------------------
00640 SDRV1    JSR SEM0
00650          STZ STBUF   ; CLEAR DRIVE STATUS
00660          LDA #20     ; GAPLAENGE ZWISCHEN DATEN UND
00670          STA FGAP    ; ID FIELD (SECTOR/SECTOR)
00680 ------------------------------
00690          JSR MOTON
00700          JSR TSTWRP  ; TEST OB KLAPPE OFFEN ODER WRITE PROTECT
00710          BNE .1      ; FEHLER !
00720 ------------------------------
00730 ; ICH GEHE DAVON AUS,DAS ES             MOEGLICH IST ,
00740 ; 19 SEKTOREN (MIT DATEN) IN            EINEM TRACK ZU FORMATIEREN.
00750 ; DAZU WERDEN DIE GAPS AUF EIN          MINIMUM GEKUERZT.
00760 ; ES BLEIBT ZU TESTEN:
00770 ; 
00780 ; >KOENNEN DANN IN EINER UMDREHU         NG ALLE ERFORDERLICHEN
00790 ;  DATEN ZURUECK-GESCHRIEBEN             WERDEN ?
00800 ; >WIRD BEI JEDEM LAUFWERK RICHT         IG FORMATIERT
00810 ------------------------------
00820          LDA HEADBUF+$17F ;  HILEN
00830          CMP #9
00840          BCC .3
00850          BEQ .2
00860          BCS .4      ; AETZER FORMAT !
00870 .2       LDA HEADBUF+$17E ;  LOLEN
00880          BEQ .3
00890 ------------------------------
00900 ;BEQ ID.NORMALFORMAT $900 BYTES
00910 ------------------------------
00920          LDA #10     ;ENGERES FORMAT !
00930          STA FGAP
00940 .3       LDA HEADBUF+$17B ;  FORMAT RETRIES
00950          AND #7
00960 .31      PHA
00970          JSR WTRACK  ; FORMAT TRACK FUNCTION
00980          PLA
00990          BCC .32     ; ERROR DURING FORMAT ?
01000          DEA
01010          BNE .31     ; NO MORE RETRIES !
01020          BEQ .4      ; FORMAT ERROR
01030 .32      LDA HEADBUF+$17B ; WRITE RETRIES
01040          AND #7
01050 .33      PHA
01060          JSR WRSEC
01070          PLA
01080          BCC .34
01090          DEA
01100          BNE .33
01110          BEQ .44     ; WRITE ERROR (TIMEOUT)
01120          LDA HEADBUF+$17B ; VERIFY ON?
01130          BPL .34
01140          JSR VERIFY
01150          BCS .45
01160 .34      JMP SEM1
01170 ------------------------------
01180 .45      LDA #4  ;VERIFY ERRROR
01190          .HX 2C      =BIT ABS.
01200 .44      LDA #3   ; WRITE ERROR
01210          .HX 2C      =BIT ABS.
01220 .4       LDA #2   ; ILLEGAL FORMAT ERROR
01230          .HX 2C      =BIT ABS.
01240 .1       LDA #1   ; FATAL ERROR
01250          STA STBUF
01260          ORA #$F0
01270          JSR HEXOUT
01280          JMP SEM1    ; SEND ERROR ?!
01290 ------------------------------
01300 FGAP     .HX 14
01310 ------------------------------
01320 ;HIER BEGINNEN DIE DIENST              ROUTINEN
01330 ------------------------------
01340 RDSEC    LDY #0    ;SET PAR
01350          STY CSEC  ;TO ZERO
01360          STY YSAV
01370          LDA #SECBUF ;SET BUFFER
01380          STA $19     ;POINTER
01390          LDA /SECBUF
01400          STA $1A
01410          LDA XSAV
01420          BNE .2
01430          RTS
01440 ------------------------------
01450 .2       LDY YSAV
01460          LDA HEADBUF+3,Y ;SET
01470 ------------------------------
01480          JSR RDSEC1
01490 ------------------------------
01500          LDY CSEC
01510          STA HEADBUF+$100,Y
01520          INC CSEC
01530          AND #$10
01540          BNE .1
01550 ------------------------------
01560          LDA $19    ;INC BUFFER
01570          EOR #$80
01580          STA $19
01590          BMI .1
01600          INC $1A
01610 .1       LDA YSAV
01620          CLC
01630          ADC #7
01640          STA YSAV
01650          CMP XSAV
01660          BCC .2
01670          LDA $19
01680          STA HEADBUF+$17E
01690          LDA $1A
01700          SEC
01710          SBC /SECBUF
01720          STA HEADBUF+$17F
01730          LDA CSEC
01740          STA TSEC
01750          RTS
01760 ------------------------------
01770 ;DIE FUNKTION SORTIERT DEN
01780 ;HEADERBUFFER UM, DAMIT EINE
01790 ;ERHOEHTE GESCHWINDIGKEIT
01800 ;BEIM SEKTORLESEN ERZIEHLT WIRD
01810 ------------------------------
01820 VAL2     .HX 00
01830 ------------------------------
01840 MOVE     LDY HEADBUF+$FF ; ZUNAECHST
01850          CPY #21  ;TESTE , OB DREI HEADER (3*7) VORHANDEN
01860          BCC MVERR
01870          LDX #0
01880 ------------------------------
01890 .1       LDA HEADBUF,X ; MOVED 14 BYTES AUF DEN STACK !
01900          PHA
01910          INX
01920          CPX #14
01930          BCC .1      ; JETZT LIEGT HEADBUF+13 AUF DEM STACK OBEN
01940          TYA
01950          SEC
01960          SBC #14
01970          STA VAL2
01980 ------------------------------
01990          LDY #0
02000 .2       LDA HEADBUF+14,Y
02010          STA HEADBUF,Y
02020          INY
02030          CPY VAL2
02040          BCC .2
02050 ------------------------------
02060          LDY HEADBUF+$FF
02070          LDX #13
02080 .3       PLA
02090          STA HEADBUF-1,Y
02100          DEY
02110          DEX
02120          BPL .3
02130 MVERR    RTS
02140 ------------------------------
02150 WRBTSL   BVC FORTO
02160 WRBYTS   BIT $280
02170          BPL WRBTSL
02180          STA $403
02190          DEY
02200          BNE WRBYTS
02210          RTS
02220 FORTO    PLA
02230          PLA
02240          SEC
02250          RTS
02260 ------------------------------
02270 WRBTL    BVC FORTO
02280 WRBYTE   BIT $280
02290          BPL WRBTL
02300          STA $403
02310          RTS
02320 ------------------------------
02330 WTRST    LDA #5
02340          STA $29F
02350          LDA #$F8    ;WRITE
02360          STA $400    ;TRACK
02370          LDA #0
02380          LDX #2
02390 .1       BIT $280
02400          BPL .1
02410          STA $403
02420          DEX
02430          BNE .1
02440          LDY #$D0
02450          STY $29F
02460          CLC
02470          RTS
02480 ------------------------------
02490 ; FORMATIERFUNKTION 1.
02500 ------------------------------
02510 WTRACK   STZ CSEC
02520          STZ YSAV
02530 ------------------------------
02540          JSR WTRST
02550 ------------------------------
02560          LDY #80     ; ACCU=0
02570          JSR WRBYTS  ;WRITE 40x
02580          LDA #$FC  ; INDEX MARK
02590          JSR WRBYTE
02600 .1       LDA #$FF
02610          LDY FGAP    ;NORMAL:20
02620          JSR WRBYTS  ; ACCU=00
02630          LDA #0
02640          LDY #5
02650          JSR WRBYTS
02660 ------------------------------
02670          LDA #$FE    ;SECTOR ID
02680          JSR WRBYTE
02690          LDA $D      ; = TRACK
02700          JSR WRBYTE
02710          LDY YSAV
02720          LDA HEADBUF+2,Y ;=SIDE
02730          JSR WRBYTE
02740          LDA HEADBUF+3,Y ; SECTOR
02750          JSR WRBYTE
02760          LDA HEADBUF+4,Y ; SECLEN
02770          JSR WRBYTE
02780 ------------------------------
02790 ;JETZT FOLGEN 2 CRC BYTES !
02800 ------------------------------
02810          LDA HEADBUF,Y
02820          BEQ .2
02830          LDA #$20    ;SET DD
02840          TRB $280
02850 .2       LDA #$F7
02860          JSR WRBYTE
02870          LDA #$20  ;SET SD
02880          TSB $280
02890          LDY #17
02900          LDA #$FF
02910          JSR WRBYTS
02920          LDY CSEC
02930          LDA HEADBUF+$100,Y
02940          AND #$10  ;MASK OUT
02950          BNE .3      ; RNF
02960          LDA HEADBUF+$17D
02970          BNE .31
02980 ------------------------------
02990 ;RAUM FUER DATEN FELD
03000 ------------------------------
03010 .32      LDA #$FB    DATA AM
03020          JSR WRBYTE
03030          LDY #$82    DATA FIELD
03040          LDA #$FF
03050          JSR WRBYTS
03060 ------------------------------
03070 .3       INC CSEC
03080          LDA YSAV
03090          CLC
03100          ADC #7
03110          STA YSAV
03120          CMP XSAV
03130          BCC .1
03140          LDA #1
03150 .11      AND $400
03160          BEQ .12
03170          BIT $280
03180          BPL .11
03190          STZ $403
03200          JMP .11
03210 .12      CLC
03220          RTS
03230 ------------------------------
03240 .31      LDX CSEC
03250          LDA HEADBUF+$120,X
03260          BEQ .32
03270          PHA
03280          LDA #$FB    DATA AM
03290          JSR WRBYTE
03300          PLA
03310          PHA
03320          TAY
03330          LDA #$FF
03340          JSR WRBYTS
03350          LDA #$FB
03360          JSR WRBYTE
03370          PLA
03380          SEC
03390          SBC #$80
03400          EOR #$FF
03410          TAY
03420          INY
03430          LDA #$20
03440          LDX #$F0
03450 .40      BIT $280
03460          BVC .41
03470          BPL .40
03480          STX $403
03490          DEX
03500          DEY
03510          BEQ .42
03520          TRB $280
03530 ------------------------------
03540 .45      BIT $280
03550          BVC .41
03560          BPL .45
03570          STX $403
03580          TSB $280
03590          DEX
03600          DEY
03610          BNE .40
03620 .42      TSB $280
03630          JMP .3
03640 .41      PLA
03650          PLA
03660          SEC
03670          RTS
03680 ------------------------------
03690 ;DIE WRITE - SECTOR ROUTINE HAT        KEIN ABBRUCH-KRITERIUM BEI
03700 ;TIMEOUT ODER RECORD NOT FOUND.
03710 ;DAS HEISST:
03720 ;ABSTURZ BEI ENDLOSSCHLEIFE.
03730 ;KEIN RETRY FLAG.
03740 ------------------------------
03750 WRSEC    STZ CSEC
03760          STZ YSAV
03770          LDA #SECBUF ;SET BUFFER
03780          STA $19    ;POINTER LO
03790          LDA /SECBUF
03800          STA $1A    ;POINTER HI
03810 ------------------------------
03820 .15      LDY #$A8
03830          LDX CSEC    ; INDEX X
03840          LDA HEADBUF+$17D
03850          BEQ .50
03860          LDA HEADBUF+$120,X
03870          BNE .30
03880 .50      LDA HEADBUF+$100,X
03890          ASL      ;NOT READY->C
03900          ASL      ;WR. PROT.->C
03910          ASL      ;C=1 DEL. DAM
03920          BCC .19
03930          INY
03940 ;
03950 .19      ASL         ;RNF->C
03960          BCS .21
03970          ASL        ;CRC ERR->C
03980          PHP        ;SAV CARRY
03990          LDX YSAV
04000          LDA HEADBUF+3,X
04010          STA $402   ;SET SEC.
04020 ------------------------------
04030          STY $400
04040          LDY #0
04050          LDA #$E6    ;SET
04060          STA $29F    ;TIMEOUT
04070 .11      LDA ($19),Y
04080          EOR #$FF
04090 .10      BIT $280
04100          BVC .22     ;TIMEOUT ?
04110          BPL .10     ;DRQ ?
04120          STA $403
04130          INY
04140          BPL .11
04150 ------------------------------
04160 ;$80 BYTES GESCHRIEBEN
04170 ------------------------------
04180          LDA HEADBUF+4,X ;ID
04190          BEQ .12    ;SECLEN=0 ?
04200          JSR CONRES
04210 .12      PLP         ;GET CARRY
04220          BCC .13    ;CRC ERROR?
04230          LDA #$20
04240          TAY
04250          TRB $280
04260 .13      LDA $400
04270          LSR
04280          BCS .13
04290          TYA
04300          TSB $280
04310 ------------------------------
04320 .1       LDA $19
04330          EOR #$80
04340          STA $19
04350          BMI .21
04360          INC $1A
04370 .21      INC CSEC
04380          LDA YSAV
04390          CLC
04400          ADC #7
04410          STA YSAV
04420          CMP XSAV
04430          BCC .15
04440          CLC
04450          RTS
04460 .22      JSR CONRES
04470          PLP
04480          SEC
04490          RTS
04500 ------------------------------
04510 .30      STA ZSAV
04520          LDX YSAV
04530          LDA HEADBUF+3,X
04540          STA $402    ; SECTOR
04550 ------------------------------
04560          LDY #$A8  WRITE SECTOR
04570          STY $400
04580          LDY #0
04590          LDA #$E6   ; SET
04600          STA $29F   ; TIMEOUT
04610 .31      LDA ($19),Y
04620          EOR #$FF
04630 .40      BIT $280
04640          BPL .40     ;DRQ ?
04650          STA $403
04660          INY        ;Y IN RANGE
04670          CPY ZSAV   ;OF 0-$7F !
04680          BCC .31
04690          JSR CONRES
04700          JMP .1
04710 ZSAV     .HX 00
04720 ------------------------------
04730 TRK00    JSR MOTON
04740          JSR TRACK0
04750          STZ $D
04760          JMP SENDC
04770 ------------------------------
04780 ;READSECTOR, ACCU = SECTOR NO
04790 ------------------------------
04800 RDSEC1   STA $402   ; SET SECTOR REGISTER
04810          LDA #$88  ;READ SECTOR
04820          STA $400
04830 ------------------------------
04840          LDY #0
04850          LDA #$E6  ;TIMEOUT
04860          STA $29F
04870 .1       BIT $280
04880          BVC .2
04890          BPL .1
04900          LDA #$A
04910          STA $29F
04920          LDA $403
04930          EOR #$FF
04940          STA ($19),Y
04950          INY
04960 .3       BIT $280
04970          BVC .5
04980          BPL .3
04990          LDA $403
05000          EOR #$FF
05010          STA ($19),Y
05020          INY
05030          BPL .3      ;$80 BYTES
05040          LDA #1
05050 .4       AND $400
05060          BNE .4
05070          LDA $400
05080          AND #$3E
05090          RTS
05100 .2       JSR CONRES
05110          LDA #$10
05120          RTS
05130 .5       JSR CONRES
05140          LDA #4
05150          RTS
05160 ------------------------------
05170 REFORM   JSR SEM0
05180          JSR MOTON
05190          JSR CLRTRA
05200          JMP SENDC
05210 ------------------------------
05220 SEM0     LDA $82
05230          STA XSAV
05240          LDA $83
05250          STA $D
05260          JMP TRACKPO
05270 ------------------------------
05280 SEM1     JSR SENDC
05290          LDA #1
05300          LDX #STBUF
05310          LDY /STBUF
05320          JMP SDBTS
05330 ------------------------------
05340 VERIFYFLG .HX 00
05350 ------------------------------
05360 SPECVERI LDX #$20
05370 .1       STZ HEADBUF+$120,X
05380          DEX
05390          BPL .1
05400          LDA #0
05410          .HX 2C      =BIT ABS.
05420 ------------------------------
05430 VERIFY   LDA #1
05440          STA VERIFYFLG
05450          LDY #0      ;SET PAR
05460          STY CSEC    ;TO ZERO
05470          STY YSAV
05480          LDA #SECBUF ;SET BUFFER
05490          STA $19     ;POINTER
05500          LDA /SECBUF
05510          STA $1A
05520          LDA XSAV
05530          BNE .2
05540          CLC
05550          RTS
05560 .2       LDY CSEC
05570          LDA HEADBUF+$100,Y
05580          AND #$10
05590          BNE .1
05600          LDY YSAV
05610          LDA HEADBUF+3,Y ;  SET
05620          JSR RDSEC2    ; SECTOR
05630          LDA VERIFYFLG  ; CARRY
05640          BEQ .13       ; BLEIBT
05650          BCS .99  ;UNVERAENDERT
05660 ------------------------------
05670 .13      LDA $19    ;INC BUFFER
05680          EOR #$80
05690          STA $19
05700          BCC .1
05710          INC $1A
05720 .1       INC CSEC
05730          LDA YSAV
05740          CLC
05750          ADC #7
05760          STA YSAV
05770          CMP XSAV
05780          BCC .2
05790          CLC
05800          RTS
05810 ------------------------------
05820 .99      SEC
05830          RTS
05840 ------------------------------
05850 RDSEC2   STA $402
05860          LDA #1
05870 .11      AND $400
05880          BNE .11
05890 ------------------------------
05900          LDA #$88
05910          STA $400
05920 ------------------------------
05930          LDY #0
05940          LDA #$FF    ;TIMEOUT
05950          STA $29F
05960 .1       BIT $280
05970          BVC .2
05980          BPL .1
05990          LDA $403
06000          EOR #$FF
06010          CMP ($19),Y
06020          BNE .2
06030          LDA $296  ;STOP TIMER?
06040          INY
06050 .3       BIT $280
06060          BPL .3
06070          LDA $403
06080          EOR #$FF
06090          CMP ($19),Y
06100          BNE .2
06110          INY
06120          BPL .3      ;$80 BYTES
06130          LDA #0
06140          LDY CSEC
06150          STA HEADBUF+$120,Y
06160          JSR CONRES
06170          CLC
06180          RTS
06190 .2       LDX CSEC
06200          TYA
06210          STA HEADBUF+$120,X
06220          JSR CONRES
06230          SEC
06240          RTS
06250 ------------------------------
06260 CRCCHECK LDY #0
06270          STY YSAV
06280          TYA
06290 .1       ORA HEADBUF+$100,Y
06300          INY
06310          CPY TSEC
06320          BCC .1
06330          AND #8
06340          CMP #1    ;IF ZERO C=1
06350          RTS
06360 ------------------------------
06370 ;HEADER LESE FUNKTION:
06380 ------------------------------
06390 READH    LDX #0     ;LOCAL VEC
06400          STX HEADBUF+$17D
06410          STX YSAV   ;GLOBAL VEC
06420 ------------------------------
06430 .2       LDA #$D6
06440          STA $29F
06450 .3       JSR RDHD1 ;GET NEXT HD
06460          BCS .4
06470          TAX
06480          LDA $7A
06490          CMP $D
06500          BNE .3
06510          LDA $7C
06520          BEQ .3
06530          CMP #19
06540          BCS .3
06550          TXA
06560 ------------------------------
06570          JSR SHTAB   ;& COPY HD
06580          JMP .3
06590 ------------------------------
06600 .4       LDY YSAV
06610          BEQ .6
06620          LDA HEADBUF+3
06630          CMP HEADBUF-4,Y
06640          BNE .5
06650          TYA
06660          SEC
06670          SBC #7
06680          TAY
06690          BRA .6
06700 .5       CMP HEADBUF-11,Y
06710          BNE .6
06720          TYA
06730          SEC
06740          SBC #14
06750          TAY
06760 ;
06770 .6       STY XSAV
06780          STY HEADBUF+$FF
06790          RTS
06800 ------------------------------
06810 ;SETZE HEADER UND STATUS IM            HEADERBUFFER :
06820 ;AUFBAU DES PUFFERS:
06830 ;BYTE:0 IST DER STATUS DIESES               HEADERS
06840 ;   1 ENTSPRICHT DEM TRACK
06850 ;   2    "        "  SEITENBYTE
06860 ;   3    "        "  SECTOR
06870 ;   4    "       DER LAENGE                 (NACH IBM STANDARD)
06880 ;   6 1. CRC BYTE
06890 ;   7 2. CRC BYTE
06900 ------------------------------
06910 SHTAB    LDY YSAV  ; GET Y
06920          STA HEADBUF,Y
06930          INY
06940          LDX #$7A
06950 .1       LDA $0,X
06960          STA HEADBUF,Y
06970          INY
06980          INX
06990          BPL .1
07000          STY YSAV
07010          RTS
07020 ------------------------------
07030 ;DRIVE DISPLAY CONTROL
07040 ------------------------------
07050 MEMDOOR  .HX 00
07060 BELL     = $FF99
07070 CLRDSP   = $FF9C
07080 HEXOUT   = $FFA5
07090 DOORCHECK = $FF6F
07100 CNT      .HX 0000
07110 LOOP     = 7
07120 ------------------------------
07130 DISKWAIT STZ $1D     ; LAST DOOR POSITION IS CLOSED
07140          LDA #1
07150          TRB $282   ; DAMIT ERHAELT DER POKEY EIN SERIAL FRAME.
07160          STZ MEMDOOR
07170 ------------------------------
07180 START    JSR CLRDSP
07190          STZ CNT
07200          LDA #LOOP   ;7
07210          STA CNT+1
07220 ------------------------------
07230          LDA #$FF
07240          STA $4002
07250          LDA #$CD
07260          JSR HEXOUT
07270          JSR BELL
07280 ------------------------------
07290 .0       JSR DISKCHECK  ; IST DIE KLAPPE GESCHLOSSEN WORDEN ?
07300          BCS .3     ; C=1 => DISK CHANGE
07310 ------------------------------
07320          JSR ESCTEST  ; IST IM COMPUTER 'ESC' GEDRUECKT ?
07330          BCS .3     ; C=1 => ESCAPE
07340 ------------------------------
07350          DEC CNT
07360          BNE .0
07370          DEC CNT+1
07380          BNE .0
07390 ------------------------------
07400 ;2. SCHLEIFE.
07410 ------------------------------
07420          JSR CLRDSP
07430          STZ CNT
07440          LDA #LOOP   ;7
07450          STA CNT+1
07460 ------------------------------
07470 .1       JSR DISKCHECK  ; IST DIE KLAPPE GESCHLOSSEN WORDEN ?
07480          BCS .3     ; C=1 => DISK CHANGE
07490 ------------------------------
07500          JSR ESCTEST  ; IST IM COMPUTER 'ESC' GEDRUECKT ?
07510          BCS .3     ; C=1 => ESCAPE
07520 ------------------------------
07530          DEC CNT
07540          BNE .1
07550          DEC CNT+1
07560          BNE .1
07570          JMP START
07580 ------------------------------
07590 .3       LDA #1
07600          TSB $282
07610          JMP CLRDSP
07620 ------------------------------
07630 CARRYC   CLC
07640          RTS
07650 CARRYS   SEC
07660          RTS
07670 ------------------------------
07680 DISKCHECK LDA MEMDOOR
07690          BNE .1
07700 ------------------------------
07710 ;LAUFWERKKLAPPE GEOEFFNET?
07720 ------------------------------
07730          JSR DOORCHECK
07740          AND #$80
07750          BEQ CARRYC
07760          STA MEMDOOR
07770 ------------------------------
07780 ;KLAPPE GESCHLOSSEN?
07790 ------------------------------
07800 .1       JSR DOORCHECK
07810          AND #$80
07820          BEQ CARRYS
07830          BRA CARRYC
07840 ------------------------------
07850 ESCTEST  LDA $282
07860          TAX
07870          AND #2
07880          BEQ .1
07890          JMP ($FFFC)
07900 .1       TXA
07910          AND #$80
07920          CMP #$80
07930          RTS
07940 ------------------------------
07950 ACTIVATE LDA #$82    ;SET SD
07960          STA $9      ;FORKEN
07970          STA $A      ;FORKEN2
07980          JSR SDRDDP
07990          LDA #$2C
08000          STA $17     ;STEPTIM
08010          LDA $9F80
08020          STA BEREIT
08030          LDA $9F80+1
08040          STA BEREIT+1
08050          LDA #NORM
08060          STA $9F80
08070          LDA /NORM
08080          STA $9F80+1
08090 ------------------------------
08100 NORM     STZ $1D
08110          LDA $282
08120          AND #2
08130          BNE .1
08140          JMP (BEREIT)
08150 .1       JMP ($FFFC)
08160 ------------------------------
08170 BEREIT   .DA $E100
08180 DRVEND

```
