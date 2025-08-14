||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|Write| 53259 |$D00B|SIZEP3|Size Player 3|both  
|Read| 53259 |$D00B|M3PL|Collision Missile 3 with Player|both  
  
### Write: Width Player 3  
||decimal||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|0|normal| | | | | | | 0| 0  
|1|double| | | | | | | 0| 1  
|2|normal| | | | | | | 1| 0  
|3|quadruple| | | | | | | 1| 1  
  
### Read: Collision Missile 3 with Player x  
  
||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|Player x=| | | |  |3| 2| 1| 0  
---
see also:[Player Missile Topics](../Pm_topics/index.md)  
  
previous: [SIZEP2](../SIZEP2/index.md), [M2PL](../SIZEP2/index.md)  
  
next: [SIZEM](../SIZEM/index.md), [P0PL](../SIZEM/index.md)  
