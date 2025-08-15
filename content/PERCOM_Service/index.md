---
title: PERCOM Service
---
# Percom Service  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	1991-2008   
  
Tool to configure Percom Block Drives. This Tool can be used to test Disk integrity and to format all kind of different Disk Formats available for Atari Disk Drives.  
  
![](attachments/percom.png)  
  
Download: [PERCOM.ATR](attachments/PERCOM.ATR)  
  
Needs ACTION! Runtime package to compile a standalone Version. Disk with Source and compiled Version attached.  
  
I wrote this Tool to configure the HDI 3 1/2" Disk drive designed by Erhard Pütz (aka FloppyDoc)  
  
### Changelog  
  
2008-01-13 disabled break key, custom error procedure, updated copyright  
  
## How to use  
  
  
|| Key	||  Description  ||  
| 1 - 4 | Read Percom Block from D1: - D4: and update display  |  
| T	  | change number of Tracks per Disc  |  
| S	  | change number of Sectors per Track  |  
| A	  | change modulation (FM or MFM)  |  
| R	  | change stepping rate  |  
| D	  | toggle doublesided <-> singlesides  |  
| B	  | change Bytes per Sectors (normally 128 or 256)  |  
| V	  | change Drive active Flag / HD flag |  
| CTRL+F | Format selected Disk in configured Format (CAUTION!!!)  |  
| CTRL+T | Read and Test all Sectors in configured Format, printing Status for each Sector |  
| CTRL+S | configure Drive for Atari Single Density, single sided (SS/SD)  |  
| CTRL+M | configure Drive for Atari Medium Density, single sided (SS/MD), 1050 Format  |  
| CTRL+D | configure Drive for Atari Double Density, single sided (SS/DD)  |  
| CTRL+H | configure Drive for Atari High Density, single sided (SS/HD)  |  
| CTRL+Z | configure Drive for Atari Single Density, double sided (DS/SD)  |  
| CTRL+Y | configure Drive for Atari Medium Density, double sided (DS/MD), 1050 Format  |  
| CTRL+X | configure Drive for Atari Double Density, double sided (DS/DD)  |  
| CTRL+V | configure Drive for Atari High Density, double sided (DS/HD)  |  
  
## Source  
  
### Main Program  
  
