||ADR||HEXADR||NAME||Description||shadow||OS  
|97,98|$0061,$0062|NEWCOL| |none|A  
Point (column) to which DRAWTO and XIO 18 (FILL) will go. [NEWROW](../NEWROW/index.md) and [NEWCOL](../NEWCOL/index.md) are initialized to the values in [ROWCRS](../ROWCRS/index.md) and [COLCRS](../COLCRS/index.md) (84 to 86; $54 to $56) above, which represent the destination end point of the DRAW and FILL functions. This is done so that [ROWCRS](../ROWCRS/index.md) and [COLCRS](../COLCRS/index.md) can be altered during these routines.  
