---
title: Fast Graphics 8 Routines
---
# Fast Graphics 8  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	09.12.90   
  
  
  
```
;********************************
;**									 **
;** Phoenix SoftCrew ACTION!	**
;**									 **
;********************************

; Programname:GR8.FAST POINT
; Programmer:CARSTEN STROTMANN
; Filename:GR8.ACT
; first Version:09.12.90
; last chnage:09.12.90
; Task:fast graphics 8 Routines
;
;


PROC Pixel=$2006 (CARD x,BYTE y)

PROC Shp=$2003 (CARD x,BYTE y)

PROC Shape (CARD x,BYTE y)

 IF x>319 THEN
  x=319
 FI
 IF y>191 THEN
  y=191
 FI

 Shp (x,y)

RETURN

PROC Line (CARD x1,y1,x2,y2)
INT fx,fy
CARD dx,dy,ful,rst,x,y,z,a,u

fx=1
fy=1
dx=x2-x1
dy=y2-y1

IF y1>y2 THEN
 dy=y1-y2
 fy=-1
FI

IF x1>x2 THEN
 dx=x1-x2
 fx=-1
FI

IF dx>dy THEN
 ful=dx/dy
 rst=dx MOD dy
 z=0
 x=x1
 y=y1
 
 DO
  z==+rst
  IF z>=dy THEN
	z==-dy
	a=ful+1
  ELSE
	a=ful
  FI
  FOR u=1 TO a
  DO 
	x==+fx
	Pixel (x,y)
  OD
  y==+fy
 UNTIL y=y2
 OD
ELSE
 ful=dy/dx
 rst=dy MOD dx
 z=0
 y=y1
 x=x1
 y=y1
 
 DO
  z==+rst
  IF z>=dx THEN
	z==-dx
	a=ful+1
  ELSE
	a=ful
  FI
  FOR u=1 TO a
  DO 
	y==+fy
	Pixel (x,y)
  OD
 x==+fx
 UNTIL x=x2
 OD
FI

RETURN

PROC HLine (CARD y,x1,x2)

CARD x

IF x1>x2 THEN
 x=x2
 x2=x1
 x1=x
FI

FOR x=x1 TO x2
DO
 Pixel (x,y)
OD

RETURN

PROC VLine (INT x,y1,y2)

BYTE y,r
CARD savmsc=$58
BYTE POINTER adr
BYTE ARRAY bit(7)=[128 64 32 16 8 4 2 1]

IF y1>191 THEN y1=191 FI
IF y2>191 THEN y2=191 FI
IF x>319 THEN x=319 FI
IF x<0 THEN x=0 FI
IF y1<0 THEN y1=0 FI
IF y2<0 THEN y2=0 FI

IF y1>y2 THEN
 y=y2
 y2=y1
 y1=y
FI

adr=y1*40+savmsc+(x/8)

r=x & 7

FOR y=y1 TO y2
DO
 IF y<191 THEN
  IF color=1 THEN
	adr^==%bit(r)
  ELSE
	adr^==!bit(r)
  FI
  adr==+40
 FI
OD

RETURN

PROC LineTo (CARD x1,y1,x2,y2)

BYTE c=$2FB

c=color

IF x1>319 THEN
  x1=319
FI
IF x2>319 THEN
  x2=319
FI
IF y1>191 THEN
  y1=191
FI
IF y2>191 THEN
  y2=191
FI

IF x1=x2 THEN 
 VLine (x1,y1,y2)
 RETURN
FI

IF y1=y2 THEN
 HLine (y1,x1,x2)
 RETURN
FI

Line (x1,y1,x2,y2)

RETURN

BYTE FUNC Inter (BYTE b)
 IF b>=0 AND b<32 THEN
  b==+64
 ELSEIF b>31 AND b<96 THEN
  b==-32
 ELSEIF b>127 AND b<160 THEN
  b==+64
 ELSEIF b>159 AND b<224 THEN
  b==-32
 FI
RETURN (b)

PROC Text (CARD x,BYTE y,BYTE ARRAY tex)

BYTE len,u,ci=$2FA

len=tex(0)

FOR u=1 TO len
DO
 ci=Inter(tex(u))
 Shape (x,y)
 x==+8
OD

RETURN

INT FUNC Abs(INT n)

	IF n<0 THEN RETURN( -n ) FI
RETURN( n )

PROC Circle(INT x,y,r)

  BYTE c=$2FB
  INT Phi,Phiy,Phixy,
		x1,y1

  Phi=0
  x1=r
  y1=0
  c=color

  DO
	 Phiy=Phi+y1+y1+1
	 Phixy=Phiy-x1-x1+1
	 Pixel(x+x1,y+y1) 
	 Pixel(x-x1,y+y1) 
	 Pixel(x+x1,y-y1) 
	 Pixel(x-x1,y-y1) 
	 Pixel(x+y1,y+x1) 
	 Pixel(x-y1,y+x1) 
	 Pixel(x+y1,y-x1) 
	 Pixel(x-y1,y-x1) 
	 Phi=Phiy
	 y1=y1+1
	 IF Abs(Phixy)+0<Abs(Phiy) THEN
		Phi=Phixy
		x1=x1-1
	 FI
  UNTIL y1>x1
  OD
RETURN

PROC Disk (CARD x,y,r)

  BYTE c=$2FB
  INT Phi,Phiy,Phixy,
		x1,y1

  Phi=0
  x1=r
  y1=0
  c=color

  DO
	 Phiy=Phi+y1+y1+1
	 Phixy=Phiy-x1-x1+1
	 VLine (y+y1,x+x1,x-x1)
	 VLine (y-y1,x+x1,x-x1)
	 VLine (y+x1,x+y1,x-y1)
	 VLine (y-x1,x+y1,x-y1)
	 Phi=Phiy
	 y1=y1+1
	 IF Abs(Phixy)+0<Abs(Phiy) THEN
		Phi=Phixy
		x1=x1-1
	 FI
  UNTIL y1>x1
  OD
RETURN

PROC Box (CARD x1,y1,x2,y2)

BYTE c=$2FB
CARD x,y

c=color

IF x1>x2 THEN
 x=x1
 x1=x2
 x2=x
FI

IF y1>y2 THEN
 y=y1
 y1=y2
 y2=y
FI

FOR x=x1 TO x2
DO
 VLine (x,y1,y2)
OD

RETURN
 
PROC Frame (CARD x1,y1,x2,y2)

BYTE c=$2FB

c=color

HLine (y1,x1,x2)
HLine (y2,x1,x2)
VLine (x1,y1,y2)
VLine (x2,y1,y2)

RETURN
```
  
