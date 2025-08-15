---
title: Plot and Draw Routines
---
# Plot and Draw Routines  
  
from BiboAssembler Toolsdisk 1  
  
### Fast 2 color (Graphics 8) plot  
  
```
00010 PLOT     LDY OLDY      Zeilen-
00020          LDA TABLO,Y   addresse
00030          STA PNT       als
00040          LDA TABHI,Y   Pointer
00050          STA PNT+1     setzen
00060          LDA OLDX
00070          PHA           X MOD 8
00080          AND #7        nach <X>
00090          TAX
00100          LDA COLOR     Farbe
00110          AND #1        MOD 2
00120          TAY           nach <Y>
00130          LDA COLFILL,Y Farbyte holen
00140          AND EMASK,X   unnoetige Bits
00150          STA HOLD      ausmaskieren
00160          PLA           X/8=
00170          LSR           Byteoffset
00180          LSR
00190          LSR
00200          TAY           in Zeile <Y>
00210          LDA (PNT),Y   Graphicbyte Holen
00220          AND CMASK,X   alten Wert ausmaskieren
00230          ORA HOLD      und durch neuen ersetzen
00240          STA (PNT),Y   speichern
00250          RTS
00260 ;
00270 ------------------------------
00280 *                            *
00290 * Farbwerte und Loeschmasken *
00300 *                            *
00310 ------------------------------
00320 COLFILL  .HX 00FF
00330 EMASK    .HX 8040201008040201
00340 CMASK    .HX 7FBFDFEFF7FBFDFE

```
  
### Fast 4 Color Plot (Graphics 15)  
  
```
00010 PLOT     LDY OLDY      Zeilen-
00020          LDA TABLO,Y   addresse
00030          STA PNT       als
00040          LDA TABHI,Y   Pointer
00050          STA PNT+1     setzen
00060          LDA OLDX
00070          PHA           X MOD 4
00080          AND #3        nach <X>
00090          TAX
00100          LDA COLOR     Farbe
00110          AND #3        MOD 4
00120          TAY           nach <Y>
00130          LDA COLFILL,Y Farbyte holen
00140          AND EMASK,X   unnoetige Bits
00150          STA HOLD      ausmaskieren
00160          PLA           X/4=
00170          LSR           Byteoffset
00180          LSR
00190          TAY           in Zeile <Y>
00200          LDA (PNT),Y   Graphicbyte Holen
00210          AND CMASK,X   alten Wert ausmaskieren
00220          ORA HOLD      und durch neuen ersetzen
00230          STA (PNT),Y   speichern
00240          RTS
00250 ;
00260 ------------------------------
00270 *                            *
00280 * Farbwerte und Loeschmasken *
00290 *                            *
00300 ------------------------------
00310 COLFILL  .HX 0055AAFF
00320 EMASK    .HX C0300C03
00330 CMASK    .HX 3FCFF3FC
```
  
### Fast Plot for 16 color modes (Graphics 9)  
  
```
00010 PLOT     LDY OLDY      Zeilen-
00020          LDA TABLO,Y   addresse
00030          STA PNT       als
00040          LDA TABHI,Y   Pointer
00050          STA PNT+1     setzen
00060          LDA OLDX
00070          PHA           X MOD 2
00080          AND #1        nach <X>
00090          TAX
00100          LDA COLOR     Farbe
00110          AND #$F       MOD 16
00120          TAY           nach <Y>
00130          LDA COLFILL,Y Farbyte holen
00140          AND EMASK,X   unnoetige Bits
00150          STA HOLD      ausmaskieren
00160          PLA           X/2=
00170          LSR           Byteoffset
00180          TAY           in Zeile <Y>
00190          LDA (PNT),Y   Graphicbyte Holen
00200          AND CMASK,X   alten Wert ausmaskieren
00210          ORA HOLD      und durch neuen ersetzen
00220          STA (PNT),Y   speichern
00230          RTS
00240 ;
00250 ------------------------------
00260 *                            *
00270 * Farbwerte und Loeschmasken *
00280 *                            *
00290 ------------------------------
00300 COLFILL  .HX 00112233445566778899AABBCCDDEEFF
00310 EMASK    .HX F00F
00320 CMASK    .HX 0FF0
```
  
