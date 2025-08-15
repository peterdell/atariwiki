---
title: STICK3
---
||ADR||HEXADR||NAME||Description||shadow of||OS  
|635| $027B|STICK3|Joystick 4| [PORTB](../PORTB/index.md) |A  
  
This denotes the direction of Joystick 4, where 15 means "centered". It is the higher nibble of [PORTB](../PORTB/index.md) 54017 $d301.  
Joystick 4 is only available on ATARI 400/800 machines. In XL and XE OS's this register has the same content as [STICK1](../STICK1/index.md).  
  
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
  
previous: [Joystick 3](../STICK2/index.md)  
