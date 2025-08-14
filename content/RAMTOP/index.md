||ADR||HEXADR||NAME||Description||OS  
|106|$006A|RAMTOP|RAM Size|both  
  
RAM size, defined by powerup as passed from [TRAMSZ](../TRAMSZ/index.md) (location 6), given in the total number of available pages (one page equals 256 bytes, so PEEK(106) * 256 will tell you where the Atari thinks the last usable address --byte-- of RAM is). [MEMTOP](../MEMTOP/index.md) (741,742; $2E5. $2E6) may not extend below this value. In a 48K Atari, [RAMTOP](../RAMTOP/index.md) is initialized to 160 ($A0), which points to location 40960 ($A000).  
  
The user's highest address will be one byte less than this value.  
This is initially the same value as in location 740. PEEK(740) / 4 or PEEK(106) / 4 gives the number of 1K blocks.  
  
You can fool the computer into thinking you have less memory than you actually have, thus reserving a relatively safe area for data (for your new character set or player/missile characters, for example) or machine language subroutines by:  
  
```
see also: [TRAMSZ], [MEMTOP]
```
