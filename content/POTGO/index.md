||Read/Write||ADR||HEXADR||NAME||Description||OS  
|Write|53771|$D20B|POTGO|Start Pot reading sequence|all  
  
Start the POT scan sequence. You must read your POT values first and then start the scan sequence, since POTGO resets the POT registers to zero. Written by the stage two VBLANK sequence.  
  
---
see also: [Controller topics](../Controller_topics/index.md), [POT0](../POT0/index.md)-[POT7](../POT7/index.md), [ALLPOT](../ALLPOT/index.md), [PADDL0](../PADDL0/index.md)-[PADDL7](../PADDL7/index.md)  
  
previous: [RANDOM](../SKREST/index.md),[SKREST](../SKREST/index.md)  
  
next: [SEROUT](../SEROUT/index.md),[SERIN](../SEROUT/index.md)  
