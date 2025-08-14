||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|write |54279 |$D407|PMBASE|PM data base address (MSB)|both  
  
The PMBASE write-only register sets the base of memory occupied by Player-Missile Graphics.  
According to bit 4 of [DMACTL](../DMACTL/index.md):  
- when it is 0, the PMG memory area occupies 1024 ($400) bytes of memory and only upper 6 bits of PMBASE matter, so the PM memory area can be set to begin of 1KB boundary.  
- when it is 1, the PMG memory area occupies 2048 ($800) bytes of memory and only upper 5 bits of PMBASE matter, so the PM memory area can be set to begin of 2KB boundary.  
---
see also: [Player Missile Topics](../Pm_topics/index.md) [Pm-memory-map](../Pm-memory-map/index.md)  
  
previous: [VSCROL](../VSCROL/index.md)  
  
next: [CHBASE](../CHBASE/index.md)  
