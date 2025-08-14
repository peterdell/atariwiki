||ADR||HEXADR||NAME||Description||shadow||OS  
|0,1|$0000,$0001|LINZBS| | |A  
  
Es scheint, als ob diese Adresse genutzt wird, um den VBLANK Timer Wert zu speichern.  
  
Ein Metronom-Programm aus dem De Re Atari (Seite 123) nutzt diese Speicherzelle:  
%%prettify  
```
5 ? " ":REM Bildschirm löschen
6 REM Routine zum Setzen einer Metronom-Rate.
7 REM Von M. Ekbers für Carla.
10 X=10:FOR I=l TO 2 STEP 0
20 TOP=l0:FOR J=l TO TOP:NEXT J:REM Verzögerungs-Schleife
50 IF STICK(0)=l3 THEN X=X+1:REM Nach oben = schneller
51 IF STICK (0)=14 THEN X=X-1:REM Nach unten = langsamer
52 IF X<l THEN X=1:REM X darf niemals kleiner als 1 oder
53 IF X>255 THEN X=255:REM grösser als 255 sein.
54 REM
56 ?"";INT(3600/X);" Schläge pro Minute "
60 POKE 0,X:REM In Speicherstelle $0000 steht die Rate
70 NEXT I:REM für die folgende Assembler-Routine.
-------------------------------------------------------------
40 *=$600
50 ; Metronom-Routine...benutzt $0000 zum Uebersetzen d. Rate.
60 ;
70 AUDF1 = $D200 Audio Frequenz-Register
80 AUDC1 = $D201 Audio Kontroll-Register
90 FREG = $08 AUDF1-Wert
0100 VOLUME = $AF WERT VON AUDC1
0110 OFF = $A0Lautstaerke ausschalten
0120 SETVBV = $E45C Routine zum Setzen des Timer-Wertes
0130 CDTMA2 = $0228 Vektor von Timer 2
0140 ZTIMER = $0000 VBLANK-Wert des Timers in Zero-Page
0150 ;
0160 START LDA #10
0170 STA ZTIMER
0180 INIT
0190 ; Setzen des Timer-Vektors
0200 ;
0210 LDA #CNTINT&255
0220 STA CDTMA2
0230 LDA #CNTINT/256
0240 STA CDTMA2+1
0250 ;
0260 ; Setzen dem Timers nach dem Voktor
0270 ;
0290 LDY ZTIMER Setzen von Timer 2 auf Zaehler
0290 JSR SETIME
0300 RTS
0310 ;
0320 ;
0330 ;
0340 CNTINT
0350 ;
0360 ; Bereitmachen das Audio-Kanals für "Klick"-
0370 ; Geraeusch
0380 LDA #VOLUME
0390 STA AUDC1
0400 LDA #FREQ
0410 STA AUDF1
0420 LDY #$FF
0430 DELAY
0440 DEY
0450 BNE DELAY
0460 STY AUDC1
0470 JMP INIT
0480 ;
0490 ; Unterroutine zum Setzen das Timers
0500 ;
0510 SETIME
0520 LDX #0 Niemals 256 VBLANKs
0530 LDA #2 Setzen von Timer 2
0540 JSR SETVBV System-Routine zum Setzen
0550 RTS der Timer
0560 *=$2E2
0570 .WORD START
0580 .END
```
/%  
