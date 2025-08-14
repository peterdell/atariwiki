||Read/Write||ADR||HEXADR||NAME||Description||shadow||OS  
|Read|53767|$D207|POT7|Pot/paddle 7|631|all  
|Write|53767|$D207|AUDC4| Audio channel 4 control|none|all  
  
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
  
previous: [AUDF4](../AUDF4/index.md)  
  
next: [AUDCTL](../AUDCTL/index.md)  
