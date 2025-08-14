# Recurse - calling a word recursively  
  
Vierte Dimension 1/1985 by DR. med.dent. Greiner  
  
(translation pending)  
  
In FORTH sind Rekursionen standardmäßig nicht mög­lich, weil ein Wort vom Compiler erst erkannt wird, wenn es fertig kompiliert ist. Manche Problemstellungen lassen sich aber nun mal besser rekursiv darstellen. Diesem Mangel kann jedoch leicht abgeholfen werden:  
```
: RECURSE ( ruft laufende Definition rekursiv auf ) 
  ?COMP LATEST PFA CFA , ; IMMEDIATE
```
( Rekursion darf auf 6502-Systemen nicht ohne besondere Beachtung des Returnstacks angewendet warden. )  
Der Befehl RECURSE bewirkt also einen Aufruf der Colon­ definition, in der er auftritt. Er macht dies, indem er die Codefield-Adresse der laufenden Definition als Aufruf an die gerade aktuelle Speicherstelle schreibt. Vorher wird mit ?COMP noch geprüft, ob gerade kompiliert wird — au­ßerhalb einer Colondefinition ergäbe RECURSE nämlich keinen Sinn.  
  
RECURSE kann bedenkenlos auch innerhalb von Kontrollstrukturen ( IF THEN, Schleifen, CASE etc,) verwendet  
werden — auf eines sollte man jedoch achten: Die Schachtelungstiefe darf nicht beliebig groß werden, da früher oder später (je nach Implementation) einer der beiden Stacks überläuft. Aber zehn bis zwanzig Ebenen dürften allemal drin sein, und mehr braucht man höchst sel­ten.  
  
Um gleich mal die Verwendung von RECURSE zu demonstrieren, folgende Definition:  
```
: DEZ ( dezimalzahl — 16-bit Integer )
BASE @ /MOD DUP IF RECURSE 10 * + ELSE DROP THEN ;
```
DEZ bewirkt, daß eine 16-bit Zahl auf dem Stack so umge­rechnet wird, als ob man sie dezimal eingegeben hätte ­ gleichgültig, unter welcher Zahlenbasis man sie tatsäch­lich eingegeben hat. Wozu das? Nun: Ich fand es immer lästig, daß z.B, bei 10 LIST mal Screen 10 und mal Screen 16 erscheint — je nachdem, ob man dezimal oder in hex arbeitet. Die Definition  
```
: LIST DEZ LIST ; 
```
löst das Problem. Jetzt kann ich mich darauf verlassen, daß auch wirklich die (dezimale) Screen­ nummer kommt, die ich haben will — egal mit welcher Za­hlenbasis ich gerade arbeite.  
