---
title: RUNAD
---
||ADR||HEXADR||NAME||OS  
|736,737|$02E0,$02E1|RUNAD|both  
  
Used by DOS for the run address read from the disk sector one or from a binary file. Upon completion of any binary load, control will normally be passed back to the DOS menu. However, DOS can be forced to pass control to any specific address by storing that address here. If RUNAD is set to 40960 ($A000), then the left cartridge (BASIC if inserted) will be called when the program is booted.  
  
With DOS 1.0, if you POKE the address of your binary load file here, the file will be automatically run upon using the DOS Binary Load (selection L).  
  
Using DOS 1.0's append (/A) option when saving a binary file to disk, you can cause the load address POKEd here to be saved with the data.  
  
In DOS 2.0, you may specify the initialization and the run address with the program name when you save it to disk (i.e., GAME.OBJ,2000,4FFF,4F00,4000). DOS 2.0 uses the /A option to merge files. In order to prevent your binary files from running automatically upon loading in DOS 2.0, use the /N appendage to  
the file name when loading the file.  
  
see also:  
[INITAD](../INITAD/index.md)  
