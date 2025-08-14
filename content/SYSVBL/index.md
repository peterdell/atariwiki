||ADR||HEXADR||NAME||Description||OS  
|59345|$E7D1|SYSVBL| |see below  
  
The VBLANK routines start here, including frame counter, update timer, update hardware registers from shadow registers, update the attract mode counter and the realtime clock.  
  
The vertical blank immediate vector, [VVBLKI](../VVBLKI/index.md), normally pointed to by locations 546,547/$0222,$0223), points to here.  
  
The Updated OS ROMs point to 59310/$E7AE.  
  
see also: [VBI_Vertical_Blank_Interrupt](../VBI_Vertical_Blank_Interrupt/index.md)  
