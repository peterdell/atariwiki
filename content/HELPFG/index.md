||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|read/write |732|$02DC|HELPFG|Help key register|XL/XE  
  
The Help-Key is read from [KBCODE](../KBCODE/index.md) and stored in HELPFG. There is no normal action when HELP is pressed. The programmer has to check HELPFG or KBCODE.  
  
## Bits  
||Bit||Function  
|0| HELP  
|4| HELP  
|6| SHIFT  
|7| CTRL  
  
## Values  
||Hex||Dec||Explanation  
|$00|0|HELP Flag cleared  
|$11|17|HELP key pressed  
|$51|81|SHIFT HELP pressed  
|$91|145|CTRL HELP pressed  
  
---
see also: [Keyboard topics](../Keyboard_topics/index.md) [Console Keys](../CONSOL/index.md)  
