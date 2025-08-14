||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|read|54287|$D40F|NMIST|Non Maskable Interrupt Status|both  
|write|54287|$D40F|NMIRES|Non Maskable Interrupt Reset|both  
  
NMIST: NMI status, holds cause for the NMI interrupt in BITs 5, 6 and 7  
  
NMIRES: Reset for NMIST. Clears the interrupt request register and resets all of the NMI status together.  
  
||Bit||Interrupt  
|7|DLI (Display List)  
|6|VBI (Vertical Blank)  
|5|SYSTEM RESET  
|4|not used  
|3|not used  
|2|not used  
|1|not used  
|0|not used  
  
---
  
see also: [Display List topics](../Displaylist_topics/index.md), [VVBLKI](../VVBLKI/index.md), [WARMSV](../WARMSV/index.md)  
  
previous: [NMIEN](../NMIEN/index.md)  
