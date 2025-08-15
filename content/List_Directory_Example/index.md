---
title: List Directory Example
---
# List Directory example  
  
```
00010          .LI OFF
00020          .OR $4000
00030 *
00040 *
00050 COL1     .EQ $2C5
00060 COL2     .EQ $2C6
00070 COL4     .EQ $2C8
00080 CURINH   .EQ $2F0
00090 *
00100 IOBCCMD  .EQ $342
00110 IOBCBFL  .EQ $344
00120 IOBCBFH  .EQ $345
00130 IOBCLNL  .EQ $348
00140 IOBCLNH  .EQ $349
00150 IOBCAB1  .EQ $34A
00160 IOBCAB2  .EQ $34B
00170 *
00180 CIO      .EQ $E456
00190 *
00200 ROW      .EQ $54
00210 COLUMN   .EQ $55
00220 *
00230 *
00240 OPEN     .EQ 3
00250 GET      .EQ 7
00260 CLOSE    .EQ 12
00270 *
00280 *
00290 *
00300 *
00310 S        JSR EOPEN     Editor
00320          LDA #0        oeffnen
00330          STA COL2      Farben
00340          STA COL4      setzen
00350          LDA #$C       Cursor
00360          STA COL1      ausschal
00370          STA CURINH    ten.
00380          JSR PRINT
00390          .AS "}Demoprogramm auf der BIBOASSEMBLER"
00400          .HX 9B
00410          .AS "Tool Box Diskette................."
00420          .HX 9B
00430          .AS "\^]\^]\^?    Directory Drive 1\^]\^]@"
00440          JSR OPEND     Datenkanal oeffnen
00450          BMI EOF       Fehler, ja ==>
00460 LOOP     JSR PRINT     Positio-
00470          .HX 9B        nieren
00480          .AS "\^?    @"
00490 LOOP2    JSR GETBYTE   Zeichen holen
00500          CPY #1        Wenn fehler
00510          BNE EOF       dann End Of File
00520          CMP #$9B      Zeichen CR
00530          BEQ LOOP      Ja, Naechste Zeile
00540          JSR PUTCHAR   Zeichen drucken
00550          JMP LOOP2     weiter machen
00560 *
00570 EOF      JSR CLOSED    Datenkanal schliessen
00580          JSR TASTE     Warten
00590          JMP S         Wiederholen
00600 *
00610 ------------------------------
00620 OPEND    JSR CLOSED    Datenkanal schliessen
00630          LDX #$10      Kanal 1
00640          LDA #OPEN     Open
00650          STA IOBCCMD,X
00660          LDA #NAME     Filename
00670          STA IOBCBFL,X    Addresse
00680          LDA /NAME     in IOBC
00690          STA IOBCBFH,X
00700          LDA #6        Directory
00710          STA IOBCAB1,X
00720          LDA #0
00730          STA IOBCAB2,X
00740          JMP CIO
00750 ------------------------------
00760 GETBYTE  LDX #$10
00770          LDA #GET      Get Byte
00780          STA IOBCCMD,X
00790          LDA #0
00800          STA IOBCLNL,X    Len=0
00810          STA IOBCLNH,X
00820          JMP CIO
00830 ------------------------------
00840 CLOSED   LDX #$10
00850          LDA #CLOSE    Close
00860          STA IOBCCMD,X
00870          JMP CIO
00880 ------------------------------
00890 TASTE    LDA ROW       Cursor
00900          PHA           merken
00910          LDA COLUMN
00920          PHA
00930          LDA #23       Neue
00940          STA ROW       Position
00950          LDA #3        POS.3,23
00960          STA COLUMN
00970          JSR PRINT     Textausgabe
00980          .DA "\M^YƒÈÛÎÂÙÙÂ\240ÂÈÓÏÂÁÂÓ¨\240‘·ÛÙÂ\240‰ÚıÂ„ÎÂÓ\^Y@"
00990          JSR GETKEY    Auf Tastewarten
01000          PLA           Alten
01010          STA COLUMN       Cursor
01020          PLA           restau-
01030          STA ROW       rieren
01040          RTS
01050 ------------------------------
01060 GETKEY   LDA $E425     Siehe
01070          PHA           INOUT.INC
01080          LDA $E424
01090          PHA
01100          RTS
01110 ------------------------------
01120 EOPEN    LDA $E401     Editor
01130          PHA           oeffnen
01140          LDA $E400     JUMP
01150          PHA           ueber
01160          RTS           Stack
01170 ------------------------------
01180 NAME     .DA "D1:*.*",#$9B
01190 *
01200          .IN "D:PRINTS.INC"
```
