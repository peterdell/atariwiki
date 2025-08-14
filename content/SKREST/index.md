||Read/Write||ADR||HEXADR||NAME||Description||OS  
|Read|53770|$D20A|RANDOM|random number generator|all  
|Write|53770|$D20A|SKREST|serial status register reset|all  
  
# SKREST (Write)  
Resets the bits 5,6,7 of the serial port status register 53775 [SKCTL](../SKCTL/index.md) to "1"  
  
# RANDOM (Read)  
Read the high order 8 bits of the 17-bit polynominal counter and returns a pseudo random number from 0-255  
  
---
see also: [SKCTL](../SKCTL/index.md), [Sound_Topics](../Sound_Topics/index.md)  
  
previous: [STIMER](../KBCODE/index.md),[KBCODE](../KBCODE/index.md)  
  
next: [POTGO](../POTGO/index.md)  
