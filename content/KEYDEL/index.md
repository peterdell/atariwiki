---
title: KEYDEL
---
||Adr||hex||Name||Description||OS  
|753|$02F1|KEYDEL|key delay flag|all  
  
Key delay flag or key debounce counter; used to see if any key has been pressed. If a zero is returned, then no key has been pressed. If three is returned, then any key. It is decremented every stage two VBLANK (1/60 or 1/30th second) until it reaches zero. If any key is pressed while KEYDEL is greater than zero, it is ignored as "bounce."  
  
see also: [Keyboard topics](../Keyboard_topics/index.md), [CH](../CH/index.md), [CH1](../CH1/index.md)  
