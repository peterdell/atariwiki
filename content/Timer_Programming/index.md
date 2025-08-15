---
title: Timer Programming
---
# ACTION! Timer Programming  
  
```
; PROGRAM : EASY INTERUPT
    
; 1. KEINE ACTION! PROC BENUTZEN
;    ALSO : KEIN PRINT, U.S.W.

; 2. PARAMETERUEBERGABE MIT NICHT 
;    MEHR ALS 3 BYTES

; 3. KEINE MULTIPLIKATION,DIVISION

; 4. SCHIEBEOPERATION RSH/LSH NUR
;    NOCH BEI BYTE ZAHLEN


BYTE COL4=712,MARGIN=82,CURSOR=752,
     RAINMEM=203,RAINMEM2=[0],
     WAITSYNC=$D40A,HARDCOL1=53271,
     KEYCODE=764,COL2=710,KEY,
     FRAME=[0],Effekt,TIMERSPEED=[1]

CARD TIMER2_COUNTER=538,
     TIMER2_VEKTOR=552

BYTE TIMER2_COUNTER_LO=538 

CARD SCREENADR=88
BYTE POINTER SCREEN 
BYTE MOVEFLAG=[0]

PROC INCCOL()
   
   RAINMEM=RAINMEM2 ; FARBEN FUER 
                    ; RAINBOW EFFEKT
                    ; NEU SETZEN UND
   RAINMEM2==+1     ; WEITERZAEHLEN

  IF FRAME>10 AND FRAME<20 THEN 

    COL4=$20        ; RAHMEN-FLASH
    FRAME==+1 IF FRAME =19 THEN FRAME=0 FI
   ELSE 
    COL4=$10
    FRAME==+1
  FI
; AB HIER BEWEGUNG DES "Balls"

   SCREEN^=0        ; ALTE POSITION 
                    ; LOESCHEN
                      

IF MOVEFLAG=0 THEN    
   SCREEN==+1
   IF SCREEN=SCREENADR+39 THEN MOVEFLAG==+1 FI
FI

IF MOVEFLAG=1 THEN
   SCREEN==+40
   IF SCREEN>SCREENADR+919 THEN MOVEFLAG==+1 FI
FI

IF MOVEFLAG=2 THEN
   SCREEN==-1
   IF SCREEN<SCREENADR+921 THEN MOVEFLAG==+1 FI
FI

IF MOVEFLAG=3 THEN
   SCREEN==-40
   IF SCREEN=SCREENADR THEN MOVEFLAG=0 FI
FI


   SCREEN^=84        ; UND SETZEN

 TIMER2_COUNTER_LO=TIMERSPEED
                     ; COUNTER NEU
                     ; SETZEN, DAMIT
                     ; DER TIMER IM
                     ; NAECHSTEN VBI
                     ; AUCH AUSGE-
                     ; FUEHRT WIRD!
RETURN



PROC INIT_TIMER() 

 TIMER2_COUNTER=0

 TIMER2_VEKTOR=INCCOL

 TIMER2_COUNTER_LO=1
 
RETURN

PROC WAIT_FOR_KEY()
IF EFFEKT=0 THEN
 DO
 WAITSYNC=1 HARDCOL1=RAINMEM
 RAINMEM==+1 
 UNTIL KEYCODE<>255
 OD
ELSE
 DO
 WAITSYNC=1 
 UNTIL KEYCODE<>255
 OD
FI
RETURN

PROC INFO_WINDOW()
 POSITION(2,2)
 MARGIN=2
 PRINTE("----------------------")
 PRINTE("|  der Ball wird im  |")
 PRINTE("|    Timer bewegt    |")
 PRINTE("| ------------------ |")
 PRINTE("|Fuer einfache Timer-|")
 PRINTE("|programmierung  in  |")
 PRINTE("|Action! bitte fol-  |")
 PRINTE("|gendes beachten:    |")
 PRINTE("|                    |")
 PRINTE("|1.Keine Action PROCs|")
 PRINTE("|  benutzen          |")
 PRINTE("|                    |")
 PRINTE("| weiter mit <Return>|")
 PRINTE("----------------------")

WAIT_FOR_KEY() KEYCODE=255

 POSITION(19,1)
 MARGIN=19
 PRINTE("----------------------")
 PRINTE("|Parameteruebergabe|")
 PRINTE("|nur mit maximal 3 |")
 PRINTE("|Byte (oder 1 Card |")
 PRINTE("|und 1 Byte).      |")
 PRINTE("|Intern gesehen    |")
 PRINTE("|werden die 3 Bytes|")
 PRINTE("|in die 6502 Regis-|")
 PRINTE("|ter gespeichert.  |")
 PRINTE("|alle anderen in   |")
 PRINTE("|Zero-Page Register|")
 PRINTE("|Das wuerde aber   |")
 PRINTE("|Konflikte mit dem |")
 PRINTE("|jeweiligen Haupt- |")
 PRINTE("|programm zur Folge|")
 PRINTE("|haben.            |")
 PRINTE("|                  |")
 PRINTE("|weiter mit<Return>|")
 PRINTE("----------------------")
WAIT_FOR_KEY() KEYCODE=255
 POSITION(5,13)
 MARGIN=5 
 PRINTE("------------------------")
 PRINTE("|Keine Multiplikationen|")
 PRINTE("|und Divisionen !!!    |")
 PRINTE("|                      |")
 PRINTE("|  weiter mit <Return> |")
 PRINTE("------------------------")
WAIT_FOR_KEY() KEYCODE=255
 POSITION(21,10)
 MARGIN=21
 PRINTE("----------------")
 PRINTE("|Schieben (RSH |")
 PRINTE("|und LSH) nur  |")
 PRINTE("|noch bei BYTE |")
 PRINTE("|Werten !!!    |")
 PRINTE("|              |")
 PRINTE("|   <Return>   |")
 PRINTE("----------------")
WAIT_FOR_KEY() KEYCODE=255

return

proc newspeed()
 POSITION(12,9)
 MARGIN=12
 PRINTE("----------------")
 PRINTE("|Bitte Neue Ge-|")
 PRINTE("|schwindigkeit |")
 PRINTE("|eingeben.     |")
 PRINTE("|Tasten 1 - 9  |")
 PRINTE("----------------")
WAIT_FOR_KEY() 

 key=getd(1) key==-48

 if key>=1 and KEY<=9 then
    timerspeed=key
    IF KEY>2 THEN EFFEKT=1
     ELSE EFFEKT=0
    FI
 fi 
RETURN

PROC WARMSTART=$E474()
RETURN

proc QUIT()
 POSITION(12,9)
 MARGIN=12
 PRINTE("----------------")
 PRINTE("|QUIT fuehrt   |")
 PRINTE("|Warmstart aus |")
 PRINTE("|(System Reset)|")
 PRINTE("|ausfuehren ?? |")
 PRINTE("|    (J/N)     |")
 PRINTE("----------------")
WAIT_FOR_KEY() 
 IF KEYCODE=1 THEN 
 KEYCODE=255
 WARMSTART() FI
 KEYCODE=255

RETURN


PROC HAUPTPROGRAMM()
 EFFEKT=0
 CLOSE(1) OPEN(1,"K:",4,0)
 GRAPHICS(0) COL2=0

 SCREEN=SCREENADR ;=SCREEN=PEEKC(88)

 INIT_TIMER()
DO
 CURSOR=1
 POSITION(9,7)
 MARGIN=9
 PRINTE("----------------------")
 PRINTE("| Action! User Group |")
 PRINTE("|                    |")
 PRINTE("|   'Easy Timers!'   |")
 PRINTE("|                    |")
 PRINTE("| I>nformation       |")
 PRINTE("| G>eschwindigkeit   |")
 PRINTE("| E>ffekt            |")
 PRINTE("| Q>uit              |")
 PRINTE("----------------------")

 WAIT_FOR_KEY()
 KEY=GETD(1)
 IF KEY='I OR KEY='i THEN INFO_WINDOW() FI
 IF KEY='E OR KEY='e THEN effekt==XOR 255 FI
 IF KEY='G OR KEY='g THEN newspeed() FI
 IF KEY='Q OR KEY='q THEN QUIT() FI
OD
RETURN
```
