---
title: SYSVBV
---
||ADR||HEXADR||NAME||Description||OS  
|58463|$E45F|SYSVBV| |both  
  
Stage one VBLANK calculations entry. It performs the processing of a VBLANK interrupt. Contains JMP instruction for the vector in the next two addresses (58464, 58465; $E460, $E461). This is the address normally found in VVBLKI (546, 547; $222, $223). It is initialized to 59345 ($E7D1), which is the VBLANK routine entry. Initialized to 59345 ($E7D1) old ROMs, 59310 ($E7AE) new ROMs.  
  
see also: [VDSLST](../VDSLST/index.md), [VVBLKI](../VVBLKI/index.md), [VVBLKD](../VVBLKD/index.md), [Interrupt](../Interrupt/index.md)  
