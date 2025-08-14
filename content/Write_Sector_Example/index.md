# Write Sector example  
  
```
0100 ;***************************************
0110 ;*  Demonstration 1 fuer Kommando $50  *
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
0250     LDA #$50    ; Kommando $50
0260     STA $0302
0270     LDA #$80    ; Status fuer Daten schreiben
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
0430     JSR $E459   ; Einsprung der SIO-Routine im OS
0440     BMI ERROR
0450     CLC
0460     RTS
0470 ERROR SEC
0480     RTS
```
  
```
0100 ;***************************************
0110 ;*  Demonstration 2 fuer Kommando $50  *
0120 ;***************************************
0130 ;
0140 PRGBUF = $8000
0150 ;
0160     .OPT NO LIST
0170     .OPT OBJ
0180     *=  $4000
0190 ;
0200     LDA #$31    ; Bus ID
0210     STA $0300
0220     LDA #1      ; Laufwerks Nummer = 1
0230     STA $0301
0240     LDA #$50    ; Kommando $50 Sector ohne Verify schreiben
0250     STA $0302
0260     LDA #$80    ; Status fuer Daten schreiben
0270     STA $0303
0280     LDA # <DATBUF ; Adresse fuer Datenbuffer Low
0290     STA $0304
0300     LDA # >DATBUF ; Adresse fuer Datenbuffer High
0310     STA $0305
0320     LDA #7      ; Wert fuer Timeout = 7 Sekunden
0330     STA $0306
0340     LDA #$80    ; 128 Bytes (in SD+MD) schreiben
0350     STA $0308
0360     LDA #0
0370     STA $0309
0380     LDA # <PRGBUF ; Adresse fuer Programmbuffer Low
0390     STA $030A
0400     LDA # >PRGBUF ; Adresse fuer Programmbuffer High
0410     STA $030B
0420     JSR $E459   ; Einsprung der SIO-Routine im OS
0430     BMI ERROR
0440     CLC
0450     RTS
0460 ERROR SEC
0470     RTS
0480 ;
0490 DATBUF
0500     LDA #$FA
0510     JMP $FFA5   ; HEXOUT
```
