||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|write only|54276|$D404|HSCROL|Horizontal Fine Scrolling|both  
  
If this location is set to a value other than zero, the ANTIC omits that number of color cycles in that line. In other words, ANTIC start displaying that number of color cycles line "later", the picture is shifted "left".  
  
Only the lower 4 bits of this register are used, so the maximum value is 15.  
  
This register should not be altered while ANTIC is drawing the screen. It has to be changed during vertical blank interrupt to get good results.  
  
  
||ANTIC Mode||BASIC Mode||Max value for HSCROL||Comment  
|$02|0|3|Text mode 0, normal text, 24 rows  
|$03|na|3|Text with full size descenders (e.g. g,p,y,j,q)  
|$04|12 XL/XE OS only|3|4-color-characters, 4 pixel width, 24 rows  
|$05|13 XL/XE OS only|3|4-color-characters, 4 pixel width, double heigth, 12 rows  
|$06|1|7|Text mode 1, double width text, 24 rows  
|$07|2|7|Text mode 2, double width and height text, 12 rows  
|$08|3| |Graphics Mode 3, 24 rows  
|$09|4| |Graphics Mode 4, 48 rows  
|$0A|5| |Graphics Mode 5, 48 rows  
|$0B|6| |Graphics Mode 6, 96 rows  
|$0C|14 XL/XE OS only| | Graphics Mode 14, 192 rows  
|$0D|7| |Graphics Mode 7, 96 rows  
|$0E|15 XL/XE OS only| |Graphics Mode 15, 192 rows  
|$0F|8| |Graphics Mode 8, 192 rows  
  
---
see also: [Display List topics](../Displaylist_topics/index.md)  
  
previous: [DLISTL](../DLISTL/index.md),[DLISTH](../DLISTL/index.md)  
  
next: [VSCROL](../VSCROL/index.md)  