### Fast Draw Routines  
```
00010          .LI OFF
00020 ;
00030 OLDX     .EQ $D5
00040 OLDY     .EQ $D4
00050 TOX      .EQ $DB
00060 TOY      .EQ $DA
00070 ADX      .EQ $E0
00080 ADX2     .EQ $E1
00090 ADY      .EQ $E2
00100 ADY2     .EQ $E3
00110 DX       .EQ $E4
00120 DY       .EQ $E5
00130 SL       .EQ $E6
00140 COUNT    .EQ $E8
00150 COLOR    .EQ $E9
00160 HOLD     .EQ $EA
00170 *
00180 PNT      .EQ $D0
00190 ;
00200 SETTABLE LDA $58       Tabelle
00210          STA $00       der
00220          LDA $59       Anfangs-
00230          STA $01       addresse
00240          LDY #0        der
00250 SET      LDA $0        Bild-
00260          STA TABLO,Y   schirm-
00270          LDA $1        zeilen
00280          STA TABHI,Y   erzeugen
00290          CLC           (192 Zeilen)
00300          LDA $0
00310          ADC #40       UNBEDINGT
00320          STA $0        NACH DEM
00330          BCC SS1       GRAPHICAUFRUF
00340          INC $1        UND VOR DER
00350 SS1      INY           BENUTZUNG
00360          CPY #192      DER GRAPHICROUTINEN
00370          BNE SET       AUFRUFEN.
00380          RTS
00390 ;
00400 ;
00410 DRAWLINE LDX #0        Richtungen
00420          STX ADX2      vorbezetzen
00430          STX ADY
00440          STX SL+1
00450          INX
00460          STX COUNT
00470          STX ADY2
00480          STX ADX
00490 ;
00500          LDA TOX       Punktabstand
00510          SEC           berechnen
00520          SBC OLDX
00530          BCS DSKIP1
00540          DEC ADX       gegebenenfalls
00550          DEC ADX       Richtung
00560          LDA OLDX      aendern
00570          SEC
00580          SBC TOX
00590 DSKIP1   STA DX        Delta X
00600 *
00610          LDA TOY       Das gleiche
00620          SEC           fuer die
00630          SBC OLDY      Y-Koor-
00640          BCS DSKIP2    dinate
00650          DEC ADY2
00660          DEC ADY2
00670          LDA OLDY
00680          SEC
00690          SBC TOY
00700 DSKIP2   STA DY
00710          LDA DX        Ist
00720          CMP DY        dy>dx,
00730          BCS DSKIP3
00740          LDX DX        dann
00750          LDA DY        dx und dy
00760          STA DX        vertauschen
00770          STA DX
00780          TXA
00790          STA DY
00800          LDA ADX       auch Richtungen
00810          STA ADX2      fuer X und Y
00820          LDA ADY2      Koordinaten
00830          STA ADY       vertauschen
00840          LDA #0
00850          STA ADX
00860          STA ADY2
00870 DSKIP3   LDA DX        DX/2
00880          LSR           fuer Fehler-
00890          STA SL        groesse setzen
00900          LDA DX        mehr als
00910          BEQ RETURN    1 Punkt setzen?
00920          JSR PLOT      Punkt setzen
00930 ;
00940 MAIN     LDA OLDX      Richtungen
00950          CLC           zu Koor-
00960          ADC ADX       dinaten
00970          STA OLDX      rechnen
00980          LDA OLDY
00990          CLC
01000          ADC ADY
01010          STA OLDY
01020          INC COUNT
01030 *
01040          LDA SL        Fehler-
01050          CLC           groesse
01060          ADC DY        SL+DY
01070          STA SL
01080          BCC .1
01090          INC SL+1
01100 *
01110 .1       LDA SL+1      SL>DX?
01120 *
01130          BNE SUB
01140          LDA DX
01150          CMP SL
01160          BCS DPLOT
01170 *
01180 SUB      LDA SL        SL=SL-DX
01190          SEC
01200          SBC DX
01210          STA SL
01220          BCS .1
01230          DEC SL+1
01240 *
01250 .1       LDA OLDX      Schritt in
01260          CLC           2. Richtung
01270          ADC ADX2      machen
01280          STA OLDX
01290          LDA OLDY
01300          CLC
01310          ADC ADY2
01320          STA OLDY
01330 *
01340 DPLOT    LDA DX        Letzter Punkt
01350          CMP COUNT     erreicht
01360          BCC RETURN    Ja!
01370          JSR PLOT      Sonst Punkt setzen
01380          JMP MAIN      Wiederholen
01390 ;
01400 RETURN   LDA TOY       OLD-Koor.
01410          STA OLDY      =TO-Koor.
01420          LDA TOX
01430          STA OLDX
01440          JMP PLOT      Punkt setzen.
01450 *
01460 OPENS    STA $2B       Graphicstufe setzen
01470          LDA #0        Ohne Textfenster
01480          STA $2A
01490          LDA #$70      Source Code
01500          STA $6A       sichern
01510          JSR OPEN      OS-OPEN
01520          JMP SETTABLE  Tabelle setzen
01530 *
01540 OPEN     LDA $E411     ROM-Jump
01550          PHA           ueber
01560          LDA $E410     Stack
01570          PHA
01580          RTS
01590 ------------------------------
01600 TABLO    .BL 192       Platz fuer
01610 TABHI    .BL 192       Tabellen

```
  
