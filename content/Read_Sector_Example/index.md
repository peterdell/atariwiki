# Speedy Read Sector example  
  
```
0100 ;***************************************
0110 ;*  Demonstration 1 fuer Kommando $52  *
0120 ;***************************************
0130 ;
0140 DATBUF = $5000
0150 SECNUM = 1
0160 ;
0170     .OPT NO LIST
0180     .OPT OBJ
0190     *=  $4000
0200 ;
0210     LDA #$31    ; Bus ID
0220     STA $0300
0230     LDA #1      ; Laufwerks Nummer = 1
0240     STA $0301
0250     LDA #$52    ; Kommando $52
0260     STA $0302
0270     LDA #$40    ; Status fuer Daten lesen
0280     STA $0303
0290     LDA # <DATBUF ; Adresse fuer Datenbuffer Low
0300     STA $0304
0310     LDA # >DATBUF ; Adresse fuer Datenbuffer High
0320     STA $0305
0330     LDA #7      ; Wert fuer Timeout = 7 Sekunden
0340     STA $0306
0350     LDA #$80    ; 128 Bytes (in SD+MD) schreiben
0360     STA $0308
0370     LDA #0
0380     STA $0309
0390     LDA # <SECNUM ; Sector Nummer Low Byte
0400     STA $030A
0410     LDA # >SECNUM ; Sector Nummer High Byte
0420     STA $030B
0430     JSR $E459   ; Einsprung in die SIO-Routine im OS
0440     BMI ERROR
0450     CLS
0460     RTS
0470 ERROR SEC
0480     RTS
```
  
```
0100 ;***************************************
0110 ;*  Demonstration 2 fuer Kommando $52  *
0120 ;***************************************
0130 ;
0140 PRGBUF = $8000
0150 DATBUF = $5000
0160 ;
0170     .OPT NO LIST
0180     .OPT OBJ
0190     *=  $4000
0200 ;
0210     LDA #$31    ; Bus ID
0220     STA $0300
0230     LDA #1      ; Laufwerks Nummer 1
0240     STA $0301
0250     LDA #$52    ; Kommando $52
0260     STA $0302
0270     LDA #$40    ; Status fuer Daten lesen
0280     STA $0303
0290     LDA # <DATBUF ; Adresse fuer Datenbuffer Low
0300     STA $0304
0310     LDA # >DATBUF ; Adresse fuer Datenbuffer High
0320     STA $0305
0330     LDA #7      ; Wert fuer Timeout = 7 Sekunden
0340     STA $0306
0350     LDA #$80    ; 128 Bytes (in SD+MD) schreiben
0360     STA $0308
0370     LDA #0
0380     STA $0309
0390     LDA # <PRGBUF ; Adresse fuer Programmbuffer Low
0400     STA $030A
0410     LDA # >PRGBUF ; Adresse fuer Programmbuffer High
0420     STA $030B
0430     JSR $E459   ; Einsprung der SIO-Routine im OS
0440     BMI ERROR
0450     CLC
0460     RTS
0470 ERROR SEC
0480     RTS
```