```
;********************************
;**				**
;** Phoenix SoftCrew ACTION!	**
;**				**
;** Carsten Strotmann		**
;** carsten@strotmann.de	**
;**				**
;** http://www.strotmann.de	**
;**				**
;********************************

; Programname:Percom Haendler
; Programmer:CAS
; Filename:PERCOM.ACT
; first Version:18.08.91
; last Change:13.01.08
; Usage:Manage Floppy Percom Block
;
;

INCLUDE "D:>WORK>SYSTEM.ACT"

MODULE

BYTE drivenum,err,p_read
CARD maxsec,bytes
BYTE ARRAY percom($C),buff($1000),txt(40),
			  sdss(12)=[40 2 0 18 0 0 0 $80 0 0 0 0],
			  sdds(12)=[40 2 0 18 1 0 0 $80 0 0 0 0],
			  mdss(12)=[40 2 0 26 0 4 0 $80 0 0 0 0],
			  mdds(12)=[40 2 0 26 1 4 0 $80 0 0 0 0],
			  ddss(12)=[40 2 0 18 0 4 1 0 0 0 0 0],
			  ddds(12)=[40 2 0 18 1 4 1 0 0 0 0 0],
			  hdss(12)=[80 2 0 36 0 4 1 0 0 0 0 0],
			  hdds(12)=[80 2 0 36 1 4 1 0 0 0 0 0]

INCLUDE "D:>WORK>PERCOM1.INC"

PROC PercError(BYTE err)
  ErrMess (err)
RETURN
  
PROC Read_Percom ()
 
 err=Sio (drivenum,$52,$40,7,buff,128,1)
 err=Sio (drivenum,$4E,$40,7,percom,12,0)
 ErrMess (err)
  
 maxsec=percom(0)*(percom(2)*$100+percom(3))
 maxsec==*(percom(4)+1)
 bytes =percom(6)*$100+percom(7)
 p_read=err

RETURN

PROC Write_Percom ()
 
 err=Sio (drivenum,$4F,$80,7,percom,12,0)
 ErrMess (err)
 
RETURN

PROC Format ()

 Write (20,10," Formatting ")
 err=Sio (drivenum,$21,$40,$40,buff,bytes,1)
 ErrMess (err)
 Write (20,10,"				")

RETURN

PROC Test()

 BYTE ARRAY t(8)
 BYTE ch=$2FC,consol=$D01F
 CARD u,b,s

 Write (18,11,"Test Sector  :")

 u=0
 
 SCopy (t,"000000")
 DO
  u==+1
  IF u<4 THEN
	b=$80
  ELSE
	b=bytes
  FI
  err=Sio (drivenum,$52,$40,$7,buff,b,u)
  t(6) == +1
  FOR s = 2 TO 6 
  DO
	IF t(s) > '9 THEN
	 t(s) = '0
	 t(s-1) == +1
	FI
  OD
  Write (32,11,t)
  IF err # 1 THEN
	ErrMess (err)
  FI
 UNTIL u=maxsec OR ch=28 or consol=6
 OD

 Pause (200)
 ch=$FF
 Write (18,11,"							 ")

RETURN
 
PROC Mask ()

 BYTE lmarg=82
 CARD savmsc=$58

 lmarg=0

 SetBlock (savmsc+120,240,0)
 
 Position (0,0)
 Print ("	PhoeniX SoftCrew Percom Service 1.1  ")

 Position (1,2)
 Print ("Drive #	 ")
 
 Position (1,3)
 Print ("Sectors  :")

 Position (20,3)
 Print ("KBytes :")

 Position (1,5)
 Print ("Tracks  :")

 Position (18,5)
 Print ("Steprate		  :")

 Position (1,6)
 Print ("Sectors :")

 Position (18,6)
 Print ("Doubleside		:")

 Position (1,7)
 Print ("Modulat.:")

 Position (18,7)
 Print ("Bytes p. Sector :")

 Position (1,8)
 Print ("Drive active :")

 Position (1,10)
 Print ("^Format		")

 Position (1,11)
 Print ("^Test Disc ")

 Position (1,13)
 Print ("^Single Density 1S")
 Position (23,13)
 Print ("^Z Sgl. Dens. 2S")

 Position (1,14)
 Print ("^Medium Density 1S")
 Position (23,14)
 Print ("^Y Med. Dens. 2S")
 
 Position (1,15)
 Print ("^Double Density 1S")
 Position (23,15)
 Print ("^X Dbl. Dens. 2S")
 
 Position (1,16)
 Print ("^High	Density 1S")
 Position (23,16)
 Print ("^V Hgh. Dens. 2S")

 Write (0,23,"	 (c) 1991-06  PhoeniX SoftCrew			")

RETURN

PROC Fill_Mask ()

 CARD c

 Mask ()

 Position (13,2)
 PrintB (drivenum)

 Position (13,3)
 PrintC (maxsec)
 
 Position (30,3)
 c=$400/bytes
 PrintC (maxsec/c)

 Position (11,5)
 PrintB (percom(0))

 Position (35,5)
 PrintB (percom(1))

 Position (11,6)
 c=percom(2)*$100+percom(3)
 PrintC (c)

 Position (35,6)
 IF percom(4)=1 THEN
  Print ("Yes ")
 ELSE
  Print ("No  ")
 FI

 Position (11,7)
 IF percom(5)=0 THEN
  Print ("FM ")
 FI
 IF percom(5)=4 THEN
  Print ("MFM")
 FI

 Position (35,7)
 c=percom(6)*$100+percom(7)
 PrintC (c)

 Position (18,8)
 IF percom(8)=$FF THEN
  Print ("Normal")
 FI
 IF percom(8)=$40 THEN
  Print ("HD	 ")
 FI

RETURN

PROC Refresh ()

 Write_Percom ()
 Read_Percom ()
 Fill_Mask ()

RETURN
 
PROC Test_Form ()

BYTE skstat=$D20F

 IF (skstat & 8) = 0 THEN
  Format ()
 FI

RETURN

PROC Percom_Service ()

 BYTE key 
 BYTE ARRAY value (3)
 CARD temperr 

 BreakOff()
 temperr = Error
 Error   = PercError

 drivenum = 1
 p_read=$FF
 MoveBlock (percom,sdss,12)

 Put (125)
 C_Off ()
 Mask ()
 
 DO
  key=Inkey ()

  IF key<'5 AND key>'0 THEN
   drivenum=key-48
   Read_Percom ()
   Refresh ()
  FI

  IF key='T OR key='t THEN
   StrB (percom(0),value)
   Position (11,5)
   GetIn (value,2)
   percom(0)=ValB(value)
   Refresh ()
  FI

  IF key='R OR key='r THEN
   StrB (percom(1),value)
   Position (35,5)
   GetIn (value,2)
   percom(1)=ValB(value)
   Refresh ()
  FI

  IF key='S OR key='s THEN
   StrC (percom(2)*$100+percom(3),value)
   Position (11,6)
   GetIn (value,5)
   percom(2)=ValC(value)/$100
   percom(3)=ValB(value)
   Refresh ()
  FI

  IF key='D or key='d THEN
   percom(4)==XOR 1
   Refresh ()
  FI

  IF key='A or key='a THEN
   percom(5)==XOR 4
   Refresh ()
  FI

  IF key='B OR key='b THEN
   StrC (percom(6)*$100+percom(7),value)
   Position (35,7)
   GetIn (value,4)
   percom(6)=ValC(value)/$100
   percom(7)=ValB(value)
   Refresh ()
  FI

  IF key='V or Key='v THEN
   IF percom(8)=$FF THEN 
    percom(8)=$40
   ELSE
    percom(8)=$FF
   FI
   Refresh ()
  FI

  IF key>='! AND key<='$ THEN
   drivenum=key-32
   Refresh ()
  FI

  IF key=' THEN
   Read_Percom ()
   Fill_Mask ()
   Test ()
  FI

  IF key=' THEN
   MoveBlock (percom,sdss,12)
   Refresh ()
   Test_Form ()
  FI

  IF key=' THEN
   MoveBlock (percom,sdds,12)
   Refresh ()
   Test_Form ()
  FI

  IF key=' THEN
   MoveBlock (percom,mdss,12)
   Refresh ()
   Test_Form ()
  FI

  IF key=' THEN
   MoveBlock (percom,mdds,12)
   Refresh ()
   Test_Form ()
  FI

  IF key=' THEN
   MoveBlock (percom,ddss,12)
   Refresh ()
   Test_Form ()
  FI

  IF key=' THEN
   MoveBlock (percom,ddds,12)
   Refresh ()
   Test_Form ()
  FI

  IF key=' THEN
   MoveBlock (percom,hdss,12)
   Refresh ()
   Test_Form ()
  FI

  IF key=' THEN
   MoveBlock (percom,hdds,12)
   Refresh ()
   Test_Form ()
  FI

  IF key='  THEN
   Format ()
  FI

 UNTIL key='q OR key='Q or key=27
 OD

 C_On ()
 Error = temperr
 BreakOn()

RETURN
```
  