### 1st Version  
  
```
;********************************
;** FAST GRAPH                 **
;** PHOENIX SOFTCREW 1990      **
;** SCHNELLE GRAPHIKROUTINEN   **
;** FUER GRAPHICS 8	       **
;********************************

BYTE FUNC Sgn (INT wert)

  Byte u

  IF wert<0 THEN
	 u=-1
  ELSE
	 u=1
  FI

RETURN (u)

CARD FUNC Abs (CARD wert)

  IF wert<0 THEN
	 wert=-wert
  FI

RETURN (wert)


PROC Point (CARD x,BYTE y,mode)

  BYTE yp=$54
  CARD savmsc=$58,xp=$55
  BYTE ARRAY pixt=[ $80 $40 $20 $10 $08 $04 $02 $01 ]
  BYTE POINTER z

  xp=x
  yp=y

  mode==MOD 2

  IF x<320 AND x>=0 AND y>=0 AND y<192 THEN
  
	 z=savmsc
	 z==+y*40
	 z==+(x RSH 3)
	 IF mode=1 THEN
		z^==%pixt(x&7)
	 ELSE
		z^==!pixt(x&7)
	 FI
  FI 

RETURN

PROC Line (CARD x,BYTE y)

  BYTE yp=$54,d1x,d2x,d1y,d2y
  CARD xp=$55,xa,ya,u,v,n,m,zp,s,z

  xa=xp
  ya=yp

  u=x-xa
  v=y-ya

  d1x=Sgn (u)
  d2x=Sgn (u)
  d1y=Sgn (v)
  d2y=0

  m=Abs (u)
  n=Abs (v)

  IF n>m THEN
	 d2x=0
	 d2y=d1y
	 zp=m
	 m=n
	 n=zp
  FI

  s=m/2
  z=0

  DO
	 Point (xa,ya,1)
	 s==+n
	 IF m<s THEN
		s==-m
		xa==+d1x
		ya==+d1y
	 ELSE
		xa==+d2x
		ya==+d2y
	 FI

	 z==+1
  UNTIL z=m
  OD

RETURN


PROC Circle(INT x,y,r,c)

  INT Phi,Phiy,Phixy,
		x1,y1

  Phi=0
  x1=r
  y1=0
  color=c
  DO
	 Phiy=Phi+y1+y1+1
	 Phixy=Phiy-x1-x1+1
	 Point(x+x1,y+y1,1) ; 
	 Point(x-x1,y+y1,1) ;|
	 Point(x+x1,y-y1,1) ;|
	 Point(x-x1,y-y1,1) ;  8 way symmetry
	 Point(x+y1,y+x1,1) ;  plotting points
	 Point(x-y1,y+x1,1) ;|
	 Point(x+y1,y-x1,1) ;|
	 Point(x-y1,y-x1,1) ; 
	 Phi=Phiy
	 y1=y1+1
	 IF Abs(Phixy)+0<Abs(Phiy) THEN
		Phi=Phixy
		x1=x1-1
	 FI
  UNTIL y1>x1
  OD
RETURN

```
  
