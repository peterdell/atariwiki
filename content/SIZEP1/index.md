---
title: SIZEP1
---
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|Write| 53257 |$D009|SIZEP1|Size Player 1|both  
|Read| 53257 |$D009|M1PL|Collision Missile 1 with Player|both  
  
### Write: Width Player 1  
||decimal||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|0|normal| | | | | | | 0| 0  
|1|double| | | | | | | 0| 1  
|2|normal| | | | | | | 1| 0  
|3|quadruple| | | | | | | 1| 1  
  
### Read: Collision Missile 1 with Player x  
  
||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|Player x=| | | |  |3| 2| 1| 0  
---
see also:[Player Missile Topics](../Pm_topics/index.md)  
  
previous: [SIZEP0](../SIZEP0/index.md), [M0PL](../SIZEP0/index.md)  
  
next: [SIZEP2](../SIZEP2/index.md), [M2PL](../SIZEP2/index.md)  
