---
title: Ultimate Basic
---
# The Ultimate Basic  
  
### Background  
There are many versions of BASIC for the Atari platform, each of which corrects some of the problems in the original. Perhaps we should build The One BASIC to Rule Them All that includes every feature from the variety and represents the one BASIC to use for the future.  
  
Some of the main features would include:  
- completely compatible with Atari BASIC  
- LEFT/MID/RIGHT string handling to make porting of MS BASIC programs easier  
- caching of line numbers and loops from BASIC XL/TURBO which makes most programs much faster  
- a new floating point library that fixes the performance problems and produces correct output  
- additional graphics commands from practically everywhere  
- performance improvements in the OS drawing routines like Alitrra  
- additional memory management like BASIC XE  
  
Some of the nice-to-haves would include:  
- enhanced math functions like TAN(X), SINH(X) etc.  
- integer variables! these can save lots of memory in almost any program  
- an integer math pack, which builds on top of the item above for vastly improved performance  
- a new full-screen editor that allows scrolling instead of the constant LISTing now required  
- perhaps a new E: driver that goes with that editor  
- a FILL command instead of the XIO call  
- CIRCLE and ARC commands  
- a compiler  
- should be able to cope with 4 MiB RAM  
  
And some of the more esoteric concepts:  
- end-of-line loop constructs like those in BASIC-PLUS, one of the few features MS did not copy from that language. These simplify many common tasks and can improve both memory and performance.  
- BYTE variables, perhaps using a A! syntax. These would be useful in so many contexts.  
- LINE variables, perhaps A@, which are stored as integers but automatically pushed on the loop stack  
  
### Issues  
There are two solutions to the floating point problems in Atari BASIC. One, used by FastChip, Atari++ and Altirra, are fully compatible with the original implementation, and could be burned into a ROM replacement. The solution in TURBO-BASIC goes a step further; by "unwinding loops" it provides even faster speed for multiplication and division, but no longer fits in the original 2k ROM space. TURBO is faster, but has to include that code in the language itself.  
  
Another question is how far do we want to extend it? With modern bank-switching there's really no limit to the size of the language, while still using only 8k of memory at a time.  
  
## Pictures  
![](attachments/Crossbreeding.jpg)  
Ultimate Basic trough crossbreeding?  
  
## References  
- [http://atariage.com/forums/topic/259857-atari-ultimate-basic-through-crossbreeding/](http://atariage.com/forums/topic/259857-atari-ultimate-basic-through-crossbreeding/) ; discussion of Ultimate Basic on AtariAge  
