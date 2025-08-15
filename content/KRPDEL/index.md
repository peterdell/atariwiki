---
title: KRPDEL
---
||Adr||hex||Name||description||OS  
|729|$02D9|KRPDEL|auto-repeat delay|XL/XE  
  
Auto-delay rate; the time elapsed before keyboard repeat begins. Initially set at 48 ($30; $28 for PAL machines) for 0.8 seconds; you can POKE it with the number of VBLANK intervals (1/60 second each) before repeat begins. A value of 60 would be a one-second delay. A value of 0 means no repeat.  
  
see also: [Keyboard topics](../Keyboard_topics/index.md), [NOCLIK](../NOCLIK/index.md), [KEYREP](../KEYREP/index.md)  
  
Bestimmt die Verzögerung der Tastenwiederholung 1/50sek (Vertical Blanks). Standardwert ist 40/$28 für PAL. Setzt man den Wert auf 0, prellt die Tastaur und Schreiben wird unmöglich.  
