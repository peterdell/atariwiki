---
title: CASINI
---
||ADR||HEXADR||NAME||Description||shadow||OS  
|2,3|$0002,$0003|CASINI| | |all  
  
Durch diese Adresse wird bei der Initialisierung eines Bootprogrammes von Kassette gesprungen. Die hier abgelegten Daten stammen aus dem 5. und 6. Byte des ersten Records (jeder Record umfasst 128 Bytes) eines Kassettenfiles. Sie repräsentieren die Startadresse des geladenen Programms.  
  
Die ersten sechs Byte eines Kasstten-Boot-Record werden wie folgt genutzt:  
||1|wird ignoriert  
||2|Anzahl der zu ladenden Blöcke  
||3,4|Ladeadresse des Programms  
||5,6|Startadresse des Programms  
  
