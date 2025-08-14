||ADR||HEXADR||NAME||Description||shadow||OS  
|85,86|$0055,$0056|COLCRS|Current cursor column|none|All  
  
Current graphics or text mode cursor column; values range from zero to 319 (high byte, for screen mode eight) depending on current GRAPHICS mode (maximum numher of columns minus one). Location 86 will always be zero in modes zero through seven. Home position is 0,0 (upper left-hand corner). Columns run vertically from the top to the bottom down the TV screen, the leftmost column being number zero, the rightmost column the maximum value in that mode. The cursor has a complete top to bottom, left to right wraparound on the screen.  
  
[ROWCRS](../ROWCRS/index.md) and [COLCRS](../COLCRS/index.md) define the cursor location for the next element to be read from or written to in the main screen segment of the display. For the text window cursor, values in locations 656 to 667 ($290 to $29B) are exchanged with the current values in locations 84 to 95 ($54 to $5F), and location 123 ($7B) is set to 255 ($FF) to indicate the swap has taken place. [ROWCRS](../ROWCRS/index.md) and [COLCRS](../COLCRS/index.md) are also used in the DRAW and FILL functions to contain the values of the endpoint of the line being drawn. The color of the line is kept in location 763 ($2FB). These values are loaded into locations 96 to 98 ($60 to $62) so that [ROWCRS](../ROWCRS/index.md) and [COLCRS](../COLCRS/index.md) may be altered during the operation.  
  
Previous: [ROWCRS](../ROWCRS/index.md)  
  
Next: [DINDEX](../DINDEX/index.md)  
