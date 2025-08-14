||R/W||ADR||HEXADR||NAME||DESCRIPTION||SHADOW||OS  
|Read |53265|$D011|TRIG1|Trigger 1|[STRIG1](../STRIG1/index.md)|both  
|Write|53265|$D011|GRAFM|Graphics Shape for Missile 0-3| |both  
  
### Read: Joystick Trigger 1 (645; $285)  
||Button pressed | 0  
||not pressed |1  
see also [GRACTL](../GRACTL/index.md)  
### Write  
||Bit|| Missile Nr.  
|7,6| 3  
|5,4| 2  
|3,2| 1  
|1,0| 0  
  
---
see also:[Player Missile Topics](../Pm_topics/index.md), [Controller topics](../Controller_topics/index.md), [Latch triggers](../GRACTL/index.md)  
  
previous: R: [TRIG0](../GRAFP3/index.md), W: [GRAFP3](../GRAFP3/index.md)   
next: R: [TRIG2](../COLPM0/index.md), W: [COLPM0](../COLPM0/index.md)  
