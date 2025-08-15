---
title: COLPM3
---
||ADR||HEXADR||NAME||DESCRIPTION||DEFAULT||SHADOW||OS  
|53269|$D015|COLPM3|Color of Player and Missile 3|0|[PCOLR3](../PCOLR3/index.md)|all  
  
Missiles have the same color as corresponding Players (e.g. P0=M0, P1=M1, ...) except when joined together as 5th player by setting Bit 4 of [PRIOR](../PRIOR/index.md)/[GPRIOR](../GPRIOR/index.md). Then they have the color of register 3 [COLOR3](../COLOR3/index.md)/[COLPF3](../COLPF3/index.md).  
  
---
see also: [Color topics](../Color_topics/index.md)  
  
previous: 53268, $D014, [COLPM2](../COLPM2/index.md), Color of Player and Missile 2  
  
next: 53270, $D016, [COLPF0](../COLPF0/index.md), Color of Playfield 0  
