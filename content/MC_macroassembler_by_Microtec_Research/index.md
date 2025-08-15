---
title: MC macroassembler by Microtec Research
---
# MC macroassembler by Microtec Research  
The MC macroassembler by Microtec Research is often found in Atari source code listings, therefore it was at least used by Atari, Inc.  
  
There are 2 EXE files:  
  
MCASM.EXE  
  
and  
  
MCLINK.EXE  
  
## EXE files  
- [MC.zip](attachments/MC.zip)  
  
## References  
---
  
Usage: \[options\] \[sourcefile[[ \]]  
  
Options are ("-" - disable, "+" or none - enable):  
  
/D\[+|-\]    - place or not debug info in the file (default is /D+)  
/W\[+|-\]    - enable or not warning messages (default is /W+)  
/L\[+|-\]    - generate or not the file (default is /L+)  
/T\[+|-\]    - swap or not the file to disk (default is /T-)  
/Mnnnn      - restrict macro recursion depth (default is /M100)  
/Rnnnn      - restrict repeat block repetitions (default is /R500)  
/Ix;x;...   - assign include directories  
/Ox         - assign object directory  
/Zx         - assign temporary directory (has no effect with /T-)  
/Kn         - assign COM port (1-4) for key device (default is /K1)  
/H or /?    - show this information  
  
Command line argument order and case are both don't care.  
Missing source file will be prompted.  
