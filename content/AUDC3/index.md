---
title: AUDC3
---
||Read/Write||ADR||HEXADR||NAME||Description||shadow||OS  
|Read|53765|$D205|POT5|Pot/paddle 5|629|all  
|Write|53765|$D205|AUDC3| Audio channel 3 control|none|all  
  
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
  
previous: [AUDF3](../AUDF3/index.md)  
  
next: [AUDF4](../AUDF4/index.md)  
