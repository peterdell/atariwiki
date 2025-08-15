---
title: CASSBT
---
||ADR||HEXADR||NAME||Description||shadow||OS  
|75|$004B|CASSBT|Cassette boot flag|none|A  
|1002|$03EA|CASSBT|Cassette boot flag|none|X  
  
The Atari attempts both a disk and a cassette boot simultaneously. Zero here means no cassette boot was successful. See location 9/$9 [BOOT](../BOOT/index.md)  
