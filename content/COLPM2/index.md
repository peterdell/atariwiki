---
title: COLPM2
---
||R/W||ADR||HEXADR||NAME||DESCRIPTION||DEFAULT||SHADOW||OS  
|W|53268|$D014|COLPM2|Color of Player and Missile 2|0|[PCOLR2](../PCOLR2/index.md)|all  
|R|53268|$D014|PAL|Determine TV System|see below|none|all  
  
Missiles have the same color as corresponding Players (e.g. P0=M0, P1=M1, ...) except when joined together as 5th player by setting Bit 4 of [PRIOR](../PRIOR/index.md)/[GPRIOR](../GPRIOR/index.md). Then they have the color of register 3 [COLOR3](../COLOR3/index.md)/[COLPF3](../COLPF3/index.md).  
  
PAL (R) Used to determine if the Atari is PAL (European and Israeli TV compatible when BITs 1 - 3 equal zero) or NTSC (North American compatible when BITs 1 - 4 equal one; 14 decimal, $F). European Ataris run 12% slower if tied to the VBLANK cycle (the PAL VBLANK cycle is every 50th second rather than every 60th second). They use only one CPU clock at three MHZ, so the 6502 runs at 2.217 MHZ -- 25% faster than North American Ataris. Also, their $E000 and $F000 ROMs are different, so there are possible incompatibilities with North American Ataris in the cassette handling routines. There is a third TV standard called SECAM, used in France, the USSR, and parts of Africa. I am unaware if there is any Atari support for SECAM standards.  
PAL TV has more scan lines per frame, 312 compared to 262. NTSC Ataris compensate by adding extra lines at the beginning of the VBLANK routine. Display lists do not have to be altered, and colors are the same because of a hardware modification.  
  
See also: [PALNTS](../PALNTS/index.md)  
  
  
---
see also: [Color topics](../Color_topics/index.md)  
  
previous: 53267, $D013, [COLPM1](../COLPM1/index.md), Color of Player and Missile 1  
  
next: 53269, $D015, [COLPM3](../COLPM3/index.md), Color of Player and Missile 3  
