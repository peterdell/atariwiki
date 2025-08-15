---
title: Simple Disk Formatter
---
# Simple Disk Formatter  
  
```
00010          .LI OFF
00020          .OR $4000
00030 *
00040 *
00050 LM       =   $52
00060 CURX     =   $55
00070 CURY     =   $54
00080 *
00090 CURINH   =   752
00100 *
00110 *
00120 *
00130 S        LDA #0        Linker Rand
00140          STA LM        auf Null setzen
00150          INC CURINH    Cursor aus
00160          JSR PRINT
00170          .AS "}\240\240\240\240\240\240\240\240\240\240\240\240\240\240ƒœ”≠ƒÈÛÎ…ÓÈÙ\240\240\240\240\240\240\240\240\240\240\240\240\240\240"
00180          .AS "\^]\^]\^]\^]\M^Y±\^Y Disk formattieren und DOS schreiben"
00190          .HX 9B
00200          .AS "\^]\M^Y≤\^Y DOS auf formattierte Disk schreiben"
00210          .HX 9B
00220          .AS "\^]\M^Y≥\^Y Disk formattieren (Single)"
00230          .HX 9B
00240          .AS "\^]\M^Y¥\^Y Programm verlassen"
00250          .HX 9B
00260          .AS "\^]\^]\^]\^]\^?     Ihre Wahl?@"
00270 *
00280 GETOP    JSR GETKEY    Taste holen
00290          AND #$7F      invers aus
00300          CMP #'1       Nur Ziffern
00310          BCC GETOP     "1"-"4"
00320          CMP #'5       zulassen
00330          BCS GETOP
00340          AND #$F       obere Bits ausmaskieren
00350          PHA
00360          LDX #8        Cursor
00370          LDY #22       positionieren
00380          JSR POSCUR
00390          JSR PRINT
00400          .AS "Sind Sie sicher? (J/N)@"
00410          JSR GETKEY    Taste holen
00420          AND #$7F      kein invers
00430          CMP #'J       Kommando OK
00440          BEQ .1
00450          PLA           Nein. zurueck
00460          JMP S         zum Menue
00470 *
00480 .1
00490          LDA #$9C      Zeile loeschen
00500          JSR PUTCHAR
00510          PLA
00520          ASL           Addresse
00530          TAX           der
00540          LDA JTAB-1,X  Routine
00550          PHA           aufs
00560          LDA JTAB-2,X  Stack
00570          PHA           legen
00580          RTS           JUMP
00590 *
00600 *
00610 JTAB     .DA OP1-1,OP2-1
00620          .DA OP3-1,OP4-1
00630 *
00640 ------------------------------
00650 GETKEY   LDA $E425     Taste
00660          PHA           holen
00670          LDA $E424
00680          PHA
00690          RTS
00700 ------------------------------
00710 *
00720 OP1      JSR FDSK      Disk formattieren
00730          JSR WRITEDOS  DOS schreiben
00740 *
00750 READY    LDX #10       Cursor
00760          LDY #22       setzen
00770          JSR POSCUR
00780          JSR PRINT
00790          .AS "Fertig!!@"
00800          JSR GETKEY    Auf Taste warten
00810          JMP S
00820 *
00830 ------------------------------
00840 *
00850 OP2      JSR WRITEDOS  DOS schreiben
00860          JMP READY     nach READY
00870 *
00880 ------------------------------
00890 *
00900 OP3      JSR FDSK      Disk formattieren
00910          JMP READY
00920 *
00930 ------------------------------
00940 *
00950 OP4      LDA #'}       Bildschirm loeschen
00960          JMP PUTCHAR   zurueck
00970 *
00980 ------------------------------
00990 *
01000 FDSK     LDX #$10      Datenkanale 1 schliessen
01010          JSR CLOSE
01020          LDA #FN       Formattierungs-
01030          LDY /FN       routine auf-
01040          JMP FORMAT    rufen
01050 *
01060 ------------------------------
01070 *
01080 WRITEDOS LDX #$10      Datenkanal 1 schliessen
01090          JSR CLOSE
01100          LDX #$18      File DOS.SYS
01110          LDA #FN       zum schreiben oeffnen
01120          LDY /FN       und schliessen
01130          JSR OPEN      (den Rest erledigt
01140          JMP CLOSE     das DOS selber)
01150 *
01160 FN       .DA "D:DOS.SYS",#$9B
01170 *
01180 ------------------------------
01190 *
01200 POSCUR   STX CURX    Cursor
01210          STY CURY    positionieren
01220          RTS
01230 *
01240 ------------------------------
01250 *
01260          .IN "D:PRINTS.INC"
01270          .IN "D:IOPACK.INC"
```