### Graphics 9 Draw Demo  
```
00010          .LI OFF
00020          .OR $4000
00030 *
00040 *
00050 *
00060 *
00070 *
00080 *
00090 START    LDA #$90      Source Code
00100          STA $6A       sichern
00110 *
00120          LDA #$0       Graphic 9
00130          STA $2A       aufrufen
00140          LDA #$9
00150          STA $2B
00160          JSR OPEN
00170 *
00180          LDA #79       Werte und
00190          STA X         Cursor
00200          STA $56       vorbereiten
00210          STA $56
00220          STA $5C
00230 *
00240 LOOP     LDA X         Punkt
00250          STA $55       (X,0) in
00260          AND #$F       Farbe
00270          STA COL       X MOD 16
00280          LDA #0        setzen
00290          STA $54
00300          LDX #6
00310          JSR PLOT
00320          DEC $55
00330          LDA #79       Verbindungs-
00340          SEC           linie nach
00350          SBC X         (79-x,191)
00360          STA $5B       ziehen
00370          LDA #191
00380          STA $5A
00390          LDX #$A
00400          JSR DRAW
00410          DEC X         X=X+1
00420          LDA X         Bis X negativ
00430          BPL LOOP
00440 ------------------------------
00450 WAIT     JMP WAIT      endlos
00460 ------------------------------
00470 X        .HX 00
00480 Y        .HX 00
00490 COL      .HX 00
00500 ------------------------------
00510 ------------------------------
00520 OPEN     LDA $E411     Screen
00530          PHA           OPEN
00540          LDA $E410     ueber
00550          PHA           Stack
00560          RTS
00570 ------------------------------
00580 DRAW     LDA #17       Drawkommando
00590          STA $22       setzen
00600 PLOT     LDA $E411,X   Screen PUT
00610          PHA           ueber
00620          LDA $E410,X   Stack
00630          PHA           Jump
00640          LDA COL
00650          RTS

```
  