### 2nd version  
  
```
;********************************
;** FAST GRAPH	               **
;** PHOENIX SOFTCREW 1990      **
;** FOR GRAPHICS 8             **
;********************************

BYTE FUNC Sgn (INT wert)

  Byte u

  IF wert<0 THEN
	 u=-1
  ELSE
	 u=1
  FI

RETURN (u)

CARD FUNC Abs (INT wert)

  IF wert<0 THEN
	 wert=-wert
  FI

RETURN (wert)


PROC Point (CARD x,BYTE y)

  BYTE yp=$54,oldy=$5A,mode
  CARD savmsc=$58,xp=$55,oldx=$5B
  BYTE ARRAY pixt=[$80 $40 $20 $10 $8 $4 $2 $1]
  BYTE POINTER z

  xp=x
  yp=y

  oldx=x
  oldy=y

  mode=color
  mode==MOD 2

  IF x<320 AND x>=0 AND y>=0 AND y<192 THEN
  
	 z=savmsc
	 z==+y*40
	 z==+(x RSH 3)
	 IF mode=1 THEN
		z^==%pixt(x&7)
	 ELSE
		z^==!pixt(x&7)
	 FI
  FI 

RETURN

PROC Line (CARD x,BYTE y)

  BYTE yp=$54
  CARD xp=$55,z
  INT xs,ys

	DrawTo (x,y)

RETURN

PROC Circle(INT x,y,r)

  INT Phi,Phiy,Phixy,
		x1,y1

  Phi=0
  x1=r
  y1=0
  DO
	 Phiy=Phi+y1+y1+1
	 Phixy=Phiy-x1-x1+1
	 Point(x+x1,y+y1) ; 
	 Point(x-x1,y+y1) ;|
	 Point(x+x1,y-y1) ;|
	 Point(x-x1,y-y1) ;  8 way symmetry
	 Point(x+y1,y+x1) ;  plotting points
	 Point(x-y1,y+x1) ;|
	 Point(x+y1,y-x1) ;|
	 Point(x-y1,y-x1) ; 
	 Phi=Phiy
	 y1=y1+1
	 IF Abs(Phixy)+0<Abs(Phiy) THEN
		Phi=Phixy
		x1=x1-1
	 FI
  UNTIL y1>x1
  OD
RETURN

PROC Disk (CARD x,y,r)

  BYTE u

  FOR u=0 TO r
  DO
	Circle (x,y,u)
  OD

RETURN

PROC Frame (CARD x1,y1,x2,y2)

  Point (x1,y1)
  Line (x2,y1)
  Line (x2,y2)
  Line (x1,y2)
  Line (x1,y1)

RETURN

PROC Box (CARD x1,y1,x2,y2)

  BYTE xs
  CARD xw

  IF x1<x2 THEN
	xs=1
  ELSE
	xs=-1
  FI

  FOR xw=x1 TO x2 STEP xs
  DO
	Plot (xw,y1)
	Line (xw,y2)
  OD

RETURN

```
  
