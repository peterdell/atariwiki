---
title: Binary File Load in ACTION
---
General Information   
Author: 	Carsten Strotmann & Matthias Drees   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	19.02.90   
  
```
;********************************
;**									 **
;** Phoenix SoftCrew ACTION!	**
;** Programme und Tips f. 8Bit **
;**									 **
;** Carsten Strotmann			 **
;**									 **
;********************************

; Programmname:BLOAD
; Programmierer:CARSTEN STROTMANN/MATTHIAS DREES
; Filename:BLOAD.ACT
; first Version:19.02.90
; last Aenderung:19.02.90
; load COMFILES
; Comment:MC-CODE
;
;


PROC Bload =$0600 ()

PROC Bload_Init ()

  BYTE ARRAY mc ($8C)=[ $4C $3D $06 $A0 $F0
	 $A2 $06 $8C $54 $03 $8E $55 $03 $A8 $A2 00
	 $8C $58 $03 $8E $59 $03 $A9 $07 $8D $52 $03 
	 $A2 $10 $4C $56 $E4 $38 $ED $F2 $06 $A8
	 $8A $ED $F3 $06 $AA $C8 $D0 $01 $E8 $AD $F2 $06
	 $8D $54 $03 $AD $F3 $06 $8D $55 $03 $4C $10 $06
	 $A9 $00 $8D $F2 $06 $8D $F3 $06 $AD $44 $03
	 $C9 $E2 $D0 $07 $AD $45 $03 $C9 $02 $F0 $34 $A9 $02
	 $20 $03 $06 $30 $2D $A9 $FF $CD $F0 $06
	 $D0 $05 $CD $F1 $06 $F0 $DF $AD $F0 $06
	 $AE $F1 $06 $8D $F2 $06 $8E $F3 $06
	 $A9 $02 $20 $03 $06 $30 $0E $AD $F0 $06
	 $AE $F1 $06 $20 $20 $06 $10 $C1 $6C $E0 $02
	 $6C $E2 $02 $60 $00]

  MoveBlock ($0600,mc,$8A)

 RETURN
```
  
  
1.1 Another Version  
  
```
; This fragment loads an Action!
;  program and executes it
;  (thru INITAD).  This fragment can be
;  easily modified to support any type
;  of binary load file by checking the
;  status of INITAD and RUNAD after
;  each block of code has been loaded.
; If you want this fragment to remain
;  resident, you must compile to a
;  specific location (outside your own
;  program, obviously) using either the
;  SET $E/SET $491 method or using
;  SET $B5 to set a compilation offset
;  (Note: due to a bug in the Action!
;  compiler offset routine, you can
;  only specify a positive offset)
; Once the program is compiled, type:
;		?Load
;  from the monitor to obtain the
;  runtime address.  In your own source
;  that calls Load, you must insert the
;  following line before its use:
;		PROC Load=$xxxx(CHAR ARRAY str)
;  where "$xxxx" is the address you
;  found above, and where the CHAR
;  ARRAY "str" is the complete filespec
;  of the program you want to load.


MODULE ;LOAD.ACT

BYTE
  CIO_status

CARD
  start,
  len

; NOTE: CIO and ReadBlock are
;  copyrighted routines of
;  Action! computer services
;  Credit such as this of their origin
;  must be given if used in your own
;  program source
CHAR FUNC CIO=*(BYTE dev, CARD addr,size, BYTE cmd,aux1,aux2)
 [$29$F$85$A0$86$A1$A$A$A$A$AA$A5$A5$9D$342$A5$A3$9D$348$A5$A4$9D$349$A5$A6$F0$8$9D$34A$A5$A7$9D$34B$98$9D$345
  $A5$A1$9D$344$20$E456$8C CIO_status$C0$88$D0$6$98$A4$A0$99 EOF$60]
CARD FUNC ReadBlock=*(BYTE dev, CARD addr, size)
 [$48$A9$7$85$A5$A9$0$85$A6$A5$A3$5$A4$D0$6$85$A0$85$A1$68$60$68$20 CIO$BD$348$85$A0$BD$349$85$A1$60]


; MAINLINE ****************************

CARD FUNC GetOne()
BYTE
  cLow
CARD
  cHigh

  DO
	 cLow=GetD(1) cHigh=GetD(1)
	 cHigh== LSH 8 % cLow
  UNTIL cHigh#$FFFF OD
RETURN(cHigh)


PROC GetAddrs=*()
  start=GetOne()
  len=GetOne()-start+1
RETURN


PROC Load(CHAR ARRAY filespec)
CARD
  INITAD=$2E2

  Close(1)
  Open(1,filespec,4,0)

  WHILE start#$2E2 DO
	 GetAddrs()
	 ReadBlock(1,start,len)
  OD
  Close(1)
  [$6C INITAD]
RETURN
```
