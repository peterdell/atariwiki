---
title: PCOLR0
---
||ADR||HEXADR||NAME||DESCRIPTION||SHADOW OF||OS  
|704|$02C0|PCOLR0|Color of Player and Missile 0|[COLPM0](../COLPM0/index.md) |all  
  
Missiles have the same color as corresponding Players (e.g. P0=M0, P1=M1) except when joined together as 5th player by setting Bit 4 of [PRIOR](../PRIOR/index.md)/[GPRIOR](../GPRIOR/index.md). Then they have the color of register 3 [COLOR3](../COLOR3/index.md)/[COLPF3](../COLPF3/index.md).  
  
---
see also: [Color topics](../Color_topics/index.md), [Player Missile Topics](../Pm_topics/index.md)  
  
previous: 703, $02BF, [BOTSCR](../BOTSCR/index.md)  
  
next: 705, $02C1, [PCOLR1](../PCOLR1/index.md), Player/Missile 1 Color Register  
