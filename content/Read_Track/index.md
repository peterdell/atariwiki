---
title: Read Track
---
# Speedy 1050 example -- read tack  
  
```
0100 ;***********************************
0110 ;* Demonstration fuer Kommando $62 *
0120 ;*     'Read Track' - Befehl       *
0130 ;***********************************
0140 ;
0150 TRKDAT = $5000  ; Adresse der kompletten Trackdaten
0160 TRKLEN = $0900  ; $900 SD, $D00 MD, $1200 DD
0170 SECTOR = 1      ; Anfangssektor eines Tracks
0180 ;
0190     .OPT NO LIST
0200     .OPT OBJ
0210     *=  $4000
0220 ;
0230     LDA #$31    ; Bus ID
0240     STA $0300
0250     LDA #1      ; Laufwerks Nummer = 1
0260     STA $0301
0270     LDA #$62    ; Kommando $62
0280     STA $0302
0290     LDA #$40    ; Status fuer Daten lesen
0300     STA $0303
0310     LDA # <TRKDAT ; Trackdaten Low Byte
0320     STA $0304
0330     LDA # >TRKDAT ; Trackdaten High Byte
0340     STA $0305
0350     LDA #7      ; Wert fuer Timeout = 7 Sekunden
0360     STA $0306
0370     LDA # <TRKLEN ; Tracklaenge Low Byte
0380     STA $0308
0390     LDA # >TRKLEN ; Tracklaenge High Byte
0400     STA $0309
0410     LDA # <SECTOR
0420     STA $030A
0430     LDA # >SECTOR
0440     STA $030B
0450     JSR $E459   ; Einsprung der SIO-Routine im OS
0460     BMI ERROR
0470     CLC
0480     RTS
0490 ERROR SEC
0500     RTS

```
