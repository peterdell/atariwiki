---
title: CHBAS
---
||ADR||HEXADR||NAME||DESCRIPTION||DEFAULT||SHADOW OF||OS  
|756|$02F4|CHBAS|Zeichensatzadresse|224 ($E0)|[CHBASE](../CHBASE/index.md) |all  
  
Defaultwert: 224 ($E0) - Adresse des ROM-Zeichensatzes   
Internationaler Zeichensatz (X): 204 ($CC)  
  
Dieses Register ist die Basisadresse des Zeichensatzes.  
Es ist die Adresse, ab der das Aussehen der Zeichen auf dem Bildschirm definiert wird. Zeichensatzdefinitionen müssen in der GRAPHICS 0 auf einer 1KByte-Grenze beginnen. In den Grafikstufen 1 und 2 muss die Definition auf einer geraden Seitengrenze beginnen; die Startadresse eines Zeichensatzes muss demnach ein Vielfaches von 512 ($200) sein. In CHBAS wird nur die Seitennummer (das High-Byte der Adresse) abgelegt.  
  
Durch Neuinitialisierung bzw. Änderung der Grafikstufe oder durch das Drücken von RESET wird das Register auf den Default-Wert zurückgesetzt.  
Die Zeichen sind nicht in der ATASCII-Reihenfolge, sondern in der „internen“ Reihenfolge im Zeichensatz abgespeichert.  
  
---
see also: [Character_Sets](../Character_Sets/index.md), [topic_list](../topic_list/index.md)  
