# ASCII - Entering ASCII Literals inline  
  
Vierte Dimension 1/1985, by DR. med.dent. Greiner  
  
(translation pending)  
  
Bei der Programmierung von Menüs braucht man haufig den ASCII-Wert eines Zeichens. Anstatt nun jedesmal In der Tabelle nachzusehen und dann einen nichtssagenden Zahlenwert ins Programm zu schreiben, ist es sinnvoller, einen Befehl zu definieren, der ein nachfolgendes Zeichen automatisch in ASCII umgerechnet auf den Stack legt.  
  
Wenn dieser Befehl ASCII heißt, dann schreibt man also ASCII A statt 65 . Die folgende Definition bewerkstelligt das:  
```
: ASCII BL WORD HERE 1+ C@ [COMPILE] LITERAL ; IMMEDIATE
```
Das Wort holt das nächste Wort vom Input-Stream, pickt den ersten Buchstaben heraus und legt es auf den Stack. Wenn ASCII während des Kompilierens aufgerufen wird ( es ist ja ein IMMEDIATE-Wort, d.h. es wird auch während  
des Kompilierens ausgeführt!), dann wird der auf dern Stack befindliche Wert als Literal in die gerade übersetzte Definition geschrieben. Der Effekt für die kompilierte Defi­nition ist genau derselbe, als wenn man den ASCII-Wert direkt in den Quelltext schreiben würde.  
