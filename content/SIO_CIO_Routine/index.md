---
title: SIO CIO Routine
---
# SIO CIO Routine  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
  
```
;******************************
;**	                     **
;** PHOENIX SOFTCREW	     **
;** IO Routines		     **
;** IO "IO.INC"		     **
;******************************

MODULE
BYTE CIO_status

;-----------------------------------

CHAR FUNC CIOQ=*(BYTE dev, CARD addr,
			 size, BYTE cmd, aux1, aux2)
[$29$F$85$A0$86$A1$A$A$A$A$AA$A5$A5
$9D$342$A5$A3$9D$348$A5$A4$9D$349
$A5$A6$F0$8$9D$34A$A5$A7$9D$34B$98
$9D$345$A5$A1$9D$344$20$E456
$8C CIO_status$C0$88$D0$6$98$A4$A0
$99 EOF$A085$60]

;-----------------------------------

CARD FUNC Bget=*(BYTE dev,
						  CARD addr, size)
[$48$A9$7$85$A5$A9$0$85$A6$A5$A3$5$A4
$D0$6$85$A0$85$A1$68$60$68$20 CIOQ
$BD$348$85$A0$BD$349$85$A1$60]

;-----------------------------------

PROC BPut=*(BYTE dev,
						  CARD addr, size)
[$48$A9$B$85$A5$A9$0$85$A6$A5$A3$5$A4
$D0$2$68$60$68$4C CIOQ]

;-----------------------------------

PROC PutCD=*(BYTE chan, CARD n)
  BYTE c=$AA, lo=$AB, hi=$AC

  [
	 $85 c
	 $86 lo
	 $84 hi
  ]

  CIOQ(c,lo,0,11,0)
  CIOQ(c,hi,0,11,0)
RETURN

;-----------------------------------

CARD FUNC GetCD(BYTE chan)
  CARD out
  BYTE lo=out, hi=out+1

  lo = CIOQ(chan,0,0,7,0)
  hi = CIOQ(chan,0,0,7,0)
RETURN(out)

;-----------------------------------

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

siov () ; Jump through SIO Vector

RETURN (dstats)

;----------------------------------
```
