---
title: How to read a Key from Keyboard with ATARI ROM Routines
---
General Information   
Author: CompyShop   
Assembler: Bibo Assembler   
Published: Bibo Assembler Toolkit Disk   
  
This routine reads the Get-Char Routines out of the Handler Tab of the "E:" Handler and pushed the Address to the Stack. The Return from Subroutine Command (RTS) uses this address to jump into the ROM GetKey Routine. Because the Address will be read from the Handler Table, this routine works with all ATARI OS Versions.  
  
The ASCII Value of the Key will be in the Accu, X and Y registers will not be saved.  
  
Taken from the Bibo Assembler Toolkit Disk.  
  
(c) CompyShop  
(c) ABBUC e.V.  
  
  
Simple JSR to the "GetKey" Routine and use the returned value in Accu. The GetKEy Routine will block and wait for an Keypress.  
  
```
...
JSR GETKEY
...

```
  
  
```
00010 ------------------------------
00020 *  READ CHAR FROM KEYBOARD   *
00030 *  CHAR WILL BE IN THE       *
00040 *  <A> REGISTER              *
00050 *  <X>,<Y> will be destroyed *
00060 ------------------------------
00070 *
00080 GETKEY   LDA $E425   GET ADRESS-VECTOR
00090          PHA         FROM ROM HANDLER TAB
00100          LDA $E424   PLACE ADDRESS AS
00110          PHA         RETURN ADDRESS TO STACK
00120          RTS         JUMP TO ROM-ROUTINE
00130 *
```
