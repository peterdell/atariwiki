---
title: PCOLR1
---
||ADR||HEXADR||NAME||DESCRIPTION||SHADOW OF||OS  
|705|$02C1|PCOLR1|Color of Player and Missile 1|[COLPM1](../COLPM1/index.md) |all  
  
Missiles have the same color as corresponding Players (e.g. P0=M0, P1=M1) except when joined together as 5th player by setting Bit 4 of [PRIOR](../PRIOR/index.md)/[GPRIOR](../GPRIOR/index.md). Then they have the color of register 3 [COLOR3](../COLOR3/index.md)/[COLPF3](../COLPF3/index.md).  
  
---
see also: [Color topics](../Color_topics/index.md), [Pm_topics](../Pm_topics/index.md)  
  
previous: 704, $02C0, [PCOLR0](../PCOLR0/index.md), Player/Missile 0 Color Register  
  
next: 706, $02C2, [PCOLR2](../PCOLR2/index.md), Player/Missile 2 Color Register  
