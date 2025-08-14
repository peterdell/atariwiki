||ADR||HEXADR||NAME||Description||shadow||OS  
|16|$10|POKMSK|Interrupt-Maske für POKEY |[IRQEN](../IRQEN/index.md)|  
  
  
  
||BIT||DECIMAL||FUNCTION  
|7|128| BREAK key is enabled.  
|6|64| "other key" interrupt is enabled.  
|5|32| Serial input data ready interrupt is enabled.  
|4|16| Serial output data required interrupt is enabled.  
|3|8| Serial out transmission finished interrupt is enabled.  
|2|4| POKEY timer four interrupt is enabled (only in the "B" or later versions of the OS ROMs).  
|1|2| POKEY timer two interrupt is enabled.  
|0|1| POKEY timer one interrupt is enabled.  
