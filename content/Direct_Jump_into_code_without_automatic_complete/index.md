---
title: Direct Jump into code without automatic complete
---
# Speedy 1050 Direct Jump example  
  
```
0100 ;*************************************
0110 ;*  Demonstration fuer Kommando $4C  *
0120 ;* Einsprungbefehl. "C" - Complete   *
0130 ;* muss selbst gesendet werden !     *
0140 ;*************************************
0150 ;
0160 GOADR = $FF5A   ; Einsprungadresse fuer "C" - Complete senden
0170 ;
0180     .OPT NO LIST
0190     .OPT OBJ
0200     *=  $4000
0210 ;
0220     LDA #$31    ; Bus ID
0230     STA $0300
0240     LDA #1      ; Laufwerks Nummer = 1
0250     STA $0301
0260     LDA #$4C    ; Kommando $4C
0270     STA $0302
0280     LDA #0      ; Status fuer keine Daten senden oder empfangen
0290     STA $0303
0300     LDA #7      ; Wert fuer Timeout = 7 Sekunden
0310     STA $0306
0320     LDA # <GOADR ; Einsprungadresse Low Byte
0330     STA $030A
0340     LDA # >GOADR ; Einsprungadresse High Byte
0350     STA $030B
0360     JSR $E459   ; Einsprung der SIO-Routine im OS
0370     BMI ERROR
0380     CLC
0390     RTS
0400 ERROR SEC
0410     RTS
```
