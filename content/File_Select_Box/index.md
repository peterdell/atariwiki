# File Select Box  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	13.02.90   
  
```
;********************************
;** Fileselect Box				 **
;** PHOENIX SOFTCREW 1990		**
;** 13.02.90						 **
;**				  "FILESEL.ACT" **
;********************************

PROC Filesel (BYTE ARRAY file)

  BYTE pos,num,u,arrow
  BYTE ARRAY dirbuf (1200),dev(20)

  MoveBlock (dev,file,4)
  SetBlock (dirbuf,1200,32)
  Close (1)
  Open (1,file,6,0)
  
  pos=0
  num=0
  arrow=0

  DO
	InputSD (1,file)
	IF file(2)=32 THEN
	 MoveBlock (dirbuf+num*17,file+1,17)
	FI
	num==+1
  UNTIL file(2)#32
  OD

  Close (1)
  C_Off ()
  Position (10,10)
  Print ("---------------")
  FOR u=11 TO 15
  DO
	Position (10,u)
	Print ("|				 |")
  OD
  Position (10,16)
  Print ("---------------")
  Position (10,17)
  Print ("| ")
  file(0)=4
  Print (file)
  Print (" Free")
  Position (24,17)
  Print ("|")	  
  Position (10,18)
  Print ("---------------")
  Position (10,19)
  Print ("|				 |")
  Position (10,20)
  Print ("---------------")

  DO
	FOR u=0 TO 4
	DO
	 MoveBlock (file+1,dirbuf+(pos+u)*17+2,8)
	 file(9)='.
	 MoveBlock (file+10,dirbuf+(pos+u)*17+10,3)
	 file(0)=12
	 Position (12,u+11)
	 Print (file)
	OD
	Position (11,11+arrow)
	Print (">")
	u=Inkey ()
	IF u=$2D THEN
	 IF arrow>0 THEN 
	  Position (11,11+arrow)
	  Print (" ")
	  arrow==-1
	 ELSEIF pos>0 THEN
	  pos==-1
	 FI
	FI
	IF u=$3D THEN
	 IF arrow<4 THEN
	  Position (11,11+arrow)
	  Print (" ")
	  arrow==+1
	 ELSEIF pos<num-6 THEN
	  pos==+1
	 FI
	FI
  UNTIL u=155
  OD

  MoveBlock (file+1,dirbuf+(pos+arrow)*17+2,8)
  file(0)=8
  u=Find (" ",file)
  IF u=0 THEN
	u=9
  FI
  file(u)='.
  file(0)=u+3
  MoveBlock (file+u+1,dirbuf+(pos+arrow)*17+10,3)
  Position (11,19)
  C_On ()
  Print (file)
  Getin (file,12)  
  Upper (file)
  MoveBlock (dev+4,file+1,12)
  MoveBlock (file,dev,16)
  file(0)=16
  u=Find (".",file)
  file(0)=u+3

RETURN
```
