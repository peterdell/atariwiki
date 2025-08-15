---
title: Kyan Pascal Error $89 (137)
---
# Kyan Pascal Error $89 (137)  
  
DOS ERROR $89  
  
A few people, while compiling their Kyan Pascal programs, have  
come across an error message that reads:  
  
```
         pc: DOS error on file: D1:filename.p
         89 - Error code
```
  
This matches the DOS 2.5 error 89 (truncated) and happens when there are more than 256 characters including EOL on one line. So, if your source code e. g. has a large comment section, it should be broken into smaller groups. This is not a bug; it is just the way the Atari 8-bit computer works. Its I/O is limited to a record length of 256 bytes.  
