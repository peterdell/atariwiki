||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS||DEFAULT VALUE  
|read only|54286|$D40E|NMIEN|Non Maskable Interrupt Enable|both|64/$40  
  
  
||Bit||Value||Interrupt  
|7|$80/128|DLI (Display List INTERRUPT) enable  
|6|$40/64|VBI (Vertical Blank INTERRUPT) enable  
|5|$20/32|SYSTEM RESET enable  
|4| |not used  
|3| |not used  
|2| |not used  
|1| |not used  
|0| |not used  
  
  
Bit 7 does NOT switch on/off the Display List itself, but the display List INTERRUPTS!  
  
---
  
see also: [Display List topics](../Displaylist_topics/index.md)  
  
previous: [PENV](../PENV/index.md)  
  
next: [NMIST](../NMIST/index.md),[NMIRST](../NMIST/index.md)  
