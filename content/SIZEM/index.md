---
title: SIZEM
---
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|Write| 53260 |$D00C|SIZEM|Size of Missiles 0-3|both  
|Read| 53260 |$D00C|P0PL|Collision Player 0 with Player x|both  
  
### Write: Width of Missiles 0-3  
||Bit ||7,6||5,4||3,2||1,0  
|Missile | M3| M2| M1| M0  
  
||Size ||Bit combination||example  
|normal | 0, 0 | *  
|double | 0, 1 | **  
|normal | 1, 0 | *  
|quadruple | 1, 1 | ****  
  
### Read: Collision Player 0 with Player x  
  
||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|Player x=| | | |  |3| 2| 1| 0  
---
see also:[Player Missile Topics](../Pm_topics/index.md)  
  
previous: [SIZEP3](../SIZEP3/index.md), [M3PL](../SIZEP3/index.md)  
  
next: [GRAFP0](../GRAFP0/index.md), [P1PL](../GRAFP0/index.md)  
