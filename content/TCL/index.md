# TCL - Test Computer Language (TCL) ; Copyright (C) 1985-1990 by David Firth  
![](attachments/TCL.png)  
Test Computer Language, Version 2.2  
  
This language has been designed for the programmer with an in-depth knowledge of ATARI's 8 bit computers. It may also be useful to know a little 6502 machine code in order to extend the functionality of the language via user defined functions and procedures.  
  
This language will also be of use to somebody just starting to learn 6502 machine code as small (or large) machine code routines may be incorporated directly within TCL programs themselves.  
  
The language was written as an exercise by the author himself. It currently works with DOS XL by just entering TCL and hitting return. It should work with other DOS systems, but it may be necessary to specify the run address for yourself. The run address is $2600.  
  
There are probably many errors contained within this document since it was last updated long before the last version of the compiler in 1986. The author has updated a few areas he knew were wrong, but he may have probably missed some bits.  
  
If the reader has any problems or queries regarding this documentation, please send an e-mail to the author and he will find the answer and update this guide.  
  
## ATR images  
- [TCL.atr](attachments/TCL.atr) ; TCL computer language with SpartaDOS 3.2g  
- [TCL-SOURCE-original.atr](attachments/TCL-SOURCE-original.atr) ; original source code with SpartaDOS 3.2g ; 720 KiB image  
- [TCL-SOURCE_CODE_with_OSS_DOS_XL_2.30p_DD.atr](attachments/TCL-SOURCE_CODE_with_OSS_DOS_XL_2.30p_DD.atr) ; original source code with OSS DOS XL 2.30p DD ; 180 KiB image  
  
## Manual  
- [TCL.pdf](attachments/TCL.pdf)  
  
## Source Code  
Boot TCL-SOURCE.ATR without BASIC from above  
LOAD MAC65  
LOAD #D:LANGUAGE.M65  
ASM,,#D:TCL.COM  
  
## Example  
![](attachments/TCL-Example3.png)  
Colour program in TCL source code  
  
## Pictures  
![](attachments/TCL-Breakout3.png)  
Break Out in TCL - picture 1  
  
![](attachments/TCL-Breakout4.png)  
Break Out in TCL - picture 2  
  
## Reference  
- [TCL on AtariAge](https://atariage.com/forums/topic/269553-test-computer-language-version-22-from-d-firth) ; Thank you so much for your help David Firth, we are deep in your debt! A great thank you from the Atari community worldwide!  
