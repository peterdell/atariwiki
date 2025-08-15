---
title: GNU Forth EC for 6502
---
# GnuFORTH EC  
  
the embedded control version of the ANS-Forth standards based GNU-Forth implementation  
  
# History (from GFORTH EC Homepage)  
  
Since 1994 there has existed a very flexible cross-compiler concept in GForth. There are no ?PC-limitations? (meaning the cross-compiler runs in every memory model) to it, it's plain ANSForth, and it creates choosable 16, 32 and 64 Bit targets in little or big endian. This was needed to support a wide range of target platforms (even DEC's Alpha for example).  
  
The difference to other forth-systems and GForth was, that the primitives were created by a C compiler. We used GNU C because we could not build a real "next" with ANSI C.  
  
On desktop-computer CPUs there is not much difference between hand-coded primitives and the generated code of a C-Compiler, so this was an easy way of making the system capable of runnung on a wide range of target platforms.  
Due to the flexible cross-compiler it was easy to use real assembler primitives instead of C. But there were problems, too: During the years GForth has migrated to a big 'PC-forth'-system, so some work was necessary work to strip down the system.  
  
# Target  
  
| MISC | Ready! |  
| 6502 | Ready! |  
| C165 | in development |  
| PSC1000 | in development |  
| 8086  | in development |  
  
# Resources  
  
- [GnuFORTH Homepage @ GNU](http://www.gnu.org/software/gforth/gforth.html)  
- [GForth Homepage](http://www.jwdt.com/~paysan/gforth.html)  
  
