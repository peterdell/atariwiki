||ADR||HEXADR||NAME||Description||OS  
|54018|$D302|PACTL|Port A Control|all  
  
||Bit||Function||Description  
|7|PA7|read only: Interrupt status of PROCEED, 1=Interrupt  
|6|PA6|always 0  
|5|PA5|always 1  
|4|PA4|always 1  
|3|PA3|Cassette player motor control, 0=on, 1=off  
|2|PA2|1=use Port A for data input/output, 0=define data direction, see below  
|1|PA1|always 0  
|0|PA0|Interrupt of PROCEED line on/off, set to 0 by OS  
  
To define the data direction of PORT A, set Bit 2 of [PACTL](../PACTL/index.md) to 0. Then write a byte to [PORTA](../PORTA/index.md), where Bits set to 1 indicate WRITE and Bits set to 0 indicate READ. Normally [PORTA](../PORTA/index.md) set to %00000000 (=all input).  
  
---
see also: [Controller topics](../Controller_topics/index.md)  
  
previous: [PORTB](../PORTB/index.md)  
  
next: [PBCTL](../PBCTL/index.md)  
