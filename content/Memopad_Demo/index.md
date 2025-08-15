---
title: Memopad Demo
---
# Memopad Demo  
  
```
00010          .LI OFF
00020          .OR $4000
00030 *
00040 *
00050 *
00060 *
00070 *
00080 *
00090 MEMO     JSR GETKEY    ZEICHEN LESEN
00100          CMP #$1b      WENN ESCAPE
00110          BNE ZOUT      RUECKKEHR ZUM
00120          RTS           ASSEMBLER
00130 *
00140 ZOUT     JSR PUTCHAR   SONST AUSGEBEN
00150          JMP MEMO      ENDLOS WIEDERHOLEN
00160 ------------------------------
00170          .IN "D:INOUT.INC"
```
