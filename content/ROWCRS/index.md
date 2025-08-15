---
title: ROWCRS
---
||ADR||HEXADR||NAME||Description||shadow||OS  
|84|$0054|ROWCRS|Current cursor row|none|All  
  
Current graphics or text screen cursor row, value ranging from zero to 191 ($BF) depending on the current GRAPHICS mode (maximum number of rows, minus one). This location, together with location 85 below, defines the cursor location for the next element to be read/written to the screen. Rows run horizontally, left to right across the TV screen. Row zero is the topmost line; row 192 is the maximum value for the bottom-most line.  
  
Previous: [RMARGN](../RMARGN/index.md)  
  
Next: [COLCRS](../COLCRS/index.md)  
