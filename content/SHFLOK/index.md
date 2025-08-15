---
title: SHFLOK
---
||Adr||Hex||Name||Description||OS||default  
|702|$02BE|SHFLOK|Keyboard lock state|all|$40/64  
  
Register contains information about "lock" status of the keyboard, eg. SHIFT-lock or CTRL-lock  
  
||Value hex||Value dec||Explanation  
|$00|0|small letters  
|$40|64|Caps Lock capital letters  
|$80|128|CTRL lock graphic characters  
  
Siehe auch: [CH](../CH/index.md) [Keyboard topics](../Keyboard_topics/index.md)  
