# XFD Transfer  
  
re-released 17.3.2003 under the terms of the GNU Public License (GPL), see http://www.gnu.org  
  
  
%%tabbedSection  
%%deutsch  
## Deutsche Anleitung  
  
  
XFormer Transfer 1.0  
(c) 1994-2003 by PhoeniX SoftCrew  
fuer ABBUC e.V.  
  
  
XFormer Transfer ist ein Hilfsprogramm  
fuer alle Atari Fans, die mit dem  
XFormer Emulator ATARI Programme auf  
einen PC bringen moechten.  
  
  
Das Programm liest eine ATARI Single  
Density Diskette und schreibt sie in  
eine XFD Datei. Diese Datei kann nun  
per Diskette oder Datenuebertragung auf  
einen PC uebertragen werden.  
  
  
Bedienung:  
  
  
Mit der Taste 'Q' kann das Quell-  
laufwerk angegeben werden, mit der  
Taste 'Z' kann man eine neue Zieldatei  
angeben. Ein Druck auf die Taste 'S'  
startet den Kopiervorgang. Das Programm  
wird mit der ESC-Taste verlassen.  
  
  
Am einfachsten ist es die erstellte  
Datei mit der ABBUC-PC Diskette auf  
den PC zu ueberspielen. Der XFormer 2  
Emulator kann die erstellten Dateien  
als virtuelle Disketten benutzen.  
  
  
  
September 1994,  
Carsten Strotmann  
/%  
%%english  
## Englisch Description  
  
  
XFormer Transfer 1.0  
(c) 1994-2003 by PhoeniX SoftCrew  
for ABBUC e.V.  
  
  
XFormer Transfer is an Utility Program for  
all ATARI Fans who wants to run ATARI  
programs with the help on an emulator to  
a PC.  
  
  
The Programm reads an ATARI Single  
Density Disk and writes its content  
into a XFD-File. This File can than  
be transfered to a PC by a Disk or  
RS232 cable.  
  
  
Usage:  
  
  
Choose the Sourcedrive with the Key "S",  
enter a Destination File with the Menu-Key "D".  
The Key "C" starts the Copy process. ESC exits the Programm  
(to DOS).  
  
It is easy to transfer the created XFD File to  
the PC with the help of the ABBUC-PC Disk.  
The PC XFormer 2 Emulator can use this files as  
virtual Disks.  
  
  
September 1994,  
Carsten Strotmann  
  
/%  
/%  
  
  
  
  
## XFDTRANS .ACT  
  
