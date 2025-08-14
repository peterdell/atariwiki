||ADR||HEXADR||NAME||DESCRIPTION||DEFAULT||SHADOW||OS  
|18-20|$12-$14|RTCLOK|Interne Uhr| | |all  
  
Die Register 18, 19 und 20 sind die "interne Uhr" des Atari.  
  
Die Speicherzelle 20 ist ein Jiffie-Zähler, d.h. der Inhalt wird alle 1/50 Sekunde (während jedes Vertikal-Blanks) um 1 erhöht und erreicht daher alle 5,12 Sekunden den Wert 255.  
  
Immer wenn Register 20 den Wert 255 erreicht hat und wieder bei Null beginnt (alle 5,1 Sekunden), wird der Inhalt von Register 19 um Eins erhöht. Gleiches geschieht mit Speicherzelle 18, wenn 19 den Wert 255 erreicht hat (alle 21:50,72 Minuten). Somit ergibt sich eine Dauer von 96:29:01 Stunden, bis auch Zelle 18 wieder bei 0 beginnt.  
  
Diese Uhr wird vom Betriebssystem nicht benutzt und wird auch während zeitkritischer I/0-Operationen weiter erhöht, sie kann vom Benutzer ohne Einschränkungen verwendet werden.  
