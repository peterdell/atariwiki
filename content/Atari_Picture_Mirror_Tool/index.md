  
# Atari Picture Mirror Tool  
  
```
;********************************
;**                            **
;** Phoenix SoftCrew ACTION!   **
;**                            **
;********************************

; Programname:PIC-MIRROR
; Programmer:Carsten Strotmann
; Filename:MIIRROR.ACT
; first Version:28.04.90
; last change:28.04.90
; Task:Mirrors GR.8 Pictures (7680 Byte Pics)
;
;

;INCLUDE "SYSTEM.ACT"

BYTE CIO_status


CHAR FUNC CIOQ=*(BYTE dev, CARD addr,
          size, BYTE cmd, aux1, aux2)
[$29$F$85$A0$86$A1$A$A$A$A$AA$A5$A5
$9D$342$A5$A3$9D$348$A5$A4$9D$349
$A5$A6$F0$8$9D$34A$A5$A7$9D$34B$98
$9D$345$A5$A1$9D$344$20$E456
$8C CIO_status$C0$88$D0$6$98$A4$A0
$99 EOF$A085$60]


CARD FUNC Bget=*(BYTE dev,
                    CARD addr, size)
[$48$A9$7$85$A5$A9$0$85$A6$A5$A3$5$A4
$D0$6$85$A0$85$A1$68$60$68$20 CIOQ
$BD$348$85$A0$BD$349$85$A1$60]


PROC BPut=*(BYTE dev,
                    CARD addr, size)
[$48$A9$B$85$A5$A9$0$85$A6$A5$A3$5$A4
$D0$2$68$60$68$4C CIOQ]

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

PROC Mirror ()

 BYTE sd,dd,key,x,y,c1,c2
 CARD z,savmsc=$58

 BYTE ARRAY col(0)=708,sf(17),df(17),fn(17),buf(250)
 
 Graphics (0)

 col(1)=15
 col(2)=115

 Position (0,0)

 Print (" PhoeniX SoftCrew Pic Mirror (c) 1990")

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

  Graphics (24)
  col(1)=0
  col(2)=14

  Close (1)
  Open (1,sf,4)
  Bget (1,savmsc,7680)
  Close (1)

  FOR x=0 TO 159
  DO
   FOR y=0 TO 191
   DO
    c1=Locate (x,y)
    c2=Locate (319-x,y)
    color=c1
    Plot (319-x,y)
    color=c2
    Plot (x,y)
   OD
  OD
 
  Close (1)
  Open (1,df,8,0)
  Bput (1,savmsc,7680)
  Close (1)

  Graphics (0)

  Position (0,20)
  Print (" Another File ?")

  key=Inkey ()

 UNTIL key ='N or key='n
 OD

RETURN

```
  
