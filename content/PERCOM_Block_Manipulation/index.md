---
title: PERCOM Block Manipulation
---
# Percom Block  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
  
```
;******************************
;**								  **
;** PHOENIX SOFTCREW			**
;** STANDARTROUTINEN			**
;** IO "IO.INC"				  **
;******************************

MODULE
BYTE track,stp,side,dens,stat,rate,x1,x2,drive
CARD sect,byt
BYTE ARRAY buffer($200)


BYTE FUNC Inkey ()

  BYTE atascii=$2FB,chasci=$2FC
  BYTE POINTER keydefp
  CARD keydef=$79

  chasci=$FF
  keydefp=keydef

  DO
  ;
  UNTIL chasci#$FF
  OD

  keydefp==+chasci
  atascii=keydefp^
  chasci=$FF

RETURN (atascii)


PROC siov=$E459 ()

;-------------------------------------

BYTE FUNC Sio (BYTE num,comnd,stats,tim,CARD buf,byt,sec)

BYTE ddevic=$300,
	  dunit=$301,
	  dcomnd=$302,
	  dstats=$303,
	  dtimlo=$306

CARD dbuf=$304,
	  dbyt=$308,
	  daux=$30A

ddevic=$31
dunit=num
dcomnd=comnd
dstats=stats
dtimlo=tim
dbuf=buf
dbyt=byt
daux=sec

siov () ; ansprung der sioroutine

RETURN (dstats)

;----------------------------------

PROC ReadPerc (BYTE drive)

BYTE ARRAY P_Block (12)

 Sio (drive,$4E,$40,7,P_Block,$C,1)

 track=P_Block(0)
 stp  =P_Block(1)
 sect  =P_Block(2)*$100+P_Block(3)
 side =P_Block(4)
 dens =P_Block(5)
 byt  =P_Block(6)*$100+P_Block(7)
 stat =P_Block(8)
 rate =P_Block(9)
 x1	=P_Block($A)
 x2	=P_Block($B)

RETURN

PROC ShowPerc ()

 ReadPerc (drive)

 Print ("Track :")
 PrintBE (track)
 Print ("Step :")
 PrintBE (stp)
 Print ("Sides :")
 PrintBE (side)
 Print ("Density :")
 PrintBE (dens)
 Print ("Status :")
 PrintBE (stat)
 Print ("Transfer rate :")
 PrintBE (rate)
 Print ("X1 :")
 PrintBE (x1)
 Print ("X2 :")
 PrintBE (x2)
 Print ("Sectoren :")
 PrintCE (sect)
 Print ("Bytes pro Sec :")
 PrintCE (byt)
 PutE ()

RETURN

PROC Convert ()

BYTE u

 FOR u=1 TO $F0
 DO
  buffer(u)==-191
 OD

RETURN

PROC ReadSec ()

BYTE drive=[1],tr,sec
CARD smadr=$58,zaehl

 ReadPerc (drive)
 sec=7
 tr=0

 DO

  Inkey ()

  sec==+1

  IF sec=10 THEN
	sec=1
	tr==+1
  FI

  zaehl=tr*18+sec

  Print ("} Sector :")
  PrintCE (zaehl)

  Sio (drive,$52,$40,7,buffer,byt,zaehl)

  Convert ()

;  MoveBlock (smadr+80,buffer,$100)
  Print (buffer)

 UNTIL zaehl=1024
 OD

RETURN
```
