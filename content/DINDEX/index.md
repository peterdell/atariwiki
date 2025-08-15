---
title: DINDEX
---
||ADR||HEXADR||NAME||Description||shadow||OS  
|87|$0057|DINDEX|Display mode/current screen mode|none|All  
  
[DINDEX](../DINDEX/index.md) contains the number obtained from the low order four bits of most recent open AUX1 byte. It can be used to barl the OS into thinking you are in a different GRAPHICS mode by POKEing DINDEX with a number from zero to 11.  
  
Previous: [COLCRS](../COLCRS/index.md)  
  
Next: [SAVMSC](../SAVMSC/index.md)  
