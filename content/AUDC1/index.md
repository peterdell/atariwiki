---
title: AUDC1
---
||Read/Write||ADR||HEXADR||NAME||Description||shadow||OS  
|Read|53761|$D201|POT1|Pot/paddle 1|625|all  
|Write|53761|$D201|AUDC1| Audio channel 1 control|none|all  
  
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
  
previous: [AUDF1](../AUDF1/index.md)  
  
next: [AUDF2](../AUDF2/index.md)  
