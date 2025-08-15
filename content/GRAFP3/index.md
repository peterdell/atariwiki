---
title: GRAFP3
---
||R/W||ADR||HEXADR||NAME||DESCRIPTION||SHADOW||OS  
|Write| 53264 |$D010|GRAFP3|Graphics Shape for Player 3| |both  
|Read| 53264 |$D010|TRIG0|Trigger 0|[STRIG0](../STRIG0/index.md)|both  
  
### Read: Joystick Trigger 0  
  
||Button pressed | 0  
||not pressed |1  
see also [GRACTL](../GRACTL/index.md)  
### Write: Graphics Shape for Player 3  
||Bit|| Missile Nr.  
|7,6| 3  
|5,4| 2  
|3,2| 1  
|1,0| 0  
  
---
see also:[Player Missile Topics](../Pm_topics/index.md), [Controller topics](../Controller_topics/index.md)  
  
previous: [GRAFP2](../GRAFP2/index.md), [P3PL](../GRAFP2/index.md)  
  
next: [GRAFM](../GRAFM/index.md), [TRIG1](../GRAFM/index.md)  