### Graphics 9 Demo 2  
```
00010          .LI OFF
00020          .OR $4000
00030 *
00040 S        LDA #$90      HiMem
00050          STA $6A       runtersetzen
00060 *
00070          LDA #$0       Graphic 9
00080          STA $2A       aufrufen
00090          LDA #$9
00100          STA $2B
00110          JSR OPEN
00120 *
00130          LDA #0        Cursor-
00140          STA X         sitionen
00150          STA $56       setzen
00160          STA $5C
00170 *
00180 LOOP     LDA X         Von-Ko-
00190          STA $55       ordinate
00200          EOR #$F       und Farbe
00210          STA COL       setzen
00220          LDA #0
00230          STA $54
00240 *
00250          LDX #6        Punkt
00260          JSR PLOT      setzen
00270 *
00280          DEC $55
00290 *
00300          LDA #79       Linie
00310          STA $5B       nach
00320          LDA #191      79,191
00330          STA $5A       ziehen
00340          LDX #$A
00350          JSR DRAW
00360 *
00370          LDA #0        Punkt
00380          STA $54       0,0
00390          STA $55       setzen
00400          LDX #6
00410          JSR PLOT
00420          DEC $55
00430 *
00440          LDA #79       und mit
00450          SEC           Punkt
00460          SBC X         79-X,191
00470          STA $5B       durch
00480          LDA #191      Linie
00490          STA $5A       verbinden
00500          LDX #$A
00510          JSR DRAW
00520 *
00530          INC X         X=X+1
00540          LDA X         Wiederholen
00550          CMP #80       bis X=80
00560          BNE LOOP
00570 ------------------------------
00580 WAIT     JMP WAIT      Endlos
00590 ------------------------------
00600 X        .HX 00
00610 Y        .HX 00
00620 COL      .HX 00
00630 ------------------------------
00640 ------------------------------
00650 OPEN     LDA $E411     Screen
00660          PHA           OPEN
00670          LDA $E410     ueber
00680          PHA           Stack
00690          RTS           Jump
00700 ------------------------------
00710 DRAW     LDA #17       Draw-Kommando
00720          STA $22       setzen
00730 PLOT     LDA $E411,X   Point-PUT
00740          PHA           Vector
00750          LDA $E410,X   auf Stack
00760          PHA           legen
00770          LDA COL       Farbe nach <A>
00780          RTS           Jump
```
  
### Graphic 8 Demo  
  
- File GR8PACK.INC  
  
