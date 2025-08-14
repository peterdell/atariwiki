||ADR||HEXADR||NAME||Description||shadow||OS  
|17|$11|BRKKEY| |X|  
  
  
''__copied from "Mapping the ATARI" as an example only! Needs to be re-written or completely written from scratch!__''  
  
17	$0011	BRKKEY  
  
Zero means the BREAK key is pressed; any other number means it's not. A BREAK during I/O returns 128 ($80). Monitored by both keyboard, display, cassette and screen handlers. See [POKMSK](../POKMSK/index.md) location 16 ($A) for hints on disabling the BREAK key. The latest editions of OS provide for a proper vector for BREAK interrupts. The BREAK key abort status code is stored in [STATUS](../STATUS/index.md) (48; $30).  
  
It is also checked during all I/O and scroll/draw routines. During the keyboard handler routine, the status code is stored in DSTAT (76; $4C). BRKKEY is turned off at powerup. BREAK key abort status is flagged by setting BIT 7 of 53774 ($D20E). See the note on the BREAK key vector, above.  
