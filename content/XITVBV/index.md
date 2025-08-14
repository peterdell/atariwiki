||ADR||HEXADR||NAME||Description||OS  
|58466|$E462|XITVBV|Exit from the VBLANK routine|both  
  
Exit from the VBLANK routine, entry point. Contains JMP to the address stored in next two locations (58467, 58468; $E463, $E464). This is the address normally found in [VVBLKD](../VVBLKD/index.md) (548,549; $0224,$0225).  
  
### OS A/B  
Initialized to 59710/$E93E, which is the VBLANK exit routine. It is used to restore the computer to its pre-interrupt state and to resume normal processing.  
  
### XL/XE OS  
Initialized to 59710/$E93E old ROMs, 59653/$E905.  
  
see also: [SETVBV](../SETVBV/index.md), [VVBLKI](../VVBLKI/index.md), [VVBLKD](../VVBLKD/index.md), [SYSVBV](../SYSVBV/index.md), [Interrupts](../Interrupts/index.md)  
