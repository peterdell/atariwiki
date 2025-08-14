# Der Display-List-Interrupt  
  
von Uwe Röder, CSM APRIL 1990  
  
  
Diese Folge des Assembler-Lehrganges ist im Grunde genommen eine Neuauflage aus meiner Serie über die Fähigkeiten unseres Ataris.  
  
Da ich in der letzten Ausgabe auf die Programmierung von Display-Lists eingegangen bin, dachte ich, dass nun unbedingt auch die Programmierung des Display-List Interrupts folgen muss.  
  
Der Display-List-Interrupt dient dazu, während des Bildschirmaufbaus den Bildschirm betreffende Daten zu verändern.  
  
Dies ist wohl die allgemeinste Definition. Konkret bedeutet dies für mich als Programmierer, dass ich praktisch nach jeder Bildschirmzeile einen neuen Zeichensatz, neue Farben usw. benutzen kann.  
  
Bei solchen einfachen Dingen, wie dem Umschalten eines Zeichensatzes oder dem Ändern der Hintergrundfarbe bedarf es im Grunde nur der elementarsten Befehle: LDA und STA  
  
Daran kann man schon erkennen wie einfach das Programmieren eines DLIs ist.  
  
Es gibt nur wenige Voraussetzungen, die erfüllt werden müssen, um einen DLI zu benutzen.  
  
Eine Grundbedingung ist, dass in der entsprechenden Zeile in der Display-List nach der der DLI ausgelöst werden soll Bit 7 gesetzt ist. Dies wurde ja schon letzten Monat deutlich gemacht.  
  
Wenn ich eine bereits existierende Display-List im Speicher nachträglich DLI-tauglich machen will, kann ich dies durch eine 'Oderierung' des entsprechenden Bytes mit $80 (128) erreichen.  
  
Danach muss die Adresse der Interrupt-Routine in [VDSLST](../VDSLST/index.md) $200,$201 (512,513) eingetragen werden und letztlich muss ich noch Bit 7 in [NMIEN](../NMIEN/index.md) $D40E (54286) setzen, damit der DLI auch ausgeführt wird. In aller Regel muss hier also $C0 (192) eingetragen werden. Bei der DLI-Routine ist noch zu beachten, dass die Registerinhalte (A,X,Y) vor und nach Aufruf der Routine identisch sein müssen, um einen System-Absturz zu vermeiden. Das heißt, dass die Registerinhalte direkt zu Beginn der Routine auf dem Stapel oder wo auch immer abgelegt werden und ganz am Ende der Routine wieder zurückgeholt werden müssen.  
  
Eine weitere (nicht zwingende) Bedingung ist das Arbeiten mit [WSYNC](../WSYNC/index.md) $D40A. Schreibt man vor dem Ändern einer Adresse einen Wert in WSYNC so wartet der Computer bis zum Beginn der nächsten Bildschirmzeile und nimmt erst dann die Änderung vor. Würde man beim Farbenumschalten auf diesen Vorgang verzichten, so kann es zu einem Flackern der Farbe im Umschaltbereich führen.  
  
Im übrigen ist es noch wichtig, dass man direkt die Hardwareregister verändert, da ein Umändern der Schattenregister erst nach dem vollständigen Aufbau des Bildschirms sichtbar wird!  
  
Als Beispiel für die Hardwareregister seien hier die wichtigsten für den DLI kurz angegeben:  
  
Farbregister: 708-712 ($2C4-$2C8)  
Hardwareregister: 53270-53274 ($D016-$D01A)  
  
Zeichensatz: 756 ($2F4)  
Hardwareregister: 54281 ($D409)  
  
  
Es ist weiterhin zu beachten, dass die Routine, die durch den DLI aufgerufen wird, nicht allzu lang ist, da sonst Probleme bei zeitkritischen Input/ Output Operationen entstehen können. So kann zum Beispiel der Diskettenzugriff trotz Speedy und High-Speed-SIO unendlich langsam werden oder gar ganz den Geist aufgeben.  
  
Sie finden im Anhang noch einige Beispiele dazu, doch will ich hier einmal ein sehr allgemeines Beispiel geben:  
  
