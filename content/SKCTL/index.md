---
title: SKCTL
---
||r/w||ADR||HEXADR||NAME||Description||Shadow||OS  
|write|53775|$D20F|SKCTL|Serial Port Control|[SSKCTL](../SSKCTL/index.md)|all  
|read|53775|$D20F|SKSTAT|Serial Port Status|[SSKCTL](../SSKCTL/index.md)|all  
  
## Write  
||Bit||Function  
|0|Enable keyboard debounce circuits.  
|1|Enable keyboard scanning circuit.  
|2|Fast pot scan: the pot scan counter completes its sequence in two TV line times instead of one frame time (228 scan lines). Not as accurate as the normal pot scan, however.  
|3|Serial output is transmitted as a two-tone signal rather than a logic true/false. POKEY two-tone mode.  
|4,5,6|Serial port mode control used to set the bi-directional clock lines so that you can either receive external clock data or provide clock data to external devices (see the Hardware Manual, p. II.27). There are two pins on the serial port for Clock IN and Clock OUT data. See the OS User's Manual, p. 133.  
|7|Force break (serial output to zero)  
  
## Read  
||Bit||Function  
|0|not used by SKSTAT  
|1|Serial input shift register busy  
|2|the last key is still pressed  
|3|the SHIFT key is pressed  
|4|Data can be read directly from the serial input port, ignoring the shift register.  
|5|Keyboard over-run. Reset BITs 7 to 5 (latches) to one writing any number to [SKREST](../SKREST/index.md) at 53770 ($D20A).  
|6|Serial data input over-run. Reset latches as above.  
|7|Serial data input frame error caused by missing or extra bits. Reset latches as above.  
  
  
  
---
see also: [Keyboard topics](../Keyboard_topics/index.md)  
  
previous: [IRQEN](../IRQEN/index.md),[IRQST](../IRQEN/index.md)  
  
next: [PORTA](../PORTA/index.md) of PIA  
