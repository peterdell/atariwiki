||R/W||ADR||HEXADR||NAME||DESCRIPTION||DEFAULT||SHADOW||OS  
|W|53267|$D013|COLPM1|Color of Player and Missile 1|0|[PCOLR1](../PCOLR1/index.md)|all  
|R|53267|$D013|TRIG3|Joystick Trigger 3|n/a|[STRIG3](../STRIG3/index.md)|all  
  
Missiles have the same color as corresponding Players (e.g. P0=M0, P1=M1, ...) except when joined together as 5th player by setting Bit 4 of [PRIOR](../PRIOR/index.md)/[GPRIOR](../GPRIOR/index.md). Then they have the color of register 3 [COLOR3](../COLOR3/index.md)/[COLPF3](../COLPF3/index.md).  
  
TRIG3: only on 400 and 800 machines, else a copy of [STRIG1](../STRIG1/index.md).  
0 when trigger pressed, 1 when trigger released  
  
---
see also: [Color topics](../Color_topics/index.md), [Controller topics](../Controller_topics/index.md)  
  
previous: 53266, $D012, [COLPM0](../COLPM0/index.md), Color of Player and Missile 0  
  
next: 53268, $D014, [COLPM2](../COLPM2/index.md), Color of Player and Missile 2 (W), [PAL](../PAL/index.md) (R)  
