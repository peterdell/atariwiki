# Speedy 1050 Drive / Display configuration example  
  
```
0100 ;*************************************
0110 ;*  Demonstration fuer Kommando $44  *
0120 ;*************************************
0130 ;
0140     .OPT NO LIST
0150     .OPT OBJ
0160     *=  $4000
0170 ;
0180     LDA #$31    ; Bus ID
0190     STA $0300
0200     LDA #1      ; Laufwerks Nummer = 1
0210     STA $0301
0220     LDA #$44    ; Kommando $44
0230     STA $0302
0240     LDA #0      ; Status fuer keine Daten senden oder empfangen
0250     STA $0303
0260     LDA #7      ; Wert fuer Timeout = 7 Sekunden
0270     STA $0306
0280     LDA #$20    ; Bit 5 fuer Format ohne Verify
0290     STA $030A
0300     JSR $E459   ; Einsprung der SIO-Routine im OS
0310     BMI ERROR
0320     CLC
0330     RTS
0340 ERROR SEC
0350     RTS
```
