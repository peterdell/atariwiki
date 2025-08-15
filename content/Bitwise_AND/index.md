---
title: Bitwise AND
---
# Bitwise AND for Kyan Pascal  
  
```
(* BITWISE AND, PD, Author:Michael P./WASEO/ABBUC 27.06.2007 *) 
FUNCTION BT_AND(B1,B2:INTEGER):INTEGER; 
BEGIN 
  BT_AND:=0; 
#A 
  LDY #9 ;OFFSET TO B1:L 
  LDA (_SP),Y ;BYTE 1 -> ACCU 
  STA _T ;BYTE 1 -> TEMP 
  LDY #7 ;OFFSET TO B2:L 
  LDA (_SP),Y ;BYTE 2 -> ACCU 
  AND _T ;B1 AND B2 -> ACCU 
  LDY #5 ;OFFSET F-RESULT:L 
  STA (_SP),Y ;STORE RESULT 
  LDY #6 ;OFFSET F-RESULT:H 
  LDA #0 
  STA (_SP),Y ;STORE 0 TO LSB OF RESULT 
# 
END;
   
```
  