```
00010 XO       .EQ $D0
00020 YO       .EQ $D2
00030 XT       .EQ $D3
00040 YT       .EQ $D5
00050 AX       .EQ $D6
00060 AX2      .EQ $D8
00070 AY       .EQ $DA
00080 AY2      .EQ $DB
00090 DX       .EQ $DC
00100 DY       .EQ $DE
00110 SL       .EQ $DF
00120 C        .EQ $E1
00130 *
00140 OFF1     .EQ $E3
00150 OFF2     .EQ $E4
00160 BIT1     .EQ $E5
00170 BIT2     .EQ $E6
00180 *
00190 PNT      .EQ $E7
00200 *
00210 BX1      .EQ $E9
00220 BY1      .EQ $EB
00230 BX2      .EQ $EC
00240 BY2      .EQ $EE
00250 *
00260 SAVMSC   .EQ $58
00270 *
00280 *
00290 *
00300 *
00310 *
00320 *
00330 *
00340 OPENGR8  LDA #0        Graphic
00350          STA $2A       8 Bild-
00360          LDA #8        schirm
00370          STA $2B       oeffen
00380          LDA #$70
00390          STA $6A
00400          JSR SOPEN
00410 *
00420          LDA SAVMSC
00430          STA PNT
00440          LDA SAVMSC+1
00450          STA PNT+1
00460          LDY #0
00470 *
00480 .1       LDA PNT       Zeilen-
00490          STA LOTAB,Y   addressen
00500          LDA PNT+1     tabelle
00510          STA HITAB,Y   erzeugen
00520          CLC
00530          LDA PNT
00540          ADC #40
00550          STA PNT
00560          BCC .2
00570          INC PNT+1
00580 .2       INY
00590          CPY #192
00600          BCC .1
00610 *
00620          LDX #0        Tabelle
00630 .3       TXA           mit
00640          LSR           Offset/8
00650          LSR
00660          LSR           erzeugen
00670          STA RSH8,X
00680          INX
00690          BNE .3
00700          RTS
00710 ------------------------------
00720 SOPEN    LDA $E411     Rom
00730          PHA           jump
00740          LDA $E410     fuer
00750          PHA           OPEN
00760          RTS
00770 ------------------------------
00780 PLOT     LDX YO        Zeilenaddresse
00790          LDA LOTAB,X   nach
00800          STA PNT       pointer
00810          LDA HITAB,X
00820          STA PNT+1
00830 *
00840          LDY XO+1      Byte-
00850          LDX XO        offset
00860          LDA HI,Y      aus X-
00870          ORA RSH8,X    Koordinate
00880          TAY           berechnen
00890 *
00900          TXA           Bit innerhalb
00910          AND #7        Byte
00920 *
00930 MO       ORA #0        +0 oder +8 je nach Modus
00940          TAX
00950          LDA (PNT),Y   Byte laden
00960 CM       ORA MASK,X    Manipulieren
00970          STA (PNT),Y   Speichern
00980          RTS
00990 *
01000 MASK     .HX 80402010080402017FBFDFEFF7FBFDFE
01010 HI       .HX 0020
01020 *
01030 CMD      .HX 1D3D5D  Opcodes fuer ORA, AND, EOR
01040 OFF      .HX 000800  Maskenoffset
01050 ------------------------------
01060 SETMODE  LDA CMD,X   Opcode
01070          STA CM      setzen
01080          STA CM1
01090          AND #$F3    auf indiziert Y-Opcode umrechnen
01100          STA CM2
01110          LDA OFF,X   Maskenoffset
01120          STA MO+1    setzen
01130          STA MO1+1
01140          RTS
01150 ------------------------------
01160 HLINE    LDX XO+1    Byte und
01170          LDA HI,X    Bit Pos-
01180          LDX XO      itionen
01190          ORA RSH8,X  der Start
01200          STA OFF1    X-Koor-
01210          TXA         dinate
01220          AND #7      berechnen
01230          STA BIT1
01240 *
01250          LDX XT+1    Das selbe
01260          STX XO+1    mit der
01270          LDA HI,X    Ziel
01280          LDX XT      X-Koor-
01290          STX XO      dinate
01300          ORA RSH8,X  und
01310          STA OFF2    Start=Ziel
01320          TXA         Koordinate
01330          AND #7
01340          STA BIT2
01350 *
01360          LDA OFF1    Subtraktion
01370          SEC         der Bytepositionen
01380          SBC OFF2    Wenn Ergebnis
01390          STA DX      >=0 dann vertauschen
01400          BCS EXOFF
01410 *
01420 HOTHER   LDA OFF2    Absulutwert
01430          SEC         der Bytepositionen
01440          SBC OFF1
01450          STA DX
01460          JMP HSETRD  weiter
01470 *
01480 EXOFF    LDX OFF2    Byte und
01490          LDA OFF1    Bit Posi-
01500          STA OFF2    tionen
01510          STX OFF1    vertau-
01520          LDX BIT1    schen
01530          LDA BIT2
01540          STA BIT1
01550          STX BIT2
01560 *
01570 HSETRD   LDX YO      Addresse
01580          LDA LOTAB,X des Zei-
01590          STA PNT     lenanfangs
01600          LDA HITAB,X in Pointer
01610          STA PNT+1   Register
01620 *
01630          LDA DX      Start und Ziel Koordinate
01640          BNE HLINE2  im selben Byte? Nein
01650 *
01660          LDX BIT1    Balkenwert
01670          LDY BIT2    berechnen
01680          LDA HMASK1,Y
01690          AND HMASK2,X
01700          STA SETBY+1 und ein-
01710          LDY OFF1    setzen
01720          JMP SETBY
01730 *
01740 HLINE2   CMP #2      Start und Ziel Koordinate in
01750          BCC SETBORD 2 nebeneinanderliegenden Byte? Ja
01760 *
01770          LDY OFF1    Bytes zwischen
01780          LDA #$FF    OFF1+1 und
01790          STA SETBY+1 OFF2-1
01800          INY         mit #$FF
01810 HLL1     JSR SETBY   fuellen
01820          INY
01830          CPY OFF2
01840          BCC HLL1
01850 *
01860 SETBORD  LDY OFF1      Werte
01870          LDX BIT1      fuer
01880          LDA HMASK1,X  Randbytes
01890          STA SETBY+1   einsetzen
01900          JSR SETBY
01910          LDY OFF2
01920          LDX BIT2
01930          LDA HMASK2,X
01940          STA SETBY+1
01950 *
01960 SETBY    LDA #$FF
01970 CM2      ORA (PNT),Y
01980          STA (PNT),Y
01990          RTS
02000 *
02010 HMASK1   .HX FF7F3F1F0F070301
02020 HMASK2   .HX 80C0E0F0F8FCFEFF
02030 ------------------------------
02040 VLINE    LDX XO+1      Byteposition
02050          LDA HI,X      bestimmen
02060          LDX XO
02070          ORA RSH8,X
02080          TAY
02090 *
02100          LDA YO        Anzahl
02110          SEC           der
02120          SBC YT        Zeilen
02130          BCC OTHER     bestimmen
02140          LDX YT        <X> haelt
02150          STA DY        die kleinere
02160          JMP VSETRD    der beiden
02170 *                      Y-Koordinaten
02180 OTHER    LDA YT
02190          SEC
02200          SBC YO
02210          STA DY
02220          LDX YO
02230 *
02240 VSETRD   INC DY
02250          LDA LOTAB,X   Zeilenaddresse
02260          STA PNT       holen
02270          LDA HITAB,X
02280          STA PNT+1
02290          LDA XO        Bitposition
02300          AND #7        bestimmen
02310 MO1      ORA #0        + Modusoffset
02320          TAX
02330 VLL      LDA (PNT),Y   Byte manipulieren
02340 CM1      ORA MASK,X
02350          STA (PNT),Y
02360          CLC           Pointer
02370          LDA PNT       +40
02380          ADC #40       Fuer
02390          STA PNT       naechste
02400          BCC VLSK      Bildzeile
02410          INC PNT+1
02420 VLSK     DEC DY        Wiederholen
02430          BNE VLL
02440          LDA YT        Koordinaten-
02450          STA YO        anpassung
02460          RTS
02470 *
02480 DRAWLINE LDX #0        Erklaerung
02490          STX C         siehe
02500          STX C+1       im
02510          STX AX2       DRAW.INC
02520          STX AX2+1     File
02530          STX AY
02540          STX SL+1
02550          STX AX+1
02560          INX
02570          STX AX
02580          STX AY2
02590          LDA XO
02600          EOR XT
02610          BNE TST2
02620          EOR XO+1
02630          EOR XT+1
02640          BNE TST2
02650          JMP VLINE
02660 *
02670 TST2     LDA YO
02680          EOR YT
02690          BNE NORMDRAW
02700          JMP HLINE
02710 *
02720 NORMDRAW JSR PLOT
02730 *
02740          SEC
02750          LDA XT
02760          SBC XO
02770          STA DX
02780          LDA XT+1
02790          SBC XO+1
02800          BPL D1OK
02810 *
02820          LDA #$FF
02830          STA AX
02840          STA AX+1
02850          SEC
02860          LDA XO
02870          SBC XT
02880          STA DX
02890          LDA XO+1
02900          SBC XT+1
02910 *
02920 D1OK     STA DX+1
02930          SEC
02940          LDA YT
02950          SBC YO
02960          BCS D2OK
02970 *
02980          LDA #$FF
02990          STA AY2
03000          SEC
03010          LDA YO
03020          SBC YT
03030 *
03040 D2OK     STA DY
03050 *
03060          LDA DX+1
03070          BNE MAIN1
03080          LDA DY
03090          CMP DX
03100          BEQ SWITCH
03110          BCC MAIN1
03120 *
03130 SWITCH   LDA DX
03140          PHA
03150          LDA DY
03160          STA DX
03170          PLA
03180          STA DY
03190          LDA AX
03200          STA AX2
03210          LDA AX+1
03220          STA AX2+1
03230          LDA AY2
03240          STA AY
03250          LDA #0
03260          STA AX
03270          STA AX+1
03280          STA AY2
03290 *
03300 MAIN1    LDA DX+1
03310          LSR
03320          LDA DX
03330          ROR
03340          STA SL
03350          LDA DX
03360          ORA DX+1
03370          BNE DRAWM
03380          JMP PLOT
03390 *
03400 DRAWM    LDA XO
03410          CLC
03420          ADC AX
03430          STA XO
03440          LDA XO+1
03450          ADC AX+1
03460          STA XO+1
03470          CLC
03480          LDA YO
03490          ADC AY
03500          STA YO
03510          INC C
03520          BNE DS1
03530          INC C+1
03540 *
03550 DS1      LDA SL
03560          CLC
03570          ADC DY
03580          STA SL
03590          BCC DS2
03600          INC SL+1
03610 *
03620 DS2      LDA DX+1
03630          CMP SL+1
03640          BEQ TST
03650          BCS OUTP
03660          BCC ADDJ
03670 TST      LDA DX
03680          CMP SL
03690          BEQ ADDJ
03700          BCS OUTP
03710 *
03720 ADDJ     CLC
03730          LDA XO
03740          ADC AX2
03750          STA XO
03760          LDA XO+1
03770          ADC AX2+1
03780          STA XO+1
03790 *
03800          LDA YO
03810          CLC
03820          ADC AY2
03830          STA YO
03840 *
03850          SEC
03860          LDA SL
03870          SBC DX
03880          STA SL
03890          LDA SL+1
03900          SBC DX+1
03910          STA SL+1
03920 *
03930 OUTP     LDA DX+1
03940          CMP C+1
03950          BNE OUTP1
03960          LDA DX
03970          CMP C
03980          BNE OUTP1
03990          JMP PLOT
04000 *
04010 OUTP1    JSR PLOT
04020          JMP DRAWM
04030 ------------------------------
04040 LOTAB    .BL 192
04050 HITAB    .BL 192
04060 RSH8     .BL 256
04070 ------------------------------
04080 *
04090 BOX      LDA BX1
04100          STA XO        Zeichnet
04110          LDA BX1+1     einen
04120          STA XO+1      Rahmen
04130          LDA BY1       mit
04140          STA YO        den
04150          STA YT        beiden
04160          LDA BX2       gegen-
04170          STA XT        ueber-
04180          LDA BX2+1     liegen-
04190          STA XT+1      den Eck-
04200          JSR DRAWLINE  Punktko-
04210          LDA BY2       ordi-
04220          STA YT        naten
04230          JSR DRAWLINE  aus
04240          LDA BX1       BX1,BY1
04250          STA XT        und
04260          LDA BX1+1     BX2,BY2
04270          STA XT+1
04280          JSR DRAWLINE
04290          LDA BY1
04300          STA YT
04310          JMP DRAWLINE

```
  
