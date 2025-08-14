# Bitwise AND, OR, XOR and NOT for BASIC (USR Call)  
  
```
00010          .LI OFF
00020 *
00030 *****************************
00040 *                           *
00050 *Algebr. AND, OR, EOR u. NOT*
00060 *                           *
00070 *****************************
00080 *
00090 *
00100 WERT1    .EQ $CD
00110 WERT2    .EQ $CE
00120 COM      .EQ $CF
00130 *
00140 *
00150 *
00160 *
00170 *
00180 *
00190 *
00200 *
00210 START    LDA #0      Rueckgabe-
00220          STA $D4     register
00230          STA $D5     loeschen
00240 *
00250          PLA         Parameterzahl
00260 *
00270          PLA         Commando
00280          PLA         holen
00290          STA COM
00300 *
00310          PLA         Wert holen
00320          PLA
00330          STA WERT1
00340 *
00350          LDA COM     NOT
00360          CMP #'N     Funktion
00370          BEQ NOT     ja
00380 *
00390          PLA         2. Wert
00400          PLA         holen
00410          STA WERT2
00420 *
00430          LDA COM     EOR
00440          CMP #'E     Funktion
00450          BEQ EOR     ja
00460 *
00470          CMP #'O     OR Funtion
00480          BEQ OR      ja
00490 *
00500 AND      LDA WERT1   And Funtion
00510          AND WERT2
00520          CLC         unbedingter
00530          BCC STORE   Sprung
00540 ------------------------------
00550 OR       LDA WERT1   Or Funktion
00560          ORA WERT2
00570          CLC         Ohne
00580          BCC STORE   Bedingung
00590 ------------------------------
00600 EOR      LDA WERT1   Eor Funk-
00610          EOR WERT2   tion
00620          CLC
00630          BCC STORE   s.o.
00640 ------------------------------
00650 NOT      LDA WERT1   2er Kom-
00660          EOR #$FF    plement
00670          CLC         bilden
00680          ADC #1
00690 ------------------------------
00700 STORE    STA $D4     In Uebergabe
00710          RTS         Register
```
