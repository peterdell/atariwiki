---
title: KEYREP
---
||Adr||hex||Name||description||OS  
|730|$02DA|KEYREP|rate of key repeat|XL/XE  
  
The rate of the repeat; default is 6, which means ten characters per second (one each six VBLANK intervals after the delay above). POKE with the number of VBLANK intervals between repeats; with a value of 1, you get 60 characters per second (50 on PAL systems)! A value of 0 provides one key repeat only per press.  
  
see also: [Keyboard topics](../Keyboard_topics/index.md), [NOCLIK](../NOCLIK/index.md), [KRPDEL](../KRPDEL/index.md)  
  
Bestimmt die Tastenwiederholrate in 1/50sek (Vertical Blanks). Standardwert ist 5.  
