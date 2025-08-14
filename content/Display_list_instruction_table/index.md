# Display List Instructions  
There are 3 kinds of instructions  
- $x0 blank lines  
- $x1 jumps  
- $x2-$xF display lines, divided into  
** $x2-$x7 text lines  
** $x8-$xF pixel/map/graphics lines  
  
# Instructions for Blank lines  
||Instruction dec||Instruction hex||BASIC Mode||Scan lines||Pixel per line||Bytes per line||Comment  
|0|$00|na|1|0|0| 1 blank line  
|16|$10|na|2|0|0| 2 blank lines  
|32|$20|na|3|0|0| 3 blank lines  
|48|$30|na|4|0|0| 4 blank lines  
|64|$40|na|5|0|0| 5 blank lines  
|80|$50|na|6|0|0| 6 blank lines  
|96|$60|na|7|0|0| 7 blank lines  
|112|$70|na|8|0|0| 8 blank lines  
  
# Jump Instructions  
||Instruction dec||Instruction hex||BASIC Mode||Scan lines||Pixel per line||Bytes per line||Comment  
|1|$01|na|0|0|0|jump to address, instruction followed by address (2 byte in LSB,MSB order)  
|65|$41|na|0|0|0|jump to address and wait for VBI, instruction followed by address (2 byte in LSB,MSB order)  
  
# Instructions for Text Lines  
||Instruction dec||Instruction hex||BASIC Mode||Scan lines||[VSCROL](../VSCROL/index.md) max||Pixel per line||Bytes per line||Comment  
|2|$02|0|8|7|40|40| Text mode 0, normal text, 24 rows  
|3|$03|na|10|9|40|40| text with full size descenders (e.g. g,p,y,j,q)  
|4|$04|12 XL/XE OS only|8|7|40|40| [4-color-characters](../4_color_character/index.md), 4 pixel width, 24 rows  
|5|$05|13 XL/XE OS only|16|15|40|40| [4-color-characters](../4_color_character/index.md), 4 pixel width, double heigth, 12 rows  
|6|$06|1|8|7|20|20| Text mode 1, double width text, 24 rows  
|7|$07|2|16|15|20|20| Text mode 2, double width and height text, 12 rows  
  
  
# Instructions for Pixel/Graphics Lines  
||Instruction dec||Instruction hex||BASIC Mode||Scan lines||[VSCROL](../VSCROL/index.md) max||Pixel per line||Bytes per line||Comment  
|8|$08|3|8|7|40|10| Graphics Mode 3, 24 rows  
|9|$09|4|4|3|80|10| Graphics Mode 4, 48 rows  
|10|$0A|5|4|3|80|20| Graphics Mode 5, 48 rows  
|11|$0B|6|2|1|160|20| Graphics Mode 6, 96 rows  
|12|$0C|14 XL/XE OS only|1|0|160|20|  Graphics Mode 14, 192 rows  
|13|$0D|7|2|1|160|40| Graphics Mode 7, 96 rows  
|14|$0E|15 XL/XE OS only|1|0|160|40|  Graphics Mode 15, 192 rows  
|15|$0F|8|1|0|320|40| Graphics Mode 8, 192 rows  
  
  
# Added functions  
To activate special functions in a display line, add the value as stated below  
||Function||add decimal||add hex||bit||comment  
|enable Horizontal Scrolling|16|$10|4| see [HSCROL](../HSCROL/index.md), possible for text and pixel lines  
|enable Vertical Scrolling|32|$20|5| see [VSCROL](../VSCROL/index.md), possible for text and pixel lines  
|Load memory scan|64|$40|6|instruction followed by address (2 byte in LSB,MSB order), possible for text and pixel lines. The screen memory can NOT cross a 4K boundary. If screen memory is bigger than 4K, the display list must contain at least 2 LMS commands.  
|enable Display List Interrupt|128|$80|7|see [VDSLST](../VDSLST/index.md), possible for blank, text and pixel lines  
  
---
  
see also: [Display List Topics](../Displaylist_topics/index.md), [VDSLST](../VDSLST/index.md), [VSCROL](../VSCROL/index.md), [HSCROL](../HSCROL/index.md), [4-color-characters](../4_color_character/index.md), [Table_of_Modes_and_Screen_Format](../Table_of_Modes_and_Screen_Format/index.md)  