```
;********************************
;**                            **
;** Phoenix SoftCrew ACTION!   **
;** Programs and Tips for 8Bit **
;**                            **
;** Carsten Strotmann          **
;** atari@strotmann.de         **
;**                            **
;********************************

; Programname:XFD Transfer
; Programmer:CS
; Filename:XFDTRANS.ACT
; first Version:09.09.94
; last change:09.09.94/17.03.2003
; Use: Copies SD Disk to XFD
;       Diskfile for
;       PC XFormer 2
; Bemerkung:
;
;
INCLUDE "SYSTEM.ACT"

MODULE

BYTE drivenum,err,p_read
CARD maxsec,bytes
BYTE ARRAY percom($C),
           buff($1000),
           txt(40),
           destfile(40)

INCLUDE "XFDTRANS.INC"
           
PROC Read_Percom ()
 
 err=Sio (drivenum,$52,$40,7,buff,128,1)
 err=Sio (drivenum,$4E,$40,7,percom,12,0)
  
 maxsec=percom(0)*(percom(2)*$100+percom(3))
 maxsec==*(percom(4)+1)
 bytes =percom(6)*$100+percom(7)
 p_read=err

RETURN

PROC Write_Percom ()
 
 err=Sio (drivenum,$4F,$80,7,percom,12,0)
 
RETURN

PROC CopyDisk()

 BYTE ch=$2FC,consol=$D01F
 CARD u,b,s,t,a

 Close(2)
 Open (2,destfile,8,0)

 Read_Percom()
 Write (0,15,"0.........1.........2.........3........9")
 Write (5,19,"...an ACTION! Program.        ")
 Write (5,20,"for ABBUC e.V., GPLed 2003        ")
 
 u=0
 t=0
 b=bytes

 DO
  a=buff
  Write (t,16,"L")
  FOR s = 1 TO 18 DO
    u ==+1
    err=Sio (drivenum,$52,$40,$7,a,b,u)
    a==+$80
  OD
  Write (t,16,"S")
  Bput (2,buff,$900)
  Write (t,16,".")
  t==+1
 UNTIL u=maxsec OR ch=28 or consol=6
 OD

 Pause (200)
 Write (0,15,"                                        ")
 Write (0,16,"                                        ")
 Write (0,19,"                                        ")
 Write (0,20,"                                        ")
 ch=$FF

 Close(2)

RETURN
 
PROC Mask ()

 BYTE lmarg=82
 CARD savmsc=$58

 lmarg=0

 SetBlock (savmsc+120,240,0)
 
 Write (0,0," PhoeniX SoftCrew XFormer Transfer  1.0 ")

 Write (5,4,"Source Drive:     (1-9)")
 StrB (drivenum,txt)
 Write (21,4,txt)

 Write (5,6,"Dest. File    :")
 Write (21,6,destfile)

 Write (5,10,"Start Copy Process ....")
 Write (5,20,"~[ESC] to end program        ")

 Write (0,23,"      (c) 1994 PhoeniX SoftCrew         ")

RETURN                   


PROC GetDriveNum()

 C_On()
 DO
  Position (21,4)
  GetIn (txt,1)
  drivenum =  ValB(txt)
 UNTIL drivenum > 0 AND drivenum < 9
 OD
 C_Off()

RETURN

PROC GetDestFile()
       
 SCopy(destfile,"D8:")
 Write (21,6,"               ")

 C_On()
 DO
  Position (21,6)
  GetIn (destfile,15)
 UNTIL destfile(0) > 1
 OD
 C_Off()

 Upper(destfile)

RETURN

PROC XFDTrans ()

 BYTE key 
 BYTE ARRAY value (3)

 drivenum = 1
 SCopy (destfile,"D8:DISK1.XFD")

 p_read=$FF

 Put (125)
 C_Off ()
 Mask ()
 
 DO
  key=Inkey ()

  IF key = 'S OR key = 's THEN
   GetDriveNum()
   Mask()
  FI

  IF key = 'D OR key = 'd THEN
   GetDestFile()
   Mask()
  FI

  IF key = 'C OR key = 'c THEN
   CopyDisk()
   Mask()
  FI

 UNTIL key=27
 OD

 C_On ()

RETURN
                          

```
  
## XFDTRANS .INC  
  
```
; Includedatei fuer XFDTRANS.ACT
;---

MODULE
BYTE CIO_status

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

  BYTE ascii,pos,u,inv

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

BYTE FUNC Find (BYTE ARRAY str2,str1)

  BYTE len1,len2,z1,z2,flg,pos

  IF str1(0)>=str2(0) THEN
   len2=str2(0)
   len1=str1(0)
   len1==-len2+1
   z1=0
   z2=0
   DO
    flg=$FF
    z1==+1
    FOR z2=1 to len2
    DO
     IF str1(z1+z2-1)#str2(z2) THEN
      flg=0
     FI
    OD
   UNTIL z1=len1 OR flg#0
   OD
   IF flg#0 THEN
    pos=z1
   ELSE
    pos=0
   FI
  ELSE
   pos=0
  FI

RETURN (pos)

PROC Upper (BYTE ARRAY text)

  BYTE u

  FOR u=1 TO text(0)
  DO
   IF text(u)>$60 AND text(u)<$7B THEN
    text(u)==-$20
   FI
  OD

RETURN

CHAR FUNC CIOQ=*(BYTE dev, CARD addr,
          size, BYTE cmd, aux1, aux2)
~[$29$F$85$A0$86$A1$A$A$A$A$AA$A5$A5
$9D$342$A5$A3$9D$348$A5$A4$9D$349
$A5$A6$F0$8$9D$34A$A5$A7$9D$34B$98
$9D$345$A5$A1$9D$344$20$E456
$8C CIO_status$C0$88$D0$6$98$A4$A0
$99 EOF$A085$60]

PROC BPut=*(BYTE dev,
                    CARD addr, size)
~[$48$A9$B$85$A5$A9$0$85$A6$A5$A3$5$A4
$D0$2$68$60$68$4C CIOQ]

```
  
