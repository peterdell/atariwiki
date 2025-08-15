---
title: ADRESS
---
||ADR||HEXADR||NAME||Description||shadow||OS  
|100,101|$0064,$0065|ADRESS| | |All  
  
  
Ein temporärer Speicher, der vom Bildschirm-Handler genutzt wird. Hier ein Anwendungsbeispiel in [Action!](../OS_Vectors/index.md)  
  
Temporary storage locations for the screen handler. Here is an example in [Action!](../OS_Vectors/index.md)  
  
```
PROC JMP =$F2AD ()

PROC Jump (CARD adr)

  CARD addr=$64
  addr=adr
  JMP ()

RETURN
```
