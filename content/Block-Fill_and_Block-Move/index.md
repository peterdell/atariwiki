---
title: Block-Fill and Block-Move
---
# Block-Fill and Block-Move  
  
```
00010 ------------------------------
00020 *     Block-Fill-Routine     *
00030 *                            *
00040 * Registerinhalte:           *
00050 * <A> Fill-Byte              *
00060 * <X> Anzahl der Pages       *
00070 * <Y> Start Page             *
00080 *                            *
00090 ------------------------------
00100 *
00110 FILL     STY $1        Pointer und
00120          LDY #0        Index Setzen
00130          STY $0
00133 *
00140 .1       STA ($0),Y    Byte setzen
00150          INY           Index hochzaehlen
00160          BNE .1        wiederholen bis Ueberschlag
00170          INC $1        Pointer MSB hochzaehlen
00180          DEX           Noch Pages
00190          BNE .1        Uebrig? Ja ==>
00200          RTS
00210 ------------------------------
00220 *
00230 *
00240 *
00250 ------------------------------
00260 *    Block-Move-Routine      *
00270 *                            *
00280 * Registerinhalte:           *
00290 *                            *
00300 * <A> Source Page            *
00310 * <X> Anzahl der Pages       *
00320 * <Y> Destination Page       *
00330 *                            *
00340 ------------------------------
00350 *
00360 MOVE     STA $1        Pointer
00370          STY $FF       setzen
00380          LDY #0        Index
00390          STY $0        loeschen
00400          STY $FF
00410 *
00420 .1       LDA ($0),Y    Move
00430          STA ($FE),Y
00440          INY           Index hochzaehlen
00450          BNE .1        wiederholen bis Ueberschlag
00460          INC $1        Pointer MSB
00470          INC $FF       hochzaehlen
00480          DEX           Anzahl runterzaehlen
00490          BNE .1        Wiederholen
00500          RTS
```
  
### Block Move for Atari-BASIC  
  
```
00010          .LI OFF
00020 *
00030 ****************
00040 *              *
00050 * MOVE-Routine *
00060 *              *
00070 ****************
00080 *
00090 *
00100 *
00110 SCL      .EQ $CD
00120 DESTL    .EQ $CF
00130 BYTES    .EQ $D1
00140 *
00150 *
00160 *
00170 *
00180 *
00190 *
00200 START    PLA           Parameterzahl holen
00210 *
00220          PLA           Start-
00230          STA SCL+1     addresse
00240          PLA           holen
00250          STA SCL
00260 *
00270          PLA           Ziel-
00280          STA DESTL+1   addresse
00290          PLA           holen
00300          STA DESTL
00310 *
00320          PLA           Auch die
00330          STA BYTES+1   Laenge
00340          PLA           wird
00350          STA BYTES     gebraucht
00360 ------------------------------
00370 MOVE     LDY #0
00380 MOVEB    LDA (SCL),Y   Byte
00390          STA (DESTL),Y verschieben
00400 *
00410          INC SCL       Start-
00420          BNE .1        pointer
00430          INC SCL+1     hochzaehlen
00440 *
00450 .1       INC DESTL     Das gleiche
00460          BNE .2        mit Ziel-
00470          INC DESTL+1   Pointer
00480 *
00490 .2       LDA BYTES     Laenge
00500          BNE .3        abzaeh-
00510          DEC BYTES+1   len
00520 .3       DEC BYTES
00530 *
00540          LDA BYTES     Ende
00550          ORA BYTES+1   erreicht
00560          BNE MOVEB     Nein
00570          RTS           zurueck
```
