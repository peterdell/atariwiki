Heute kommen wir zu einem Thema, dem es keine direkte Ensprechung in BASIC Welt gibt: Erstellen von ausführbaren COM-Dateien. Basic (und auch Turbo-Basic) erlauben nicht das Erstellen von direkt ausführbaren Maschinenprogrammen (COM-Programme). Hierzu musste man kommerzielle BASIC-Compiler kaufen, die dann mehr schlecht als recht funktionieren.  
  
Unter Forth ist dies schon möglich.  
  
Zuerst schreiben wir ein kleines "Hallo-Welt" Programm, als Demonstration:  
  
```
: HALLO-WELT (-- )
  CR ." Hallo Welt. Hier ist volksForth" CR
  KEY DROP
  BYE ;
```
  
  
Erklärung: HALLO-WELT ist unser neues Forth Wort. Das Forth-Wort "CR" erzeugt einen Zeilenvorschub auf dem Bildschirm (Carriage Return)  
  
Das Wort ." gibt den Text bis zum folgenden Anführungsstrichen aus (Leerzeichen hinter den ." beachten!)  
  
"KEY DROP" wartet auf einen Tastendruck, der ASCII Wert der Taste wird auf den Stapel gelegt un per DROP sofort wieder "weggeworfen".  
  
"BYE" beendet Forth und springt (nein, nicht in den Selbsttest) zurück in das DOS.  
  
Nun müssen wir Forth sagen, das unser neues Wort "HALLO-WELT" nach dem Start unseres zu speichernden Programmes direkt ausgeführt werden soll. Dies geschied, indem wir die Ausführungsaddresse des Wortes HALLO-WELT dem "verzögerten" (deferred) Wort 'COLD zuweisen ('COLD = ausgesprochen "tick cold"). Die Ausführungaddresse unseres neuen Wortes holen wir uns mit dem Wort ' (tick), die Zuweisung geschied mit dem Wort "IS":  
  
```
' HALLO-WELT IS 'COLD

SAVE

SAVE-SYSTEM D:HALLO.COM
```
  
Das Wort "SAVE" sichert (im Hauptspeicher) unsere Erweiterungen zum Forth (die können danach nicht mehr im Speicher gelöscht werden), SAVE-SYSTEM <dateiname> speichert dann das Programm als COM-Datei ab.  
  
SAVE-SYSTEM muss ggf. aus der Datei SAVESYS.F nachgeladen werden:  
  
```
INCLUDE" D:SAVESYS.F"
```
  
Warum ist das "HELLO.COM" Programm so groß? Weil SAVE-SYSTEM immer das gesamte Forth System speichert, inklusive aller Worte, die schon vorher im Forth definiert waren. Später werde ich Euch zeigen wie wir das Programm schlanker bekommen.  
