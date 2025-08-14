General Information   
Author: CompyShop   
Assembler: Bibo Assembler   
Published: Bibo Assembler Toolkit Disk   
  
This routine reads the Print-Char Routines out of the Handler Tab of the "E:" Handler and pushed the Address to the Stack. The Return from Subroutine Command (RTS) uses this address to jump into the ROM <nop>PrintChar Routine. Because the Address will be read from the Handler Table, this routine works with all ATARI OS Versions.  
  
The ASCII Value of the Char is the Accu, X and Y registers will not be saved.  
  
Taken from the Bibo Assembler Toolkit Disk.  
  
(c) CompyShop (c) ABBUC e.V.  
  
```
00140 ------------------------------
00150 * PRINT CHAR TO SCREEN       *
00160 * CHAR IS PLACED IN <A> REG  *
00170 * <X> and <Y> WILL BE        *
00180 * DESTROYED                  *
00190 ------------------------------
00200 *
00210 PUTCHAR  TAX         SAVE CHAR
00220          LDA $E407   PUSH PRINT CHAR OS VECTOR
00230          PHA         ON STACK
00240          LDA $E406   
00250          PHA
00260          TXA         RECOVER CHAR
00270          RTS         JUMP TO ROM ROUTINE
00280 *
00290 ------------------------------
```
  
  