```
00010          .LI OFF
00020 ------------------------------
00030 WSYNC    .EQ $D40A
00040 VSDLST   .EQ $200  ;DLI-VEKTOR
00050 SDLST    .EQ $230  ;DL-VEKTOR
00060 NMIEN    .EQ $D40E
00070 COLOR    .EQ $D018
00080 ADR      .EQ $D0
00090 ------------------------------
00100 START    LDA SDLST
00110          STA ADR
00120          LDA SDLST+1
00130          STA ADR+1
00140 ------------------------------
00150          LDY #16
00160 ;POSITION DES BYTES IN DL
00170 ------------------------------
00180          LDA (ADR),Y
00190          ORA #$80
00200          STA (ADR),Y
00210 ;BIT 7 IN DL SETZEN
00220 ------------------------------
00230          LDA #0
00240          STA NMIEN
00250 ;INTERRUPTS SPERREN
00260 ------------------------------
00270          LDA #DLI
00280          STA VSDLST
00290          LDA /DLI
00300          STA VSDLST+1
00310 ;DLI-ADRESSE IN VEKTOR
00320 ------------------------------
00330          LDA #$C0
00340          STA NMIEN
00350 ;INTERRUPTS FREIGEBEN
00360 ------------------------------
00370          RTS
00380 ;FERTIG !
00390 ------------------------------
00400 DLI      PHA
00410          TXA
00420          PHA
00430          TYA
00440          PHA
00450 ;REGISTER AUF STAPEL RETTEN
00460 ------------------------------
00470          LDA #$30
00480          STA WSYNC
00490 ;FLACKERN VERMEIDEN
00500          STA COLOR
00510 ;BELIEBIGE AENDERUNGEN ...
00520 ------------------------------
00530          PLA
00540          TAY
00550          PLA
00560          TAX
00570          PLA
00580 ;REGISTER ZURUECKHOLEN
00590 ------------------------------
00600          RTI
00610 ;ENDE DES DLI
00620 ------------------------------
```
Sie müssen sich also nur an das folgende einfache Schema halten:  
  
1. Bit 7 in Display-List setzen  
1. Interrupt sperren; NMIEN=0  
1. DLI-Adresse in VSDLST eintragen  
1. Interrupt freigeben; NMIEN=$C0  
  
In der DLI-Routine ist nur zu beachten, dass die Prozessor-Register gerettet und nur die Hardwareregister verändert werden. Um Flackern von Farben etc. zu vermeiden, sollte vor einer Farbänderung ein beliebiger Wert in WSYNC geschrieben werden.  
  
Also alles ganz einfach!!!  
  
Ich hoffe, Sie kommen mit allem klar. Wenn irgendwelche Unklarheiten existieren experimentieren Sie doch einfach mit den DEMO-Programmen. Sie sind im Bibo-Assemblerformat im Anhang.  
  
  
---
## Anahng  
### Beispiel 1 (DLI1.ASM)  
```
00010          .LI OFF
00020 ------------------------------
00030 WSYNC    .EQ $D40A
00040 VSDLST   .EQ $200  ;DLI-VEKTOR
00050 SDLST    .EQ $230  ;DL-VEKTOR
00060 NMIEN    .EQ $D40E
00070 COLOR    .EQ $D018
00080 ADR      .EQ $D0
00090 ------------------------------
00100 START    LDA SDLST
00110          STA ADR
00120          LDA SDLST+1
00130          STA ADR+1
00140 ------------------------------
00150          LDY #16
00160 ;POSITION DES BYTES IN DL
00170 ------------------------------
00180          LDA (ADR),Y
00190          ORA #$80
00200          STA (ADR),Y
00210 ;BIT 7 IN DL SETZEN
00220 ------------------------------
00230          LDA #0
00240          STA NMIEN
00250 ;INTERRUPTS SPERREN
00260 ------------------------------
00270          LDA #DLI
00280          STA VSDLST
00290          LDA /DLI
00300          STA VSDLST+1
00310 ;DLI-ADRESSE IN VEKTOR
00320 ------------------------------
00330          LDA #$C0
00340          STA NMIEN
00350 ;INTERRUPTS FREIGEBEN
00360 ------------------------------
00370          RTS
00380 ;FERTIG !
00390 ------------------------------
00400 DLI      PHA
00410          TXA
00420          PHA
00430          TYA
00440          PHA
00450 ;REGISTER AUF STAPEL RETTEN
00460 ------------------------------
00470          LDA #$30
00480          STA WSYNC
00490 ;FLACKERN VERMEIDEN
00500          STA COLOR
00510 ;BELIEBIGE AENDERUNGEN ...
00520 ------------------------------
00530          PLA
00540          TAY
00550          PLA
00560          TAX
00570          PLA
00580 ;REGISTER ZURUECKHOLEN
00590 ------------------------------
00600          RTI
00610 ;ENDE DES DLI
00620 ------------------------------
```
  
