# Alfasm, Turbo-Assembler/16 ; Copyright (C) 1990 Jeff Williams and DataQue Software  
Alfasm, Turbo-Assembler/16 was written by Jeff Williams and is a two pass assembler for 6502 and 65816 processors  
  
A) Introduction:  
  
1) ALFASM is a full 65816 assembler, handling all opcodes and addressing modes.  
  
2) The assembler can handle files of any size, with a label capacity of 4096 labels currently (using a 256k 800XL).  
  
B) Running ALFASM:  
  
1) ALFASM will work under either SpartaDos or any Dos 2.x variant, such as MyDos, etc. The command line interface is only valid in the SpartaDos case, although it should also work under Dos XL.  
  
2) Simply load the file AA.COM.  
  
3) You will be prompted for the source filespec.  
  
a) The filespec is in the form D<n>:<path>FILENAME.EXT.  
b) The filespec must be in uppercase letters.  
c) The maximum filedspec length is 40 characters.  
  
4) The object file produced by the assembler will have the same primary name as the source, but the extender will be .COM.  
  
5) If a listing file isbeing produced, its extension will be .LST.  
  
## ATR image  
- [816ASM.atr](attachments/816ASM.atr)  
