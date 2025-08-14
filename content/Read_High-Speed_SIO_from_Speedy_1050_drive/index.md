# Speeday 1050 example -- read high speed SIO routine from drive  
  
```
0100 ;****************************************
0110 ;*  Lesen der SIO-Routine vom Laufwerk  *
0120 ;****************************************
0130 ;
0140 ADR =   $5000   ; Adresse fuer die SIO-Routine
0150 ;
0160     .OPT NO LIST
0170     .OPT OBJ
0180     *=  $4000
0190 ;
0200     LDA #$31    ; Bus ID
0210     STA $0300
0220     LDA #1      ; Laufwerks Nummer = 1
0230     STA $0301
0240     LDA #$68    ; Kommando $68
0250     STA $0302
0260     LDA #$40    ; Status fuer Daten lesen
0270     STA $0303
0280     LDA #8
0290     STA $0304   ; Adresse fuer Laengenbyte Low
0300     STA $0306   ; Wert fuer Timeout = 8 Sekunden
0310     LDA #3
0320     STA $0305   ; Adresse fuer Laengenbyte High
0330     LDA #2
0340     STA $0308   ; 2 Bytes lesen
0350     LDA #0
0360     STA $0309
0370     JSR $E459   ; Einsprung der SIO-Routine im OS
0380     BMI ERROR
0390     INC $0302   ; Kommando $69
0400     LDA # <ADR
0410     STA $0304   ; Target Adresse der SIO-Routine Low
0420     STA $030A   ; Original Adresse der SIO-Routine Low
0430     LDA # >ADR
0440     STA $0305   ; Target Adresse der SIO-Routine High
0450     STA $030B   ; Original Adresse der SIO-Routine High
0460     LDA #$40
0470     STA $0303   ; Status fuer Daten lesen
0480     JSR $E459   ; Einsprung der SIO-Routine im OS
0490     BMI ERROR
0500     CLC
0510     RTS
0520 ERROR SEC
0530     RTS


```
