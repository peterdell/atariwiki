---
title: VDELAY
---
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|write |53276 |$D01C|VDELAY|Vertical Delay for PM|both  
  
Vertical Delay register. When using double line resolution for players and missiles you can normally only use every second line. Setting bit in this register moves the object down one scan line on the screen.  
  
||Bit||Object  
|7|Player 3  
|6|Player 2  
|5|Player 1  
|4|Player 0  
|3|Missile 3  
|2|Missile 2  
|1|Missile 1  
|0|Missile 0  
  
  
For switching between single and double line resolution see Bit 5 of [SDMCTL](../SDMCTL/index.md)  
  
---
see also: [Player Missile Topics](../Pm_topics/index.md), [SDMCTL](../SDMCTL/index.md)  
  
previous: [PRIOR](../PRIOR/index.md)  
  
next: [GRACTL](../GRACTL/index.md)  
