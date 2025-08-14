||ADR||HEXADR||NAME||Description||shadow||OS  
|79|$004F|COLRSH|Color shift mask|none|All  
  
Attract color shifter; the color registers are EOR'd with locations 78 and 79 at the stage two VBLANK (see locations 18-20;$12-$14). When set to zero and location 78 equals 246, color luminance is reduced 50%. [COLRSH](../COLRSH/index.md) contains the current value of location 19, therefore is given a new color value every 4.27 seconds.  
  
See also:  
  
[ATRACT](../ATRACT/index.md), [DRKMSK](../DRKMSK/index.md)  
