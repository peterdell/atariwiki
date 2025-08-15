---
title: TXTCOL
---
||DEC||HEX||NAME||OS  
|657,658|$291,$292|TXTCOL|all  
  
Text window cursor column; value ranges from zero to 39. Unless changed by the user, location 658 will always be zero (there are only 40 columns in the display, so the MSB will be zero). Since POSITION, PLOT, LOCATE and similar commands refer to the graphics cursor in the display area above the text window, you must use POKE statements to write to this area if PRINT statements are insufficient.  
  
see also:  
  
previous: [TXTROW](../TXTROW/index.md)  
  
next: [TINDEX](../TINDEX/index.md)  
