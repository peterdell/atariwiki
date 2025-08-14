# Working with files (translation pending)  
  
Arbeiten mit Dateien. Um in BASIC Dateien zu lesen oder schreiben, benutzen wir den Befehl OPEN. Beispiel, Oeffnen einer Datei zum Lesen und Einlesen des ersten Satzes:  
  
```
DIM A$(100)
OPEN #1,4,0,"D:DATEI.TXT"
INPUT #1,A$
close #1
```
  
In BASIC geben wir mit dem zweiten Wert im OPEN Befehl an, ob die Datei zum Lesen (4) oder Schreiben (8) oder zum Lesen/Schreiben (12) geoeffnet wird. In Forth haben wir hierzu extra Woerter:  
  
- R/O = Read Only  
- W/O = Write Only  
- R/W = Read Write  
  
```
VARIABLE filechannel
CREATE BUFFER 200 ALLOT

S" D:DATEI.TXT" R/O OPEN-FILE  
   ABORT" Datei konnte nicht geoeffent werden"
filechannel !
BUFFER filechannel @ READ-LINE 
  ABORT" Datei konnte nicht gelesen werden"
filechannel @ CLOSE-FILE
  ABORT" Datei konnte nicht geschlossen werden"
```
  
Bei OPEN-FILE koennen wir nicht angeben, welcher Dateikanal benutzt wird. Forth sucht den naechst freien. Diesen speichern wir in der Variable "filechannel".  
  
FILE-OPEN liefert ein Flag zurueck, welches angibt ob die DAtei geoeffnet werden konnte. ABORT" fragt ein Flag ab und wenn ein Fehler aufgetreten ist, wird der Text hinter ABORT" ausgegeben.  
