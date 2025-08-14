||R/W||ADR||HEXADR||NAME||DESCRIPTION||DEFAULT||SHADOW||OS  
|W|53266|$D012|COLPM0|Color of Player and Missile 0|0|[PCOLR0](../PCOLR0/index.md)|all  
|R|53266|$D012|TRIG2|Trigger Joystick 2|n/a|[STRIG2](../STRIG2/index.md)|all  
  
Missiles have the same color as corresponding Players (e.g. P0=M0, P1=M1, ...) except when joined together as 5th player by setting Bit 4 of [PRIOR](../PRIOR/index.md)/[GPRIOR](../GPRIOR/index.md). Then they have the color of register 3 [COLOR3](../COLOR3/index.md)/[COLPF3](../COLPF3/index.md).  
  
TRIG2: only on 400 and 800 machines, else a copy of [STRIG0](../STRIG0/index.md). 0 when trigger pressed, 1 when trigger released  
  
---
see also: [Color topics](../Color_topics/index.md), [Controller topics](../Controller_topics/index.md)  
  
previous: 53265, $D011, [GRAFM](../GRAFM/index.md), Graphics for Missiles  
  
next: 53267, $D013, [COLPM1](../COLPM1/index.md), Color of Player and Missile 1  
