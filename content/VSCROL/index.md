||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|write only|54277|$D405|VSCROL|Vertical Fine Scrolling|both  
  
If this location is set to a value other than zero, the ANTIC starts displaying every line with bit 5 set (enable vertical scrolling) that number of scan line "later", the picture is shifted "up".  
  
This register should not be altered while ANTIC is drawing the screen. It has to be changed during vertical blank interrupt to get good results.  
  
```
VSCROL=0  VSCROL=2 
........  ..####..
...##...  .##..##.
..####..  .######.
.##..##.  .##..##.
.######.  .##..##.
.##..##.  ........
.##..##.  ........
........  .##..##.

........  .##..##.
.##..##.  .######.
.##..##.  .##..##.
.######.  .##..##.
.##..##.  .##..##.
.##..##.  ........
.##..##.  ........
........  ........
```
  
If there are several consecutive lines set for vertical fine scrolling (display list instruction with bit 5 set to "1"), the last line to be scrolled has to have bit 5 set to 0, to inhibit lines "jumping" into the screen.  
  
  
---
see also: [Display List topics](../Displaylist_topics/index.md)  
  
previous: [HSCROL](../HSCROL/index.md)  
  
next: [PMBASE](../PMBASE/index.md)  
