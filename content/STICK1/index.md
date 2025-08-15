---
title: STICK1
---
||ADR||HEXADR||NAME||Description||shadow of||OS  
|633| $0279|STICK1|Joystick 2| [PORTA](../PORTA/index.md) |all  
  
This denotes the direction of Joystick 2, where 15 means "centered". It is the higher nibble of [PORTA](../PORTA/index.md) 54016 $d300.  
This address is only updated every 1/50 second during VBlank!  
  
||dec ||left|| ||right  
|up|10|14|&nbsp;6  
| |11|15| &nbsp;7  
|down|&nbsp;9|13|&nbsp;5  
  
||hex ||left|| ||right  
|up|$0A|$0E|$06  
| |$0B|$0F|$07  
|down|$09|$0D|$05  
  
||bin ||left|| ||right  
|up|1010|1110|0110  
| |1011|1111|0111  
|down|1001|1101|0101  
  
---
see also [Controller topics](../Controller_topics/index.md)  
  
previous: [Joystick 1](../STICK0/index.md)  
  
next: [Joystick 3](../STICK2/index.md)  
