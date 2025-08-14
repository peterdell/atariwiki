||ADR||HEXADR||NAME||Description||shadow||OS  
|30|$001E|PBUFSZ| |none|A  
Print buffer size of printer record for current mode. Normal buffer size and line size equals 40 bytes; double-width print equals 20 bytes (most printers use their own control codes for expanded print); sideways printing equals 29 bytes (Atari 820 printer only). Printer status request equals four. PBUFSZ is initialized to 40. The printer handler checks to see if the same value is in PBPNT and, if so, sends the contents of the buffer to the printer.  