### Beispiel 2 (DLI2.ASM)  
```
00010          .LI OFF
00020 ------------------------------
00030 VDSLST   .EQ $200
00040 SDLSTL   .EQ $230
00050 DL       .EQ $D0
00060 COLOR    .EQ $D018
00070 WSYNC    .EQ $D40A
00080 VCOUNT   .EQ $D40B
00090 UHR      .EQ $14
00100 COLOR2   .EQ $D01A
00110 ------------------------------
00120 S        LDY #0
00130          LDA SDLSTL
00140          STA DL
00150          LDA SDLSTL+1
00160          STA DL+1
00170          LDA (DL),Y
00180          ORA #$80
00190          STA (DL),Y
00200          LDA #0
00210          STA $D40E
00220          LDA #DLI
00230          STA VDSLST
00240          LDA /DLI
00250          STA VDSLST+1
00260          LDA #$C0
00270          STA $D40E
00280          LDA #$E
00290          STA $2C5
00300          RTS
00310 ------------------------------
00320 DLI      PHA
00330          TXA
00340          PHA
00350          TYA
00360          PHA
00370 ------------------------------
00380          LDA #$50
00390          STA WSYNC
00400          STA COLOR2
00410          LDA #0
00420          STA COLOR
00430 .1       LDA VCOUNT
00440          CMP #$30
00450          BCC .1
00460          LDA #$30
00470          STA COLOR
00480 .2       LDA VCOUNT
00490          CMP #$50
00500          BCC .2
00510          LDA #$19
00520          STA COLOR
00530 ------------------------------
00540 .3       PLA
00550          TAY
00560          PLA
00570          TAX
00580          PLA
00590          RTI
00600 ------------------------------
```
  
### Beispiel 3 (DLI3.ASM)  
```
00010          .LI OFF
00020 ------------------------------
00030 COLOR    .EQ $D018
00040 VCOUNT   .EQ $D40B
00050 WSYNC    .EQ $D40A
00060 ADR      .EQ $D0
00070 ------------------------------
00080 S        LDA $230
00090          STA ADR
00100          LDA $231
00110          STA ADR+1
00120          LDY #2
00130          LDA (ADR),Y
00140          ORA #$80
00150          STA (ADR),Y
00160          LDY #12
00170          LDA (ADR),Y
00180          ORA #$80
00190          STA (ADR),Y
00200          LDY #$14
00210          LDA (ADR),Y
00220          ORA #$80
00230          STA (ADR),Y
00240          LDA #6
00250          LDX /VBI
00260          LDY #VBI
00270          JSR $E45C
00280          LDA #$E
00290          STA $2C5
00300          RTS
00310 ------------------------------
00320 VBI      LDA #0
00330          STA $D40E
00340          LDA #DL1
00350          STA $200
00360          LDA /DL1
00370          STA $201
00380          LDA #$C0
00390          STA WSYNC
00400          STA $D40E
00410          LDA #$90
00420          STA $2C8
00430          JMP $E45F
00440 ------------------------------
00450 DL1      PHA
00460          LDA #0
00470          STA WSYNC
00480          STA COLOR
00490          LDA #DL2
00500          STA $200
00510          LDA /DL2
00520          STA $201
00530          PLA
00540          RTI
00550 ------------------------------
00560 DL2      PHA
00570          LDA #$30
00580          STA WSYNC
00590          STA COLOR
00600          LDA #DL3
00610          STA $200
00620          LDA /DL3
00630          STA $201
00640          PLA
00650          RTI
00660 ------------------------------
00670 DL3      PHA
00680          LDA #$A0
00690          STA WSYNC
00700          STA COLOR
00710          LDA #DL1
00720          STA $200
00730          LDA /DL1
00740          STA $201
00750          PLA
00760          RTI
00770 ------------------------------
```
  
### Beispiel 4 (DLI4.ASM)  
```
00010          .LI OFF
00020 ------------------------------
00030 VDSLST   .EQ $200
00040 SDLSTL   .EQ $230
00050 DL       .EQ $D0
00060 COLOR    .EQ $D018
00070 WSYNC    .EQ $D40A
00080 VCOUNT   .EQ $D40B
00090 UHR      .EQ $14
00100 COLOR2   .EQ $D01A
00110 ------------------------------
00120 S        LDY #0
00130          LDA SDLSTL
00140          STA DL
00150          LDA SDLSTL+1
00160          STA DL+1
00170          LDA (DL),Y
00180          ORA #$80
00190          STA (DL),Y
00200          LDA #0
00210          STA $D40E
00220          LDA #DLI
00230          STA VDSLST
00240          LDA /DLI
00250          STA VDSLST+1
00260          LDA #$C0
00270          STA $D40E
00280          LDA #$E
00290          STA $2C5
00300          RTS
00310 ------------------------------
00320 DLI      PHA
00330          TXA
00340          PHA
00350          TYA
00360          PHA
00370 ------------------------------
00380          LDA #$50
00390          STA WSYNC
00400          STA COLOR2
00410          LDA #0
00420          STA COLOR
00430 .1       LDA VCOUNT
00440          CMP #$30
00450          BCC .1
00460          LDA #$30
00470          STA COLOR
00480 .2       LDA VCOUNT
00490          CMP #$50
00500          BCC .2
00510          LDA #$19
00520          STA COLOR
00530 ------------------------------
00540 .3       PLA
00550          TAY
00560          PLA
00570          TAX
00580          PLA
00590          RTI
00600 ------------------------------
```
  
