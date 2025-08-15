---
title: MEMTOP
---
||ADR||HEXADR||NAME||Description||shadow||OS  
|741,742|$02E5,$02E6|MEMTOP aka HIMEM| | |all  
  
Zeiger auf das letzte für den Anwender freie Byte im Speicher. Das entspricht jedoch nicht dem Ende des RAM. Oberhalb von MEMTOP liegen noch die Display-List und die Bildspeicherdaten. Der Wert von MEMTOP kann sich ändern beim Wechsel der Grafikstufe, Öffnen eines Kanals für den Bildschirm, RESET und POWER-UP.  
  
Von BASIC wird diese Speicherstelle als [HIMEM](../MEMTOP/index.md) bezeichnet.  
  
Wenn ein Wechsel der Grafikstufe dazu führt, dass Speicher unterhalb der von [APPMHI](../APPMHI/index.md) angegebenen Adresse benötigt wird, dann wird der Bildschirm zurück in GRAPHICS 0 gesetzt, MEMTOP wird aktuallisert und ein Fehler wird ausgegeben. Andernfalls wird der Wechsel der Grafikstufe durchgeführt und MEMTOP wird auf den neuen Wert gesetzt.  
  
Es ist Vorsicht geboten, wenn Daten unterhalb von MEMTOP abgelegt werden, da diese durch einen Wechsel der Grafikstufe zerstört werden können. Um dies zu vermeiden, muss sichergestellt werden, dass APPMHI einen Wert hat, der oberhalb der relevanten Daten liegt.  
  
---
  
Siehe auch:  
*[MEMTOP](../TOPSTK/index.md) - BASIC MEMTOP/TOPSTK (Ende des Runtime Stack und damit des Ende des BASIC-Programmes)  
*[APPMHI](../APPMHI/index.md) - Adresse oberhalb derer die Bildschirmdaten und die Displaylist liegen können  
