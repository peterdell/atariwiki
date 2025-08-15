---
title: Der XIO Befehl fuer Grafikoperationen
---
# Der XIO Befehl für Grafikoperationen  
  
von Markus Kuhnen  
  
Daß der Atari Grafikbefehle zum Zeichnen von Punkten und Linien besitzt, dürfte wohl jedem Atari-User bekannt sein. Auch Kreise lassen sich mit Hilfe der Sinus- und Kosinusfunktionen relativ leicht auf dem Bildschirm ausgeben. Allein das Füllen von Flächen war bisher immer ein großes Problem, wenn man in Basic eine Grafik erstellen wollte.  
  
Es existiert aber eine Möglichkeit, über den allgemein etwas unbekannten Befehl XIO eingeschränkt Flächen auszufüllen.  
  
Dieser Befehl lautet:  
```
XIO 18,#6,0,0,"S:"
```
und ist identisch mit dem Turbo-Basic Befehl FILLTO.  
  
Zunächst muß die Füllfarbe festgelegt werden. Dies geschieht über POKE 765,X. X ist hierbei die Farbe, die auch bei  
COLOR X verwendet wird. Dieser Poke entspricht dem FCOLOR-Befehl des Turbo-Basic.  
  
Nun muß man den linken oberen Rand des zu füllenden Objektes mit PLOT X,Y angeben. Anschließend wird die linke untere Ecke mit POSITION X,Y angegeben. Die Gerade zwischen diesen beiden Punkten wird nach dem Füllen die linke Begrenzung der Fläche sein. Diese Begrenzung muß also nicht unbedingt schon vorher gezeichnet werden. Auch die obere und untere Begrenzung braucht nicht festgelegt zu werden, da der XIO-Befehl die Fläche nur mit waagerechten Linien  
ausfüllt. Auf diese Weise sind die obere und untere Begrenzung immer eine waagerechte Linie oder ein Punkt (wenn die rechte und linke Begrenzung an einem dieser Punkte zusammenlaufen).  
  
Die einzige Linie, die unbedingt schon voeher gezeichnet sein muß, ist die rechte Begrenzung, weil sie genau an gibt, bis wo die einzelnen waagerechten Linien gezeichnet werden sollen.  
  
Das ist es auch, was ich mit eingeschränkt meinte. Die auszufüllende Fläche muß oben und unten entweder durch eine waagerechte Linie oder durch einen Punkt begrenzt sein. Die linke Begrenzung muß eine beliebige Gerade sein.  
Nur die rechte Begrenzung ist frei wählbar. Kreise sind beispielsweise nicht ausfüllbar.  
  
Beispiele:  
  
[xio.png](attachments/xio.png)  
  
Auf der linken Seite ist die Fläche vor dem Füllen gezeichnet. Die Anfangs- und Endpunkte für das Füllen sind mit A und E gekennzeichnet. Rechts ist dann das Resultat zu sehen.  
  
