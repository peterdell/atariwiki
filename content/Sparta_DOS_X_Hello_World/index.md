---
title: Sparta DOS X Hello World
---
# SDX Hello World  
  
General Information  
  
Author: trub / DLT Ltd.   
Assembler: masm   
Download: [http://trub.atari8.info](http://trub.atari8.info)  
  
The idea is to show an example how the SDX system libraries can be used dynamically. The code shows the way to call and use "PRINTF". Using this technique the resulting object file can be very small and 100% system compliant.  
  
```
PRINTF    smb 'PRINTF'

    blk reloc main

start    jsr PRINTF
    .byte $9b,'Hello world!',$9b,0

    jsr PRINTF
    .byte $9b,'My numbers:',$9b
    .byte '%b, %d, %x',$9b
    .byte '%e, %l',$9b,0
    .word bdec,wdec,whex,tdec,ldec
    rts

bdec    .byte $FF
wdec    .word $FFFF
whex    .word $FFFF
tdec    .long $FFFFFF
ldec    .word $FFFF,$FFFF 
```