### Assembler Source (BIBO Assembler)  
  
```
00010			 .LI OFF
00020 ******************************
00030 *									 *
00040 * PROGRAMM:SCHNELLER GR8.PLOT*
00050 * AUTOR	:CARSTEN STROTMANN *
00060 * DATUM	:12.12.90			 *
00070 * VERSION :.2					 *
00080 * FUER	 :ACTION!			  *
00090 *									 *
00100 ******************************
00110 ;
00120			 .OR $7000
00130			 .OF "D:GR8.COM"
00140 ;
00150 ROWCRS	=	$54
00160 COLCRS	=	$55
00170 ROWAC	 =	$70
00180 COLAC	 =	$72
00190 ATACHR	=	$2FB
00200 SAVMSC	=	$58
00210 OLDROW	=	$5A
00220 OLDCOL	=	$5B
00230 ZAEHLER  =	$E4
00240 DELTAX	=	$77
00250 DELTAY	=	$76
00260 XFLAG	 =	$74
00270 YFLAG	 =	$75
00280 HILFA	 =	$E9
00290 HILFB	 =	$EB
00300 HILFT	 =	$ED
00310 HLP1	  =	$E6
00320 HLP2	  =	$E7
00330 HLP3	  =	$E8
00340 TXTROW	=	$290
00350 TXTCOL	=	$291
00360 CADR	  =	$70
00370 CHBAS	 =	$2F4
00380 CHAR	  =	$2FA
00390 ;
00400 ;
00410 CALC
00420			 STA COLCRS
00430			 STX COLCRS+1
00440			 STY ROWCRS
00450 ;
00460			 LDA #0
00470			 STA HLP1
00480			 STA HLP2
00490			 STA HLP3
00500 ;
00510			 TYA
00520			 ASL
00530			 ROL HLP1
00540			 ASL
00550			 ROL HLP1
00560			 ASL
00570			 ROL HLP1  ;Y*8
00580			 STA HLP2
00590			 LDX HLP1
00600			 STX HLP3
00610			 ASL
00620			 ROL HLP1
00630			 ASL
00640			 ROL HLP1  ;Y*32
00650 ;
00660			 CLC
00670			 ADC HLP2
00680			 STA HLP2
00690			 LDA HLP3
00700			 ADC HLP1
00710			 STA HLP3  ;*8+*32=*40
00720 ;
00730			 CLC
00740			 LDA SAVMSC
00750			 ADC HLP2
00760			 STA ROWAC
00770			 LDA SAVMSC+1
00780			 ADC HLP3
00790			 STA ROWAC+1
00800 ;
00810			 LDA COLCRS
00820			 AND #7
00830			 TAX
00840			 LDA COLCRS
00850			 LSR
00860			 LSR
00870			 LSR
00880			 TAY
00890			 LDA COLCRS+1
00900			 BEQ .1
00910			 TYA
00920			 CLC
00930			 ADC #32
00940			 TAY
00950 ;
00960 .1
00970			 LDA ATACHR
00980			 BEQ CLEAR
00990			 CMP #1
01000			 BEQ PLOT
01010			 CMP #2
01020			 BEQ XPLOT
01030 ;
01040 LOCATE
01050			 LDA (ROWAC),Y
01060			 AND PTAB,X
01070			 STA ATACHR
01080			 RTS
01090 ;
01100 PLOT
01110			 LDA (ROWAC),Y
01120			 ORA PTAB,X
01130			 STA (ROWAC),Y
01140			 RTS
01150 ;
01160 XPLOT
01170			 LDA (ROWAC),Y
01180			 EOR PTAB,X
01190			 STA (ROWAC),Y
01200			 RTS
01210 ;
01220 CLEAR
01230			 LDA (ROWAC),Y
01240			 AND CTAB,X
01250			 STA (ROWAC),Y
01260			 RTS
01270 ------------------------------
01280 * BITTABELLE
01290 PTAB	  .HX 8040201008040201
01300 CTAB	  .HX 7FBFDFEFF7FBFDFE
01310 ------------------------------
01320 SHAPE
01330 ;  ZEICHENSATZ AUF GRAFIK
01340 ;  BILDSCHIRM
01350 ;  A = X-POSITION LSB
01360 ;  X = X-POSITION MSB
01370 ;  Y = Y-POSITION
01380 ;  CHAR=ZEICHEN IM INT-CODE
01390 ;
01400			 STA TXTCOL
01410			 STX TXTCOL+1
01420			 STY TXTROW
01430 ;
01440			 LDA #0
01450			 STA HLP1
01460			 STA HLP2
01470			 STA HLP3
01480 ;
01490			 LDA CHBAS
01500			 STA CADR+1
01510			 LDA #0
01520			 STA CADR
01530 ;
01540			 LDA CHAR
01550			 ASL
01560			 ROL HLP1
01570			 ASL
01580			 ROL HLP1
01590			 ASL
01600			 ROL HLP1
01610			 CLC
01620			 ADC CADR
01630			 STA CADR
01640			 LDA HLP1
01650			 ADC CADR+1
01660			 STA CADR+1
01670			 LDA #0
01680			 STA HLP1
01690 ;
01700 ; ZEICHEN UEBERTRAGEN
01710 ;
01720			 LDX #16
01730			 LDY #8
01740 .1
01750			 LDA (CADR),Y
01760			 STA CTABL,X
01770			 DEX
01780			 DEX
01790			 DEY
01800			 BNE .1
01810 ;
01820 ; ZEICHEN SCHIFTEN
01830 ;
01840			 LDA TXTCOL
01850			 AND #7
01860			 TAY
01870 .3
01880			 LDX #16
01890 ;
01900 .2
01910			 LSR CTABL,X
01920			 ROR CTABL+1,X
01930			 DEX
01940			 DEX
01950			 BNE .2
01960 ;
01970			 DEY
01980			 BNE .3
01990 ;
02000 ; ADRESSE ERRECHNEN
02010 ;
02020			 LDA TXTROW
02030			 ASL
02040			 ROL HLP1
02050			 ASL
02060			 ROL HLP1
02070			 ASL
02080			 ROL HLP1
02090			 LDA HLP1
02100			 STA HLP2
02110			 LDX HLP1
02120			 STX HLP3
02130			 ASL
02140			 ROL HLP1
02150			 ASL
02160			 ROL HLP1
02170			 CLC
02180			 ADC HLP2
02190			 STA HLP2
02200			 LDA HLP3
02210			 ADC HLP1
02220			 STA HLP3
02230 ;
02240			 CLC
02250			 LDA SAVMSC
02260			 ADC HLP1
02270			 STA ROWAC
02280			 LDA SAVMSC+1
02290			 ADC HLP3
02300			 STA ROWAC+1
02310 ;
02320			 LDA TXTCOL
02330			 LSR
02340			 LSR
02350			 LSR
02360			 TAY
02370			 LDA TXTCOL+1
02380			 BEQ .4
02390			 TYA
02400			 CLC
02410			 ADC #32
02420			 TAY
02430 ;
02440 ; ZEICHEN AUF BILDSCHIRM
02450 ;
02460 .4
02470			 LDX #8
02480 .6
02490			 LDA (ROWAC),Y
02500			 EOR CTAB,X
02510			 STA (ROWAC),Y
02520			 INY
02530			 LDA (ROWAC),Y
02540			 EOR CTAB+1,X
02550			 STA (ROWAC),Y
02560			 DEY
02570			 CLC
02580			 LDA ROWAC
02590			 ADC #40
02600			 STA ROWAC
02610			 BCC .5
02620			 INC ROWAC+1
02630 .5		 DEX
02640			 BNE .6
02650 ;
02660			 RTS
02670 ------------------------------
02680 ; BUFFERTABLLE FUER ZEICHEN
02690 CTABL
02700			 .HX 0000
02710			 .HX 0000
02720			 .HX 0000
02730			 .HX 0000
02740			 .HX 0000
02750			 .HX 0000
02760			 .HX 0000
02770			 .HX 0000
02780 ------------------------------

```
  
