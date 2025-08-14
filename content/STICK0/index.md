||ADR||HEXADR||NAME||Description||shadow of||OS  
|632| $0278|STICK0|Joystick 1| [PORTA](../PORTA/index.md) |all  
  
This denotes the direction of Joystick 1, where 15 means "centered". It is the lower nibble of [PORTA](../PORTA/index.md) 54016 $d300.  
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
  
previous: [PADDL7](../PADDL7/index.md)  
  
next: [Joystick 2](../STICK1/index.md)  
