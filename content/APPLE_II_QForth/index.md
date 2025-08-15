---
title: APPLE II QForth
---
# APPLE II QForth  
  
QForth 2.2 is an updated version of Toshiyasu Morita's original.  QForth is a small integer Forth for Apple IIe/IIc/IIgs computers.  It will not work with an Apple II+.  Unlike most Apple Forths, QForth uses normal ProDOS text files for source input.  It also has ProDOS file support as well as block disk access.  Version 2.2 fixes a couple of small bugs, adds about ten new words to extend the language, and alters the interpreter to suit my tastes.  
  
Source: [http://www.dwheeler.com/6502/oneelkruns/qforth.html](http://www.dwheeler.com/6502/oneelkruns/qforth.html)  
  
## Source Code Notice  
  
  
__A note about QForth__  
  
The source code for the original Apple IIe version of QForth is given here:  
  
  
- QFORTH.S           --   main code for the interpreter/compiler  
- QF.REGWRDS1.S      --   standard predefined words  
- QF.REGWRDS2.S  
- QF.SPCWRDS1.S      --   compiler words  
- QF.SPCWRDS2.S  
- QF.FILESYS         --   ProDOS file access words  
  
  
I have no idea as to what Apple II assembler you need to assemble this  
code yourself, but imagine that it would not be hard to port.  
  
  
  
__AN IMPORTANT NOTE__  
  
The file QF.FILESYS.S contained an error that prevented using file  
numbers 1 and 2.  The error has been corrected in this copy of the file  
and in the version running within MacQForth.  If you want to work with  
the original Apple version and cannot re-assemble the file, patch the  
locations below:  
```
$3C79:A2
$3C7A:9E
```
  
This can be accomplished by using a disk sector editor and careful  
counting (the original values in these locations are zero).  Less daring  
types can use QForth itself:  
  
```
162 15481 c!  158 15482 c!
```
  
__Where's the original?__  
  
The original Apple II version of QForth can be found at:  
  
ftp.cco.caltech.edu  as  /pub/apple2/8bit/comm/qforth8.shk  
  
You will need ShrinkIt to expand the archive.  ShrinkIt is also available  
on ftp.cco.caltech.edu.  
  
  
  
  
  
  
  
  