### Percom Tool Include Library  
  
```
; Includedatei fuer PERCOM.ACT
;---

PROC siov=$E459 ()

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

;---

PROC C_On ()

BYTE crsin=752

crsin=0

RETURN

PROC C_Off ()

BYTE crsin=752

crsin=1

RETURN

BYTE FUNC Inkey ()

BYTE atascii

 Close (2)
 Open (2,"K:",4,0)
 atascii=GetD(2)
 Close(2)

RETURN (atascii)

PROC Pause (CARD times)

BYTE wsync=$14,q
CARD u

FOR u=1 TO times
DO
  FOR q=1 TO 200
  DO
	wsync=q
  OD
OD

RETURN

PROC Beep (BYTE times)

BYTE u

FOR u= 1 TO times
DO
  PutD (0,253)
  Pause (10)
OD

RETURN

PROC Getin (BYTE ARRAY text,BYTE len)

  BYTE ascii,pos,u,inv,ch=764

  C_On ()
  ch=$FF

  pos=text(0)+1
  inv=0

  IF text(0)#0 THEN
	Print (text)
  FI

  DO
	ascii=Inkey ()

	IF ascii=129 THEN
	 inv==!$80
	FI
	IF ascii=$1E AND pos>1 THEN
	 pos==-1
	 PutD (0,$1E)
	FI
	IF ascii=$7E AND pos>1 THEN
	 pos==-1
	 PutD (0,$7E)
	FI
	IF ascii=$1F AND pos#len+1 THEN
	 pos==+1
	 PutD (0,$1F)
	FI 
	IF ascii>26 AND ascii<32 THEN
	 ascii=128
	FI
	IF pos#len+1 AND ascii<$7E THEN
	 ascii==+inv
	 PutD (0,ascii)
	 text(pos)=ascii
	 pos==+1
	FI
	text(0)=pos-1
  UNTIL ascii=$9B
  OD

  C_Off ()
  Put (31)
RETURN

PROC Write (BYTE x,y,BYTE ARRAY string)

  BYTE u,chr
  CARD savmsc=$58
  BYTE POINTER adr

  adr=savmsc+y*40+x

  FOR u=1 TO string(0)
  DO
	chr=string(u)
	IF chr>=0 AND chr<32 THEN
	 chr==+64
	ELSEIF chr>31 AND chr<95 THEN
	 chr==-32
	ELSEIF chr>127 AND chr<160 THEN
	 chr==+64
	ELSEiF chr>159 AND chr<224 THEN
	 chr==-32
	FI
	adr^=chr
	adr==+1
  OD
RETURN

;-----------------------------------

PROC ErrMess (BYTE err)

 Write (10,20,"Status - ")
 StrB(err,txt)
 Write (20,20,"	")
 Write (20,20,txt)
 IF err>$7F THEN
  Write (25,20," ERROR ")
 ELSE
  Write (25,20,"OK	  ") 
 FI
RETURN

PROC BreakOff()
  BYTE POKMSK = $10
  BYTE IRQEN  = $D20E
  POKMSK ==& $7F
  IRQEN  ==& $7F
RETURN
 
PROC BreakOn()
  BYTE POKMSK = $10
  BYTE IRQEN  = $D20E
  POKMSK ==% $80
  IRQEN  ==% $80
RETURN


```
