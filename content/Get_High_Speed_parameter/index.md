---
title: Get High Speed parameter
---
# Get High Speed parameter  
  
```
0100 ;*************************************************
0110 ;*        Demonstration fuer Kommando $3F        *
0120 ;*  Uebertragungsrate fuer High-Speed ermitteln  *
0130 ;*************************************************
0140 ;
0150 DATBUF = $5000
0160 ;
0170     .OPT NO LIST
0180     .OPT OBJ
0190     *=  $4000
0200 ;
0210     LDA #$31    ; Bus ID
0220     STA $0300
0230     LDA #1      ; Laufwerks Nummer = 1
0240     STA $0301
0250     LDA #$3F    ; Kommando $3F
0260     STA $0302
0270     LDA #$40    ; Status fuer Daten lesen
0280     STA $0303
0290     LDA # <DATBUF ; Adresse fuer Datenbuffer Low
0300     STA $0304
0310     LDA # >DATBUF ; Adresse fuer Datenbuffer High
0320     STA $0305
0330     LDA #7      ; Wert fuer Timeout = 7 Sekunden
0340     STA $0306
0350     LDA #1      ; 1 Byte lesen
0360     STA $0308
0370     LDA #0
0380     STA $0309
0390     JSR $E459   ; Einsprung der SIO-Routine im OS
0400     BMI ERROR
0410     CLC
0420     RTS
0430 ERROR SEC
0440     RTS
```
