# Speedy 1050 example -- install a custom command  
  
```
0100 ;***************************************
0110 ;*  Demonstration 1 fuer Kommando $41  *
0120 ;*      Kommando $54 installieren      *
0130 ;***************************************
0140 ;
0150     .OPT NO LIST
0160     .OPT OBJ
0170     *=  $4000
0180 ;
0190     LDA #$31    ; Bus ID
0200     STA $0300
0210     LDA #1      ; Laufwerks Nummer = 1
0220     STA $0301
0230     LDA #$41    ; Kommando $41
0240     STA $0302
0250     LDA #$80    ; Status fuer Daten schreiben
0260     STA $0303
0270     LDA # <COMBUF ; Adresse fuer Kommandobuffer Low
0280     STA $0304
0290     LDA # >COMBUF ; Adresse fuer Kommandobuffer High
0300     STA $0305
0310     LDA #7      ; Wert fuer Timeout = 7 Sekunden
0320     STA $0306
0330     LDA #3      ; 3 Bytes schreiben
0340     STA $0308
0350     LDA #0
0360     STA $0309
0370     JSR $E459   ; Einsprung der SIO-Routine im OS
0380     BMI ERROR
0390     CLC
0400     RTS
0410 ERROR SEC
0420     RTS
0430 COMBUF .BYTE $54 ; Kommando $54
0440     .WORD $8000 ; Einsprung $8000

```
