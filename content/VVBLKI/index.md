---
title: VVBLKI
---
||ADR||HEXADR||NAME||Description||OS  
|546,547|$0222,$0223|VVBLKI|Vertical Blank Immediate Register|both  
  
VBLANK immediate register. Normally jumps to the stage one VBLANK vector NMI interrupt processor at location 59345 ($E7D1); in the new OS "B" ROMs; 59310, $E7AE). The NMI status register tests to see if the interrupt was due to a VBI (after testing for a DLI) and, if so, vectors through here to VBI the routine, which may be user-written. On powerup, VBI's are enabled and DLI's are disabled. See [VDSLST](../VDSLST/index.md) location 512/$200.  
  
  
see also: [VDSLST](../VDSLST/index.md), [VVBLKD](../VVBLKD/index.md), [Interrupts](../Interrupts/index.md)  
