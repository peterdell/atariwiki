---
title: TOPSTK
---
||ADR||HEXADR||NAME||Description||shadow||OS  
|144,145|$0090,$0091|MEMTOP/TOPSTK| | |all  
  
*Das Register zeigt auf das Ende des Runtime-Stack (daher TOPSTK). Der Runtime-Stack ist der hinterste Bereich, den ein BASIC-Programm im RAM nutzt und damit ist auch ein  
*Zeiger auf das Ende des BASIC-PRogrammes. Der Platz zwischen MEMTOP und dem Bildspeicher wird durch die FRE(0)-Funktion angegeben.  
  
Grundsätzlich ist der Speicher oberhalb von MEMTOP/TOPSTK bis zur Display-List verfügbar. Da der Runtime-Stack sich jedoch während der Programmausführung verändern kann, ist Vorsicht geboten.  
  
---
  
Hilfsprgramm für das Reservieren von Speicherplatz:  
%%prettify  
```
10 ANZPAGE = 1 : REM ANZAHL DER ZU RESERVIERENDEN SEITEN
20 SIZE = (PEEK(106) - ANZPAGE) * 256
30 IF SIZE <= PEEK(144) + PEEK(145) * 256 THEN PRINT "PROGRAMM ZU GROSS!"
40 END 
```
/%  
  
---
Siehe auch:  
*[MEMTOP](../MEMTOP/index.md) - OS MEMTOP  
*[RUNSTK](../RUNSTK/index.md) - Runtime-Stack-Pointer  
*[SDLSTL](../SDLSTL/index.md) - Display-List-Adresse  
