---
title: OS Versions
---
# How to find the OS Version of your computer  
## [Atari ROM Checker by JAC!](http://www.wudsn.com/productions/atari800/atariromchecker/help/AtariROMChecker.html)  
## For ATARI 400 and ATARI 800 Computers  
In Atari BASIC type the following command if you have an 400/800  
%%prettify  
```
PRINT PEEK(65528) 
```
/%  
and press the RETURN key  
  
||Value||OS Version||CRC 32||MD5||ROMs  
|255|First 800 OS NTSC ; please further see [Rarity_10](../Rarity_10/index.md)|?|?|__we are still searching for this. Please help us ;-)__  
|221|400/800 OS Rev. A NTSC|c1b3bb02|a3c1585b5d19719f8acfa2b093bea75f|CO12499A, CO14599A, CO12399B  
|214|400/800 OS Rev. A PAL|72b3fed4|eb1f32f5d9f382db1bbfb8d7f9cb343a|CO15199, CO15299, CO12399B  
|243|400/800 OS Rev. B NTSC|0e86d61d|4177f386a3bac989a981d3fe3388cb6c|CO12499B, CO14599B, 12399B  
|34|400/800 OS Rev. B PAL; please further see [Rarity_10](../Rarity_10/index.md)|0c913dfc|89d5e5f4713267667ab713449944f8a9 Kr0tki-Version|__we are still searching for this. Please help us ;-)__  
  
## For ATARI XL and XE Computers  
If you have an XL or XE Computer, type  
  
%%prettify  
```
PRINT PEEK(65527)
```
/%  
and press the RETURN key  
  
||Value||Version  
|10|XL/XE OS Rev 10  
|11|XL/XE OS Rev 11  
|1|XL/XE OS Rev 1  
|2|XL/XE OS Rev 2  
|3|XL/XE OS Rev 3  
|59|XL/XE OS Rev 3B (Arabic)  
|4|XL/XE OS Rev 4  
  
see also [How_to_find_the_revision_number_of_Atari_Basic](../How_to_find_the_revision_number_of_Atari_Basic/index.md)  
