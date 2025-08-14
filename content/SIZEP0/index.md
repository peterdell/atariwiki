||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|Write| 53256 |$D008|SIZEP0|Size Player 0|both  
|Read| 53256 |$D008|M0PL|Collision Missile 0 with Player|both  
  
### Write: Width Player 0  
||decimal||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|0|normal| | | | | | | 0| 0  
|1|double| | | | | | | 0| 1  
|2|normal| | | | | | | 1| 0  
|3|quadruple| | | | | | | 1| 1  
  
### Read: Collision Missile 0 with Player x  
  
||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|Player x=| | | |  |3| 2| 1| 0  
---
see also:[Player Missile Topics](../Pm_topics/index.md)  
  
previous: [HPOSM3](../HPOSM3/index.md), [P3PF](../HPOSM3/index.md)  
  
next: [SIZEP1](../SIZEP1/index.md), [M1PL](../SIZEP1/index.md)  
