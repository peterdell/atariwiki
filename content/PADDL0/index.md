||ADR||HEXADR||NAME||Description||shadow of||OS  
|624|$0270|PADDL0|Paddle 1|[POT0](../POT0/index.md) |all  
# Values  
Value of Paddle 1. The value is between 1/$01 (rightmost) and 228/$E4 (leftmost), so it is increasing when turned counter-clockwise.  
  
Paddles come in pairs, 2 Paddles with one connector.  
  
Because people tend to enumerate beginning with "1" and the ports at the ATARI are called "1","2","3","4", we will call the paddles "1" to "8". The ATARI starts counting at "0", so the list goes from "0" to "7".  
# Numbering the paddles  
||Physical (User)||logical (ATARI)  
|first pair (in port 1)|  
|1|0 (PADDL0)  
|2|1 (PADDL1)  
|second pair (in port 2)|  
|3|2 (PADDL2)  
|4|3 (PADDL3)  
|third pair (in port 3, only on ATARI 400/800 with 4 controller jacks)|  
|5|4 (PADDL4)  
|6|5 (PADDL5)  
|fourth pair (in port 4, only on ATARI 400/800 with 4 controller jacks)|  
|7|6 (PADDL6)  
|8|7 (PADDL7)  
  
---
see also: [Controller topics](../Controller_topics/index.md), [POTGO](../POTGO/index.md), [ALLPOT](../ALLPOT/index.md)  
  
previous: [GPRIOR](../GPRIOR/index.md)  
  
next: [PADDL1](../PADDL1/index.md)  
