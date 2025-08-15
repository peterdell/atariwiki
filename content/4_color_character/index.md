---
title: 4_color_character
---
# 4-color Characters  
The color of each pixel (4 in a line instead of the usual 8) depends on the bit combination of the byte in the character definition.  
  
||Bit Pair||Color||Address dec||Address hex||comment  
|00|[COLOR4](../COLOR4/index.md) BAK|712|$02C8|  
|01|[COLOR0](../COLOR0/index.md) PF0|708|$02C4|  
|10|[COLOR1](../COLOR1/index.md) PF1|709|$02C5|  
|11|[COLOR2](../COLOR2/index.md) PF2|710|$02C6|if bit 7 of character code = 0  
|11|[COLOR3](../COLOR3/index.md) PF3|711|$02C7|if bit 7 of character code = 1  
  
# Example  
character "A" (code=65) would be displayed as  
```
00000000 BAK BAK BAK BAK
00011000 BAK PF0 PF1 BAK
00111100 BAK PF2 PF2 BAK compare with line 3 below
01100110 PF0 PF1 PF0 PF1
01100110 PF0 PF1 PF0 PF1
01111110 PF0 PF2 PF2 PF1 compare with line 6 below
01100110 PF0 PF1 PF0 PF1
00000000 BAK BAK BAK BAK
```
  
character "inverse A" (code=193, Bit 7 set because inverse video is on!) would be displayed as  
```
00000000 BAK BAK BAK BAK
00011000 BAK PF0 PF1 BAK
00111100 BAK PF3 PF3 BAK compare with line 3 above
01100110 PF0 PF1 PF0 PF1
01100110 PF0 PF1 PF0 PF1 
01111110 PF0 PF3 PF3 PF0 compare with line 6 above
01100110 PF0 PF1 PF0 PF1
00000000 BAK BAK BAK BAK
```
  
To try this, type (works only on an ATARI XL or XE):  
```
GRAPHICS 13:? #6;"A A A":? #6;"A A A":REM the second 3 "A"s are inverse video!
```
![](attachments/GR13DEMO.png)  
---
see also: [Color topics](../Color_topics/index.md), [topic_list](../topic_list/index.md)  
