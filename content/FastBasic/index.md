# FastBasic  
Daniel Serpell (dsmc), June/July 2017  
  
### Background  
FastBasic is one of the newest BASICs for the Atari 8-bit platform. It is a complete re-implementation of the BASIC system, using a built-in bytecode compiler rather than a tokenizing interpreter.  
  
Typical BASICs use an interpreter that examines every line of code as the program runs. They do this because it minimizes the amount of RAM used; only one line of code is actively worked on so the amount of temporary memory required is small. To improve speed and memory usage, most BASICs "tokenize" the lines, replacing keywords with "tokens", typically a single byte. Atari BASIC does this when the line is entered, so, for instance, when it sees a {{PRINT}} in the line of code, it replaces this with a 32 (decimal), making the source more compact and easier to process when it's run. This process is reversed when you {{LIST}} the program, converting the 32 back into {{PRINT}} so you never even realize it happened. This is why, for instance, typing {{P.}} turns into {{PRINT}} when you later {{LIST}} it.  
  
In contrast, FastBasic works on an entirely different principle. When a line is parsed in FastBasic, it (essentially) compiles the entire line into tokens and then ''leaves them in memory''. This way the line does not have to be repeatedly parsed, even from the simplified token format, which makes it ''much'' faster to run. This generally requires more memory to store this format, but by using a compact notation this impact can be reduced, especially as the parser code can be made smaller. FastBasic is not a compiler, although it works in a similar fashion; a compiler would convert the code directly into machine language, FastBasic converts it to an intermediate bytecode format which can then be very quickly converted into the equivalent machine language at runtime. In this fashion it sits between the interpreter and compiler worlds, a concept also used in the p-code systems like the Berkeley p-System.  
  
FastBasic further improves performance with several other speed-ups. Among these is the inclusion of 16-bit and 8-bit arrays, which save memory and are faster to process. It also includes integer variables; in cases where the parser can determine that the entire math function is integer, the expensive floating-point math routines found in most BASICs are replaced by much simpler and faster bit-fiddling routines. FastBasic uses whatever floating-point library is found in the system, so code that does use floating-point routines can be further sped up with a replacement math ROM like FashChip or the libraries in Atari++ and Altirra.  
  
On top of this, FastBasic uses a new full-screen editor instead of the classic line-number based systems of the past. Line-number-based editing was invented because early video terminals could not scroll, so to edit a file you needed a way to refer to a given line of code. This is a problem that few (if any) of the home computers had, but by the time they arrived the line-number concept was too ingrained in MS BASIC for people to think outside that box. FastBasic does, and this makes editing far easier. Gone are the days of typing in long strings of numbers to delete lines or move code around, all of this is now done using the cursor controls, as it always should have been.  
  
FastBasic is a truly unique approach to the BASIC language on the Atari, a must-see program for everyone. AtariWiki deeply thanks dmsc from AtariAge for the license to publish his FastBasic here. Thank you dmsc, your help is very much appreciated. :-)  
  
  
## Latest release  
- [https://github.com/dmsc/fastbasic/releases](https://github.com/dmsc/fastbasic/releases) ; Home page for V3.4 from March 2018  
- [https://github.com/dmsc/fastbasic/releases/download/v3.4/fastbasic-v3.4.atr](https://github.com/dmsc/fastbasic/releases/download/v3.4/fastbasic-v3.4.atr) ; ATR image  
- [https://github.com/dmsc/fastbasic/archive/v3.4.zip](https://github.com/dmsc/fastbasic/archive/v3.4.zip) ; source code  
  
## Manual  
- [https://github.com/dmsc/fastbasic/blob/master/manual.md](https://github.com/dmsc/fastbasic/blob/master/manual.md)  
  
## Pictures  
![](attachments/fastbasic1.jpg)  
dmsc FastBasic - startscreen  
  
![](attachments/fastbasic2.jpg)  
dmsc FastBasic - 1st menu  
  
## References  
- [https://github.com/dmsc/fastbasic](https://github.com/dmsc/fastbasic) ; source site for FastBasic  
- [http://atariage.com/forums/topic/267929-fastbasic-beta-version-available/](http://atariage.com/forums/topic/267929-fastbasic-beta-version-available/) ; discussion about FastBasic on AtariAge  
