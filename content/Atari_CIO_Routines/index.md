# Atari CIO Routines  
  
```
00010          .LI OFF
00020 *
00030 *
00040 IOCOM    =   $342
00050 IOBUFF   =   $344
00060 IOLEN    =   $348
00070 IOAUX1   =   $34A
00080 IOAUX2   =   $34B
00090 *
00100 CIO      =   $E456
00110 *
00120 *
00130 CLOSEF   =   12
00140 OPENF    =   3
00150 GETB     =   7
00160 PUTB     =   11
00170 FORMATF  =   254
00180 *
00190 *
00200 *
00210 ------------------------------
00220 * Routinen zum Schliessen,
00230 * Oeffnen, Lesen von Bytes,
00240 * Schreiben von Bytes und
00250 * Formattieren von Datenfiles
00260 * bzw Disketten
00270 ------------------------------
00280 *
00290 *
00300 *
00310 ------------------------------
00320 * CLOSE:
00330 * Datenkanalnummer *16 im
00340 * <X> Register.
00350 *
00360 ------------------------------
00370 *
00380 CLOSE    LDA #CLOSEF
00390          STA $342,X
00400          JSR CIO
00410          BPL .1
00420          JMP ERROR
00430 .1       RTS
00440 *
00450 ------------------------------
00460 *
00470 * OPEN:
00480 * <X> Register: Datenkanal*16+
00490 *               OPENspezifikation
00500 *               4: Lesen
00510 *               6: Directory
00520 *               8: Schreiben
00530 *               9: Append
00540 *              12: Update
00550 *
00560 * <A> Register: LO-Byte des
00570 *               Filenamepointers
00580 *
00590 * <Y> Register: HI-Byte des
00600 *               Filenamepointers
00610 *
00620 ------------------------------
00630 *
00640 OPEN     PHA
00650          TXA
00660          PHA
00670          AND #$70
00680          TAX
00690          PLA
00700          AND #$F
00710          STA IOAUX1,X
00720          LDA #0
00730          STA IOAUX2,X
00740          PLA
00750          STA IOBUFF,X
00760          TYA
00770          STA IOBUFF+1,X
00780          LDA #OPENF
00790          STA IOCOM,X
00800          JSR CIO
00810          BPL .1
00820          JMP ERROR
00830 .1       RTS
00840 *
00850 ------------------------------
00860 *
00870 * GETBYTES:
00880 * <A> Register: Page des Buffers
00890 * <X> Register: Datenkanal*16
00900 * <Y> Register: Laenge der Bytes
00910 ------------------------------
00920 *
00930 GETBYTES STA IOBUFF+1,X
00940          LDA #GETB
00950          STA IOCOM,X
00960          TYA
00970          STA IOLEN,X
00980          LDA #0
00990          STA IOBUFF,X
01000          STA IOLEN+1,X
01010          JMP CIO
01020          BPL .1
01030          JMP ERROR
01040 .1       RTS
01050 *
01060 ------------------------------
01070 *
01080 * PUTBYTES:
01090 * <A> Register: Page des Buffers
01100 * <X> Register: Datenkanal*16
01110 * <Y> Register: Laenge der Bytes
01120 ------------------------------
01130 *
01140 PUTBYTES STA IOBUFF+1,X
01150          LDA #PUTB
01160          STA IOCOM,X
01170          TYA
01180          STA IOLEN,X
01190          LDA #0
01200          STA IOBUFF,X
01210          STA IOLEN+1,X
01220          JMP CIO
01230          BPL .1
01240          JMP ERROR
01250 .1       RTS
01260 *
01270 ------------------------------
01280 *
01290 * FORMAT:
01300 * <A> Register: LO-Byte der De-
01310 *               viceaddresse
01320 * <Y> Register: HI-Byte der De-
01330 *               viceaddresse
01340 * <X> Register: Datenkanal*16
01350 *
01360 ------------------------------
01370 *
01380 FORMAT   STA IOBUFF,X
01390          TYA
01400          STA IOBUFF+1,X
01410          LDA #FORMATF
01420          STA IOCOM,X
01430          JSR CIO
01440          BPL .1
01450          JMP ERROR
01460 .1       RTS
01470 *
01480 ------------------------------
01490 *
01500 ERROR    TYA
01510          RTS
01520 *
01530 * Hier sollte eine eigene Feh-
01540 * lerroutine stehen.
01550 * <Y> Register haelt Fehler-
01560 * nummer.
```
  
### Call CIO from Atari Basic  
  
```
00010          .LI OFF
00020 *
00030 ****************
00040 *              *
00050 * CIO-Routinen *
00060 *              *
00070 ****************
00080 *
00090 *
00100 *
00110 CIOV     .EQ $E456
00120 *
00130 ICCOM    .EQ $0342
00140 ICSTAT   .EQ $0343
00150 ICBALO   .EQ $0344
00160 ICBLEN   .EQ $0348
00170 *
00180 COUNT    .EQ $CD
00190 *
00200 *
00210 *
00220 *
00230 *
00240 *
00250 START    PLA           Parameterzahl holen
00260 *
00270          PLA           Daten-
00280          PLA           kanalnr.
00290          ASL           holen
00300          ASL           *16
00310          ASL           als
00320          ASL           Index nach
00330          TAX           nach <X>
00340 *
00350          PLA           Kommando
00360          PLA           holen
00370          STA ICCOM,X
00380 *
00390          PLA           Daten
00400          STA ICBALO+1,X
00410          PLA           addresse
00420          STA ICBALO,X  holen
00430 *
00440          PLA           Daten-
00450          STA ICBLEN+1,X
00460          PLA           laenge
00470          STA ICBLEN,X  holen
00480 *
00490 EXEC     JSR CIOV      CIO aufrufen
00500 *
00510          LDA ICSTAT    Status
00520          STA $D4       ins
00530          LDA #0        Ueberga-
00540          STA $D5       beregis-
00550          RTS           ter
```
