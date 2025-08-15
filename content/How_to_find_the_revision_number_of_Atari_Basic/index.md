---
title: How to find the revision number of Atari Basic
---
# How to find the revision number of Atari Basic  
  
With the BASIC cartridge put into your 400/800 or BASIC switched on, type (e.g. after the READY prompt)  
  
%%prettify  
```
? PEEK(43234) 
```
/%  
  
and then press RETURN.  
  
The computer will give you an result.  
  
||Result||BASIC||Comment  
|162|Revision A|First Atari BASIC cartridge, 8K ROM.  
|96|Revision B|Found built-in on the 600XL and early 800XLs. Never supplied on cartridges.  
|234|Revision C|Found on later 800XLs, the 800XLF, XEGS and all XE computers. Limited cartridge production run.  
  
For an description of the known errors, see the Wikipedia Article on ATARI Basic:  
[https://en.wikipedia.org/wiki/Atari_BASIC](https://en.wikipedia.org/wiki/Atari_BASIC)  
  
  
See also [OS_Versions](../OS_Versions/index.md)  