- File GR8PACK2.DEM  
```
00010          .LI OFF
00020          .OR $4000
00030 *
00040 *
00050 *
00060 *
00070 *
00080 *
00090 *
00100 *
00110 ------------------------------
00120          .IN "D:GR8PACK.INC"
00130 ------------------------------
00140 *
00150 DEMO     JSR OPENGR8
00160          LDX #2
00170          JSR SETMODE
00180          LDA #0
00190          STA WERT
00200 *
00210 LL1      LDA #191
00220          SEC
00230          SBC WERT
00240          STA WERT2
00250          STA YO
00260          LDA #0
00270          STA $2C6
00280          STA XO
00290          STA XO+1
00300          LDA #319
00310          STA XT
00320          LDA /319
00330          STA XT+1
00340          LDA WERT
00350          STA YT
00360          JSR DRAWLINE
00370          LDA WERT
00380          STA YO
00390          LDA #0
00400          STA XO
00410          STA XO+1
00420          LDA WERT2
00430          STA YT
00440          JSR DRAWLINE
00450          LDA WERT
00460          CLC
00470          ADC #7
00480          CMP #192
00490          BCC .1
00500          SEC
00510          SBC #192
00520 .1       STA WERT
00530          LDA #$FF
00540          CMP 764
00550          BEQ LL1
00560          STA 764
00570          JSR OPENGR8
00580 *
00590 DM2      LDA WERT
00600          STA BX1
00610          STA BY1
00620          LDA #0
00630          STA BX1+1
00640          LDA #191
00650          SEC
00660          SBC WERT
00670          STA BY2
00680          LDA #319
00690          LDX /319
00700          SEC
00710          SBC WERT
00720          STA BX2
00730          BCS .1
00740          DEX
00750 .1       STX BX2+1
00760          JSR BOX
00770          LDA WERT
00780          CLC
00790          ADC #115
00800          CMP #192
00810          BCC .2
00820          SEC
00830          SBC #192
00840 .2       STA WERT
00850          LDA #$FF
00860          CMP 764
00870          BEQ DM2
00880          STA 764
00890          JMP DEMO
00900 *
00910 WERT     .HX 00
00920 WERT2    .HX 00

```
