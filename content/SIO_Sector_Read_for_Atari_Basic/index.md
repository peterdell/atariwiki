---
title: SIO Sector Read for Atari Basic
---
# SIO Sector Read for Atari Basic  
  
```
00010          .LI OFF
00020 *
00030 *
00040 *******************
00050 *   SIO-Routine   *
00060 *******************
00070 *
00080 *
00090 *
00100 DRIVE    =   $301
00110 COM      =   $302
00120 STAT     =   $303
00130 BUFF     =   $304
00140 SECTOR   =   $30A
00150 *
00160 *
00170 DSK      =   $E453
00180 *
00190 *
00200 *
00210 LEN      =   $CB
00220 REG      =   $D4
00230 *
00240 *
00250 *
00260 *
00270 *
00280 S        PLA           Parameter holen
00290 *
00300          PLA           Laufwerks-
00310          PLA           Nummer holen
00320          STA DRIVE
00330 *
00340          PLA           Kommando holen
00350          PLA           'R=Read, 'W=Write
00360          STA COM       'S=Status, 'P=Put, '!=Format
00370 *
00380          PLA           Buffer
00390          STA BUFF+1    addresse
00400          PLA           holen
00410          STA BUFF
00420 *
00430          PLA           Sektor-
00440          STA SECTOR+1  holen
00450          PLA
00460          STA SECTOR
00470 *
00480          PLA           Anzahl
00490          STA LEN+1     der
00500          PLA           Sektoren
00510          STA LEN       holen
00520 ------------------------------
00530 LOOP     JSR DSK       Sektor lesen
00540          LDA STAT      Status holen
00550          BMI ERROR     Error, wenn negativ
00560 *
00570          INC SECTOR    Naechster
00580          BNE .1        Sektor
00590          INC SECTOR+1
00600 *
00610 .1       LDA BUFF      Buffer
00620          CLC           +Sektor-
00630          ADC #$80      laenge
00640          STA BUFF      ($80 Bytes)
00650          BCC .2        bei Single und Medium
00660          INC BUFF+1    Density)
00670 *
00680 .2       LDA LEN       Laenge
00690          BNE .3        runterzaehlen
00700          DEC LEN+1
00710          DEC LEN
00720 *
00730          LDA LEN       Schon alle
00740          ORA LEN+1     Sektoren
00750          BNE LOOP      geladen? Nein
00760          RTS           Zurueck
```
