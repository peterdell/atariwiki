---
title: Integer Math
---
# Integer Math for 6502  
  
```
00010          .LI OFF
00030 * RECHENROUTINEN FUER GANZZAHLEN
00040 *
00050 *
00060 *
00070 *
00080 *
00090 *
00100 MLPCND   .EQ $D0
00110 MLPLER   .EQ $D1
00120 PROD     .EQ $D2
00130 *
00140 DVDND    .EQ $D4
00150 DVSOR    .EQ $D6
00160 RMNDR    .EQ $D8
00170 *
00180 RADCND   .EQ $DA
00190 ROOT     .EQ $DC
00200 TEMP     .EQ $DE
00210 SIGN     .EQ $DF
00220 *
00230 *
00240 *
00250 *
00260 *
00270 *
00280 SQUARE   LDA MLPCND    Multiplikant
00290          BPL POSITIV   =|MLPCND|
00300          SEC           Multiplikator
00310          LDA #$0
00320          SBC MLPCND
00330          STA MLPCND
00340 POSITIV  STA MLPLER
00350 *
00360 MULT     LDA #0
00370          LDX #8        8 Bits
00380 MLOOP    LSR MLPLER    Multiplikator/2
00390          BCC NOADD     Bit=0
00400          CLC           addiere
00410          ADC MLPCND    Multiplikanten
00420 NOADD    ROR           schiebe Bits
00430          ROR PROD      ins Produktregister
00440          DEX           Naechstes
00450          BNE MLOOP     Bit
00460          STA PROD+1    MSB Produkt
00470          RTS
00480 ------------------------------
00490 MULTV    LDA MLPCND    Vorzeichen
00500          EOR MLPLER    des Produktes
00510          AND #$80      bestimmen
00520          STA SIGN
00530          LDX #MLPCND   Berechnung
00540          JSR ABS8      von
00550          LDX #MLPLER   |MLPLER|*|MLPCND|
00560          JSR ABS8
00570          JSR MULT
00580          LDA SIGN      Ergebnis
00590          BPL .1        positiv?
00600          LDX #PROD     Vorzeichen des
00610          JSR CHS16     Produktes aendern
00620 .1       RTS
00630 ------------------------------
00640 ABS8     LDA $0,X      Absolutwert einer 8 Bit Zahl
00650          BPL AO        Zahl Positiv
00660 CHS8     LDA #0        Vorzeichen aendern
00670          SEC
00680          SBC $0,X
00690          STA $0,X
00700 AO       RTS
00710 *
00720 ABS16    LDA $1,X      Wie ABS8 Jedoch fuer 16 Bit Zahl
00730          BPL AO
00740 CHS16    JSR CHS8      Wie CHS8
00750          LDA #0
00760          SBC $1,X
00770          STA $1,X
00780          RTS
00790 ------------------------------
00800 DIVIDEV  LDA DVDND+1   Vorzeichen des
00810          EOR DVSOR+1   Quotienten
00820          AND #$80      bestimmen
00830          STA SIGN
00840          LDX #DVDND    Berechnung
00850          JSR ABS16     des Quotienten
00860          LDX #DVSOR    aus |DVDND|/|DVSOR|
00870          JSR ABS16
00880          JSR DIVIDE
00890          BCS .1        Division durch Null?
00900          LDA SIGN      Vorzeichen
00910          BPL .1        aendern wenn
00920          LDX #DVDND    Ergebnis
00930          JSR CHS16     negativ sein muss
00940          CLC
00950 .1       RTS
00960 ------------------------------
00970 DIVIDE   LDA DVSOR     Divisor=0
00980          ORA DVSOR+1   dann Error
00990          BNE DIVOK
01000          SEC
01010          RTS
01020 *
01030 DIVOK    LDA #$00      Werte vorbesetzen
01040          STA RMNDR
01050          STA RMNDR+1
01060 *
01070          LDX #$10      16 Bit
01080 DLOOP    ROL DVDND     Bit von DVDND nach
01090          ROL DVDND+1
01100          ROL RMNDR     RMNDR
01110          ROL RMNDR+1   schieben
01120          SEC
01130          LDA RMNDR     Wenn RMNDR-DVSOR>=0
01140          SBC DVSOR     dann
01150          TAY           RMNDR=
01160          LDA RMNDR+1   RMNDR-DVSOR
01170          SBC DVSOR+1
01180          BCC DECCNT
01190          STY RMNDR
01200          STA RMNDR+1
01210 DECCNT   DEX           Naechstes Bit
01220          BNE DLOOP
01221 *
01230          ROL DVDND     Anschaetzung
01240          ROL DVDND+1   fuer
01250          ASL RMNDR     Rundung
01260          ROL RMNDR+1
01270          BCS ROUND
01280          SEC
01290          LDA DVSOR
01300          SBC RMNDR
01310          LDA DVSOR+1
01320          SBC RMNDR+1
01330          BCS NOCHNG
01340 ROUND    INC DVDND     Ergebnis
01350          BNE NOCHNG    steht in
01360          INC DVDND+1   DVDND
01370 NOCHNG   CLC           No Error
01380          RTS
01390 *
01400 ------------------------------
01410 *
01420 SQRT     LDX #$8       Berechnung
01430          LDA #0        der Qudrat-
01440          STA ROOT      wurzel einer
01450          STA ROOT+1    16 Bit Zahl
01460          STA TEMP      Nach dem
01470          STA TEMP+1    Newton-
01480 SQRT1    ASL ROOT      Verfahren
01490          ROL ROOT+1
01500          INC ROOT
01510          BNE NEXT1
01520          INC ROOT+1
01530 NEXT1    ASL RADCND
01540          ROL RADCND+1
01550          ROL TEMP
01560          ROL TEMP+1
01570          ASL RADCND
01580          ROL RADCND+1
01590          ROL TEMP
01600          ROL TEMP+1
01610          SEC
01620          LDA TEMP
01630          SBC ROOT
01640          TAY
01650          LDA TEMP+1
01660          SBC ROOT+1
01670          BCC RESTOR
01680          STA TEMP+1
01690          STY TEMP
01700          INC ROOT
01710          BNE NEXT2
01720          INC ROOT+1
01730 NEXT2    DEX
01740          BNE SQRT1
01750          JMP FINIS
01760 RESTOR   SEC
01770          LDA ROOT
01780          SBC #1
01790          STA ROOT
01800          BCS NEXT3
01810          DEC ROOT+1
01820 NEXT3    DEX
01830          BNE SQRT1
01840 FINIS    ROR ROOT+1
01850          ROR ROOT
01860          RTS
01870 *
01880 WURZEL   LDA RADCND+1  Einsprung
01890          BMI WERR      in Wurzel-
01891          JSR SQRT      Routine
01900          JSR SQRT
01910          CLC           wenn
01920          RTS           Radikant positiv
01930 WERR     SEC           sonst Error
01940          RTS
```
