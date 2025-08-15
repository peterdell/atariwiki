---
title: FINE
---
||ADR||HEXADR||NAME||Description||shadow||OS  
|622|$026E|FINE|Fine scroll enable|none|X  
  
Fine-scroll enable for graphics mode 0 (text); POKE with 0 for coarse scrolling (the default) and 255 ($FF) for fine scrolling. Follow the POKE with GR.0 or an OPEN for device E:. Try listing a long program - it's slow and smooth! The display list for fine scrolling is one byte longer than for coarse scrolling. The OS places the address (64708; $FCC4) of a Display List Interrupt (DLI) at 512,513/$0200,$0201 [VDSLST](../VDSLST/index.md), replacing any you might have placed there. The color register at 53271/$D017 [COLPF1](../COLPF1/index.md) is altered for the last visible screen line.  
If you enable fine scrolling and go immediately to DOS, you'll see that it's still enabled when you do a copy to screen or disk directory.  
