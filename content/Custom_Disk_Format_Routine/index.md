  
  
# Custom Disk Format Routine  
  
```
10       .OPT NO LIST
20 ;
30 ; Neuer Befehl F
40 ; Formatiert eine Spur mit selbst
50 ; definiertem Format
60 ;
70 DAUX  =   $82
80 SPUR  =   $8D
90 ;
0100 PORTA = $0280
0110 BEFSTA = $0400
0120 DATEN = $0403
0130 ;
0140 CONRES = $F362
0150 MOTAN = $F239
0160 KOPFSPUR = $F2EC
0170 SENDCPL = $F48F
0180 SENDERR = $F494
0190 ;
0200 PUF =   $8000   ; Format-Daten
0210 STAB =  PUF     ; Sektor-Nummer
0220 ETAB =  PUF+30  ; Fehler-Nummer
0230 LTAB =  PUF+60  ; Sektor-Laenge
0240 FTAB =  PUF+90  ; Sektor-Inhalt
0250 GP1 =   PUF+120 ; POST INDEX
0260 GP2 =   PUF+121 ; PRE ADDRESS
0270 GP3 =   PUF+122 ; POST ADDRESS
0280 GP4 =   PUF+123 ; POST DATA
0290 DEN =   PUF+124 ; Sng oder Enh
0300 ANZ =   PUF+125 ; Anzahl der Sek.
0310 ;
0320 ; Schreibe Akku auf Diskette
0330 ;
0340     .MACRO WRT1 
0350 ?W1 BIT PORTA
0360     BVS *+5     ; Fehler ?
0370     JMP SENDERR
0380     BPL ?W1     ; Data Request ?
0390     STA DATEN
0400     .ENDM 
0410 ;
0420 ; Schreibe X-mal Akku auf Diskette
0430 ;
0440     .MACRO WRT 
0450 ?W2 BIT PORTA
0460     BVS *+5     ; Fehler ?
0470     JMP SENDERR
0480     BPL ?W2     ; Data Request ?
0490     STA DATEN
0500     DEX 
0510     BNE ?W2
0520     .ENDM 
0530 ;
0540     *=  $9000
0550 ;
0560     LDA DEN
0570     CMP #'S
0580     BNE ED
0590     LDA PORTA   ; Aktiviere FM
0600     ORA #$20    ; Modus
0610     BNE ?L0
0620 ED  LDA PORTA   ; Aktiviere MFM
0630     AND #$DF    ; Modus
0640 ?L0 STA PORTA
0650 ;
0660     LDY #29     ; Der Sektorinhalt
0670 ?L1 LDA FTAB,Y  ; muss wegen dem
0680     EOR #$FF    ; "inverted Data
0690     STA FTAB,Y  ; Bus" noch
0700     DEY         ; "inverted"
0710     BPL ?L1     ; werden
0720 ;
0730     JSR CONRES  ; FDC reset
0740     BIT BEFSTA
0750     BMI ERR     ; Write Protect
0760     BVS ERR     ; Not ready
0770     JSR MOTAN   ; Motor anschalten
0780     LDA DAUX    ; Schreib-/Lese-
0790     STA SPUR    ; Kopf auf Spur
0800     JSR KOPFSPUR ; ruecken
0810     LDA #15     ; Timer fuer 1.
0820     STA $029F   ; Indeximp. setzen
0830     LDA #$F0    ; WRITE-TRACK
0840     STA BEFSTA  ; Kommando an FDC
0850 ;
0860     LDY #0      ; Pointer auf 0
0870     LDA DEN
0880     CMP #'S
0890     BEQ SNG
0900     JMP ENH
0910 ;
0920 ERR JMP SENDERR
0930 ;
0940 SNG BIT PORTA   ; Formatiere in
0950     BPL SNG     ; Single Density
0960     LDA #0
0970     STA DATEN
0980 ?S0 BIT PORTA
0990     BPL ?S0
1000     STA DATEN
1010     LDA #$D2    ; Timer auf 210
1020     STA $029F   ; ms setzen
1030 ;
1040     LDX #$AC    ; $ac Gapbytes
1050     LDA #0
1060      WRT  
1070     LDA #$FC    ; INDEX MARK
1080      WRT1  
1090     LDX GP1     ; POST INDEX
1100     LDA #0
1110      WRT  
1120 ;
1130 ?S1 LDX GP2     ; PRE ADDRESS
1140     LDA #0
1150      WRT  
1160 ;
1170 ; Formatiere einen Header
1180 ;
1190     LDA #$FE    ; ADDRESS MARK
1200      WRT1  
1210     LDA SPUR    ; Spur-Nummer
1220      WRT1  
1230     LDA #0      ; Seiten-Nummer
1240      WRT1  
1250     LDA STAB,Y  ; Sektor-Nummer
1260      WRT1
1270     LDA #0      ; Sektor-Laenge
1280      WRT1  
1290     LDX ETAB,Y  ; Die Pruefsummen-
1300     LDA ETB2,X  ; bytes dienen zur
1310      WRT1       ; Fehlererzeugung
1320 ;
1330     LDX GP3     ; POST ADDRESS
1340     LDA #0
1350      WRT  
1360 ;
1370 ; Formatiere ein Datenfeld
1380 ;
1390     LDX ETAB,Y  ; DATA ADDRESS
1400     LDA ETB1,X  ; dient zur
1410      WRT1       ; Fehlererzeugung
1420     LDX LTAB,Y  ; Sektor-Laenge
1430     LDA FTAB,Y  ; Sektor-Inhalt
1440      WRT  
1450     LDX ETAB,Y  ; Die Pruefsummen-
1460     LDA ETB3,X  ; bytes dienen zur
1470      WRT1       ; Fehlererzeugung
1480     LDX GP4     ; POST DATA
1490     LDA #0
1500      WRT  
1510     INY         ; Naechster Sektor
1520     CPY ANZ     ; Fertig ?
1530     BCS *+5
1540     JMP ?S1
1550     LDX #0
1560     JMP FEN
1570 ;
1580 ENH BIT PORTA   ; Formatiere in
1590     BPL ENH     ; Enhanced Density
1600     LDA #$4E
1610     STA DATEN
1620 ?E0 BIT PORTA
1630     BPL ?E0
1640     STA DATEN
1650     LDA #$D2    ; Timer auf 210 ms
1660     STA $029F   ; setzen
1670 ;
1680     LDX #$90    ; $190 Gapbytes
1690     LDA #$4E
1700      WRT  
1710     LDX #0
1720     LDA #$4E
1730      WRT  
1740     LDX #$0C    ; $c   Gapbytes
1750     LDA #0
1760      WRT  
1770     LDX #3      ; $c2 ohne Takt
1780     LDA #$F6
1790      WRT  
1800     LDA #$FC    ; INDEX MARK
1810      WRT1  
1820     LDX GP1     ; POST INDEX
1830     LDA #$4E
1840      WRT  
1850 ;
1860 ?E1 LDX GP2     ; PRE ADDRESS
1870     LDA #0
1880      WRT  
1890 ;
1900 ; Formatiere einen Header
1910 ;
1920     LDX #3      ; $a1 ohne Takt
1930     LDA #$F5
1940      WRT  
1950     LDA #$FE    ; ADDRESS MARK
1960      WRT1
1970     LDA SPUR    ; Spur-Nummer
1980      WRT1  
1990     LDA #0      ; Seiten-Nummer
2000      WRT1  
2010     LDA STAB,Y  ; Sektor-Nummer
2020      WRT1  
2030     LDA #0      ; Sektor-Laenge
2040      WRT1  
2050     LDX ETAB,Y  ; Die Pruefsummen-
2060     LDA ETB2,X  ; bytes dienen zur
2070      WRT1       ; Fehlererzeugung
2080 ;
2090     LDX GP3     ; POST ADDRESS
2100     LDA #$4E
2110      WRT  
2120 ;
2130 ; Formatiere ein Datenfeld
2140 ;
2150     LDX #3      ; $a1 ohne Takt
2160     LDA #$F5
2170      WRT  
2180     LDX ETAB,Y  ; DATA ADDRESS
2190     LDA ETB1,X  ; dient zur
2200      WRT1       ; Fehlererzeugung
2210     LDX LTAB,Y  ; Sektor-Laenge
2220     LDA FTAB,Y  ; Sektor-Inhalt
2230      WRT  
2240     LDX ETAB,Y  ; Die Pruefsummen-
2250     LDA ETB3,X  ; bytes dienen zur
2260      WRT1       ; Fehlererzeugung
2270     LDX GP4     ; POST DATA
2280     LDA #$4E
2290      WRT  
2300     INY         ; Naechster Sektor
2310     CPY ANZ     ; Fertig ?
2320     BCS *+5
2330     JMP ?E1
2340     LDX #$4E
2350 ;
2360 FEN LDA #1
2370 ?F1 AND BEFSTA  ; FDC busy ?
2380     BEQ ?F2     ; nicht mehr busy
2390     BIT PORTA   ; Data Request ?
2400     BPL ?F1     ; Nein
2410     STX DATEN
2420     BMI ?F1     ; Immer
2430 ?F2 LDA $0296
2440     LDA BEFSTA
2450     PHA         ; Save FDC-Status
2460     JSR CONRES  ; FDC reset
2470     PLA 
2480     AND #4      ; Datenverlust ?
2490     BNE *+5     ; Ja
2500     JMP SENDCPL
2510     JMP SENDERR
2520 ;
2530 ETB1 .BYTE $FB,$F8,$F8,$FB,$00,$FB
2540 ETB2 .BYTE $F7,$F7,$F7,$00,$F7,$F7
2550 ETB3 .BYTE $F7,$00,$F7,$F7,$F7,$00
```
  
