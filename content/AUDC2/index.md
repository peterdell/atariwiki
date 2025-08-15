---
title: AUDC2
---
||Read/Write||ADR||HEXADR||NAME||Description||shadow||OS  
|Read|53763|$D203|POT3|Pot/paddle 3|627|all  
|Write|53763|$D203|AUDC2| Audio channel 2 control|none|all  
  
||Bit||Description  
|7,6,5|Distortion  
|4|Volume only  
|3,2,1,0|Volume  
  
Volume from 0 to 15 (16 steps)  
  
||7||6||5||description of distortion  
|1|1|1|rectangular curve  
|1|1|0|4-bit poly  
|1|0|1|rectangular curve  
|1|0|0|17-bit-poly  
|0|1|1|5-bit poly  
|0|1|0|5-bit poly, then 4-bit-poly  
|0|0|1|5-bit poly  
|0|0|0|5-bit poly, then 17-bit-poly  
  
---
  
see also: [Sound_Topics](../Sound_Topics/index.md), [AUDCTL](../AUDCTL/index.md), [STIMER](../KBCODE/index.md)  
  
previous: [AUDF2](../AUDF2/index.md)  
  
next: [AUDF3](../AUDF3/index.md)  
