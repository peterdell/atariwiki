---
title: PBCTL
---
||ADR||HEXADR||NAME||Description||OS  
|54019|$D303|PBCTL|Port B Control|only A (400/800)  
  
||Bit||Function||Description  
|7|PA7|Interrupt status of SIO  
|6|PA6|always 0  
|5|PA5|always 1  
|4|PA4|always 1  
|3|PA3|Status of command line of SIO  
|2|PA2|1=use Port B for data input/output, 0=define data direction, see below  
|1|PA1|always 0  
|0|PA0|Interrupt of PROCEED line on/off, set to 0 by OS  
  
To define the data direction of PORT B, set Bit 2 of [PBCTL](../PBCTL/index.md) to 0. Then write a byte to [PORTB](../PORTB/index.md), where Bits set to 1 indicate WRITE and Bits set to 0 indicate READ. Normally [PORTB](../PORTB/index.md) is set to %00000000 (=all input).  
  
---
see also: [Controller topics](../Controller_topics/index.md)  
  
previous: [PACTL](../PACTL/index.md)  
  
next: [DMACTL](../DMACTL/index.md) of ANTIC  
