||ADR||HEXADR||NAME||Description||OS  
|740|$02E4|RAMSIZ|RAM Size, high byte/number of pages|both  
  
RAM size, high byte only; this is the number of pages that the top of RAM represents (one page equals 256 bytes). Since there can never be less than a whole page, it becomes practical to measure RAM in those page units. This is the same value as in [RAMTOP](../RAMTOP/index.md) location 106 ($6A), passed here from [TRAMSZ](../TRAMSZ/index.md), location 6. Space saved by moving [RAMSIZ](../RAMSIZ/index.md) or [RAMTOP](../RAMTOP/index.md) has the advantage of being above the display area. Initialized to 160 for a 48K Atari.  
  
see also: [RAMTOP](../RAMTOP/index.md)  
