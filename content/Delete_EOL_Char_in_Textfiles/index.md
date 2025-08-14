# Delete EOL Char in Textfiles  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	27.04.90   
  
```
;********************************
;**									 **
;** Phoenix SoftCrew ACTION!	**
;**									 **
;********************************

; Programmname:EOL-Delete
; Programmierer:Carsten Strotmann
; Filename:EOLDEL.ACT
; first Version:27.04.90
; last change:27.04.90
; Task:delete EOL Char in Textfiles
;
;

INCLUDE "SYSTEM.ACT"

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

PROC Upper (BYTE ARRAY text)

  BYTE u

  FOR u=1 TO text(0)
  DO
	IF text(u)>$60 AND text(u)<$7B THEN
	 text(u)==-$20
	FI
  OD

RETURN

PROC C_On ()

BYTE crsin=752

crsin=0

RETURN

PROC C_Off ()

BYTE crsin=752

crsin=1

RETURN

PROC Del ()

 BYTE sd,dd,key
 CARD z

 BYTE ARRAY col(0)=708,sf(17),df(17),fn(17),buf(250)

 Graphics (0)

 col(1)=15
 col(2)=115

 Position (0,0)

 Print (" PhoeniX SoftCrew EOL-Delete (c) 1990")

 DO
  C_On ()

  Position (5,5)
  Print ("Source Disk :")
  sd=InputB ()

  Position (5,7)
  Print ("Dest.  Disk :")
  dd=InputB ()

  Position (5,10)
  Print ("Source File :")
  InputS (fn)
  Upper (fn)

  SCopy (sf,"D1:")
  sf(2)='0 + sd
  SAssign (sf,fn,4,4+fn(0))

  Position (5,12)
  Print ("Dest.  File :")
  InputS (fn)
  Upper (fn)

  SCopy (df,"D1:")
  df(2)='0 + dd
  SAssign (df,fn,4,4+fn(0))

  z=0

  C_Off ()
  Position (0,15)
  Print ("Work on Line	:")

  IF dd#sd THEN
	Close (1)
	Open (1,sf,4)
	Close (2)
	Open (2,df,8)
	DO
	 z==+1
	 InputSD (1,buf)
	 PrintD (2,buf)
	 PutD (2,$20)
	 Position (20,15)
	 PrintC (z)
	UNTIL EOF (1)#0
	OD
  FI

  Close (1)
  Close (2)

  Position (0,20)
  Print (" More Files ?")

  key=Inkey ()

 UNTIL key ='N or key='n
 OD

RETURN

```
