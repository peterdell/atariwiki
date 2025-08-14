# Simple XOR encoding (for BASIC USR Call)  
  
```
00010          .LI OFF
00020 *
00030 ****************
00040 *              *
00050 * CODE-Routine *
00060 *              *
00070 ****************
00080 *
00090 *
00100 *
00110 SC       .EQ $CD
00120 BYTES    .EQ $CF
00130 WERT     .EQ $D1
00140 *
00150 *
00160 *
00170 *
00180 *
00190 START    PLA           Anzahl Parameter holen
00200 *
00210          PLA           Start
00220          STA SC+1 addresse
00230          PLA           holen
00240          STA SC
00250 *
00260          PLA           Laenge
00270          STA BYTES+1   holen
00280          PLA
00290          STA BYTES
00300 *
00310          PLA           Code-
00320          PLA           wert
00330          STA WERT      holen
00340 ------------------------------
00350 CODE     LDY #0
00360 .3       LDA (SC),Y    Wert
00370          EOR WERT      codieren
00380          STA (SC),Y
00390 *
00400          INC SC        Pointer
00410          BNE .1        hoch-
00420          INC SC+1      zaehlen
00430 *
00440 .1       LDA BYTES     Byte-
00450          BNE .2        zahl
00460          DEC BYTES+1   ernie-
00470 .2       DEC BYTES     drigen
00480 *
00490          LDA BYTES+1   Ende
00500          ORA BYTES     erreicht
00510          BNE .3        nein
00520          RTS           zureck
```
