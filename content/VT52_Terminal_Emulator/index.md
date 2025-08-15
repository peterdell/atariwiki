---
title: VT52 Terminal Emulator
---
# VT52 Emulator  
  
The following is a very primitive vt52 emulator for the 800.  This actually  
is a vt52 with insert/delete line added, with auto-wrap, and tabs.  
It is written in Action! with lower case enabled.  
  
To use this, you will need an rs232 device (I have only tested this at  
300 buad using an 850 interface and 830 modem, but it seems to work well).  
The rs232 parameters are hard coded, so you will probably have to change  
the values of baud, parity, etc.  Consult your 850 or R-verter manual.  
The values that may require change are the following..  
  
```
   speed = ~[1],
   wsize = ~[0],
   sbits = ~[0],
   lf = ~[0],
   iparity = ~[0],
   oparity = ~[0]     
```
  
This works by defining an output device A: which works in graphics mode 8,  
which writes characters in 4 bits.  I have used this emulator with vi, rogue,  
jove, etc., under UNIX using the vt52 termcap entry, and also (with some  
slight modification to allow generation of ENTER, pf, and cursor keys) under  
CMS.  If anyone wants this version, I can mail the diff's.  
  
The following characters are defined in addition to those found on the  
keyboard.  
  
```
ctrl clear - {
ctrl insert - }
ctrl delete - ~
```
  
---
```
;*********************************
;*                               *
;* VT52A.ACT - a VT52+ emulator  *
;* written in ACTION(tm) by      *
;*                               *
;*     Michael R. M. Jenkin      *
;*     University of Toronto     *
;*     ...!utcsri!utai!jenkin    *
;*     copyright(c) 1985         *
;*                               *
;* released into the public      *
;* domain May, 1986. No part of  *
;* this program may be           *
;* redistributed for profit      *
;* without permission of the     *
;* author.                       *
;*                               *
;*********************************

MODULE
;A: handler, by Michael Jenkin

DEFINE LDY  = "$A0",
       RTS  = "$60",
       JMP  = "$4C"

BYTE lmargin = $52, rmargin = $53,
     rowcrs  = $54, oldrow  = $5A,
     colcrs  = $55,
     oldchr  = $5D, inesc, need,
     needx, inv
CARD savmsc  = $58,
     oldcol  = $5B

PROC Achr(BYTE cx, cy, cc)
   BYTE POINTER base, offset
   BYTE i, char, c
   BYTE ARRAY chset = ~[
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 0 0 0 0 0 0 0
      0 6 6 6 6 0 6 0
      0 10 10 10 0 0 0 0
      10 14 10 14 10 0 0 0
      4 14 8 14 2 14 4 0
      0 10 2 6 12 8 10 0
      0 14 2 6 6 2 14 0
      0 6 6 6 0 0 0 0
      0 6 12 8 8 12 6 0
      0 12 6 2 2 6 12 0
      0 10 4 14 4 10 0 0
      0 4 4 14 4 4 0 0
      0 0 0 0 0 6 6 12
      0 0 0 14 0 0 0 0
      0 0 0 0 0 6 6 0
      0 2 2 4 4 8 8 0
      0 14 10 10 10 10 14 0
      0 4 12 4 4 4 14 0
      0 14 2 2 14 8 14 0
      0 14 2 14 2 2 14 0
      0 10 10 10 14 2 2 0
      0 14 8 14 2 2 14 0
      0 14 8 14 10 10 14 0
      0 14 2 6 4 4 4 0
      0 14 10 14 10 10 14 0
      0 14 10 14 2 2 2 0
      0 0 6 6 0 6 6 0
      0 0 6 6 0 6 6 12
      0 2 6 12 12 6 2 0
      0 0 14 0 0 14 0 0
      0 8 12 6 6 12 8 0
      0 4 10 2 4 0 4 0
      14 10 10 14 8 8 14 0
      0 4 14 10 10 14 10 0
      0 12 10 12 10 10 12 0
      0 14 10 8 8 10 14 0
      0 12 10 10 10 10 12 0
      0 14 8 12 8 8 14 0
      0 14 8 12 8 8 8 0
      0 14 8 8 10 10 14 0
      0 10 10 14 10 10 10 0
      0 14 4 4 4 4 14 0
      0 2 2 2 2 10 14 0
      0 10 10 12 12 10 10 0
      0 8 8 8 8 8 14 0
      0 10 14 14 10 10 10 0
      0 12 10 10 10 10 10 0
      0 14 10 10 10 10 14 0
      0 14 10 14 8 8 8 0
      0 14 10 10 10 10 14 2
      0 14 10 14 12 10 10 0
      0 14 8 14 2 2 14 0
      128 14 4 4 4 4 4 0
      0 10 10 10 10 10 14 0
      0 10 10 10 10 10 4 0
      0 10 10 10 14 14 10 0
      0 10 10 4 4 10 10 0
      0 10 10 4 4 4 4 0
      0 14 2 4 4 8 14 0
      0 14 8 8 8 8 14 0
      0 8 8 4 4 2 2 0
      0 14 2 2 2 2 14 0
      0 4 4 10 0 0 0 0
      0 0 0 0 0 0 15 0
      0 4 6 2 0 0 0 0
      0 0 14 2 14 10 14 0
      0 8 8 14 10 10 14 0
      0 0 0 14 8 8 14 0
      0 2 2 14 10 10 14 0
      0 0 14 10 14 8 14 0
      0 0 14 8 12 8 8 0
      0 0 14 10 10 14 2 14
      0 8 8 14 10 10 10 0
      0 6 0 6 6 6 6 0
      0 6 0 6 6 6 6 12
      0 8 8 10 14 10 10 0
      0 12 4 4 4 4 14 0
      0 0 10 14 14 10 10 0
      0 0 12 10 10 10 10 0
      0 0 14 10 10 10 14 0
      0 0 14 10 10 14 8 8
      0 0 14 10 10 14 2 2
      0 0 14 10 8 8 8 0
      0 0 14 8 14 2 14 0
      0 4 14 4 4 4 4 0
      0 0 10 10 10 10 14 0
      0 0 10 10 10 10 4 0
      0 0 10 10 14 14 10 0
      0 0 10 14 4 14 10 0
      0 0 10 10 10 14 2 14
      0 0 14 2 4 8 14 0
      2 4 4 8 4 4 2 0
      6 6 6 0 0 6 6 6
      8 4 4 2 4 4 8 0
      0 10 5 0 0 0 0 0
      0 0 0 0 0 0 0 0
   ]
   ;strip high bit (inverse video)
   cc ==& $7F
   ;display character            
   base = (cx RSH 1) + cy * 320 + savmsc
   offset = cc
   offset = offset LSH 3
   offset ==+ chset
   FOR i = 0 TO 7
   DO
      c = offset^  
      IF inv = 1 THEN
         c = c XOR $FF ; c = NOT c
      FI                           
      char = base^                 
      IF (cx & 1) THEN
         c ==& $0F
         char ==& $F0
      ELSE        
         c = c LSH 4
         char ==& $0F           
      FI                             
      base^ = char % c
      base ==+ 40
      offset ==+1
  OD
RETURN

PROC Acurse(BYTE cx, cy); invert char
   BYTE POINTER base
   BYTE i, char
   base = (cx RSH 1) + 320 * cy + savmsc
   FOR i = 0 TO 7
   DO
      char = base^
      IF (cx & 1) THEN
         char = char XOR $0F
      ELSE
         char = char XOR $F0
      FI
      base^ = char
      base ==+ 40
   OD
RETURN

PROC Ascroll() ; update cursor
   IF colcrs > rmargin THEN
      colcrs = lmargin
      rowcrs ==+ 1
   FI
   IF rowcrs > 23 THEN
      MoveBlock(savmsc,savmsc+320,320*23)
      Zero(savmsc+23*320,320)
      rowcrs = 23
   FI
   Acurse(colcrs,rowcrs)
RETURN

PROC Aesc(BYTE char) ; escape sequence
   BYTE ch
   BYTE POINTER addr
   CARD i
   IF need = 2 THEN ; 1st ESC Y
      needx = char - $20
      need ==- 1
   ELSEIF need = 1 THEN ; 2nd ESC Y
      char ==- $20
      IF (needx <= 23) AND (char <= rmargin) THEN
         Acurse(colcrs,rowcrs)
         colcrs = char
         rowcrs = needx
         Acurse(colcrs,rowcrs)
      FI
      need = 0
   ELSEIF char = 'A THEN ; cursor up
      IF rowcrs > 0 THEN
         Acurse(colcrs,rowcrs)
         rowcrs ==- 1
         Acurse(colcrs,rowcrs)
      FI
   ELSEIF char = 'B THEN ; cursor down
      IF rowcrs < 23 THEN 
         Acurse(colcrs,rowcrs)
         rowcrs ==+ 1
         Acurse(colcrs,rowcrs)
      FI
   ELSEIF char = 'C THEN ; cursor right
      IF colcrs < rmargin THEN
         Acurse(colcrs,rowcrs)
         colcrs ==+ 1
         Acurse(colcrs,rowcrs)
      FI
   ELSEIF char = 'D THEN ; cursor left
      IF colcrs > 0 THEN
         Acurse(colcrs,rowcrs)
         colcrs ==- 1
         Acurse(colcrs,rowcrs)
      FI
   ELSEIF char = 'F THEN ; inverse on
      inv = 1
   ELSEIF char = 'G THEN ; inverse off
      inv = 0
   ELSEIF char = 'H THEN ; home
      Acurse(colcrs,rowcrs)
      colcrs = 0
      rowcrs = 0
      Acurse(colcrs,rowcrs)
   ELSEIF char = 'I THEN ; reverse lf
      Acurse(colcrs,rowcrs)
      IF rowcrs > 0 THEN   
         rowcrs ==- 1
         Acurse(colcrs,rowcrs)
      ELSE
         FOR i = 0 TO 22 DO
            addr = savmsc+320*(23-i)
            MoveBlock(addr,addr-320,320)
         OD
         Zero(savmsc,320)
         Acurse(colcrs,rowcrs)
      FI
   ELSEIF char = 'J THEN ; erase to EOS
      FOR ch = colcrs TO 79
      DO
         Achr(ch,rowcrs,' )
      OD                             
      IF rowcrs < 23 THEN
         Zero(savmsc+320*(rowcrs+1),320*(23-rowcrs))
      FI
      Acurse(colcrs,rowcrs)
   ELSEIF char = 'K THEN ; erase to EOL
      FOR ch = colcrs TO 79
      DO
         Achr(ch,rowcrs,' )
      OD                   
      Acurse(colcrs,rowcrs)
   ELSEIF char = 'L THEN ; insert line
      Acurse(colcrs,rowcrs)
      FOR i = rowcrs TO 22 DO
         addr = savmsc+320*(23-i+rowcrs)
         MoveBlock(addr,addr-320,320)
      OD
      Zero(savmsc+320*rowcrs,320)
      colcrs = 0
      Acurse(colcrs,rowcrs)
   ELSEIF char = 'M THEN ; delete line
      IF rowcrs < 23 THEN
         MoveBlock(savmsc+320*rowcrs,savmsc+320*(rowcrs+1),320*(23-rowcrs))
      FI
      Zero(savmsc+320*22,320)
      colcrs = 0
      Acurse(colcrs,rowcrs)
   ELSEIF char = 'Y THEN ; cursor addr
      need = 2
   FI      
   IF need = 0 THEN
      inesc = 0
   FI
RETURN

PROC Aopen()
   SetColor(0,0,0)
   SetColor(1,12,15)
   inesc = 0
   inv = 0
   need = 0
   lmargin = 0
   rmargin = 79   
   rowcrs = 0
   colcrs = 0
   Acurse(colcrs,rowcrs)
   ~[LDY 1 RTS]

PROC Aclose()
   ~[LDY 1 RTS]

PROC Aput(BYTE areg)
   BYTE i, n
   IF inesc = 1 THEN; escape sequence
      Aesc(areg)
   ELSEIF areg = $1B THEN ; ESC
      inesc = 1
   ELSEIF areg = $9B THEN ; EOL
      Acurse(colcrs,rowcrs)
      colcrs = 0
      Ascroll()                     
   ELSEIF areg = $0A THEN ; lf
      Acurse(colcrs,rowcrs)
      rowcrs ==+ 1
      Ascroll()
   ELSEIF areg = $08 THEN ; BS 
      IF colcrs > 0 THEN    
         Acurse(colcrs,rowcrs)
         colcrs ==- 1
         Ascroll()
      FI
   ELSEIF areg = $07 THEN ; bell
      ; do nothing
   ELSEIF areg = $09 THEN ; TAB
      Acurse(colcrs,rowcrs)
      colcrs = (colcrs + 8) & $F8
      Ascroll()
   ELSE
      Achr(colcrs,rowcrs,areg)
      colcrs ==+ 1
      Ascroll()
   FI
   ~[LDY 1 RTS]  

PROC Anofunc()
   ~[RTS]        

PROC Adummy()
   ~[LDY 1 RTS]

PROC Ahandler()
   BYTE ARRAY hatabs = $031A
   BYTE pos, found
   ;do not change the following 3 lines
   CARD ARRAY atab(6)
   BYTE Jmp = ~[JMP]
   CARD init
   ; define device entry points
   atab(0) = Aopen - 1       ;OPEN
   atab(1) = Aclose - 1      ;CLOSE
   atab(2) = Anofunc - 1     ;READ
   atab(3) = Aput - 1        ;WRITE
   atab(4) = Adummy - 1      ;STATUS
   atab(5) = Anofunc - 1     ;SPECIAL
   init = Adummy             ;INIT
   ; find entry in hatabs
   found = 0;
   pos = 0
   WHILE (pos < 34) AND (found = 0)
   DO
       IF hatabs(pos) = 0 THEN
          found = 1
       ELSE
          pos ==+ 3
       FI
   OD
   IF found = 0 THEN
       PrintE("*** A: too many devices")
   ELSE
       hatabs(pos) = 'A
       hatabs(pos + 1) = atab & 255
       hatabs(pos + 2) = atab RSH 8
   FI
RETURN

;*******************************
;*  MAIN PROGRAM
;*******************************

MODULE

BYTE
   ch = $02FC,
   bcount = $02EB,
   speed = ~[1],
   wsize = ~[0],
   sbits = ~[0],
   lf = ~[0],
   iparity = ~[0],
   oparity = ~[0]     
   
; iocb 3 definitions 
BYTE iocb3cmd=$372 ; cmd byte
CARD iocb3buf=$374,; buffer address
     iocb3len=$378 ; buffer length

DEFINE BUFLEN = "1024"
BYTE ARRAY BUFFER(BUFLEN)
                                 
PROC CIO=$E456(BYTE areg, xreg)

PROC init_R(); set options for R:
   Close(3)
   Open(3,"R:",13,0)
   XIO(3,0,38,lf*64+oparity+4*iparity,0,"R1:")
   XIO(3,0,36,speed+7+wsize*16+128*sbits,0,"R1:")
   XIO(3,0,34,192,0,"R1:")
   iocb3cmd=40 ; start concurrent I/O
   iocb3buf=BUFFER
   iocb3len=BUFLEN
   CIO(0,$30)  ; *** call CIO ***
   bcount = 0
RETURN            

PROC init_A(); set up A: device
   Ahandler() ; install A: handler
   Close(2)
   Graphics(8+16)
   Open(2,"A:",8,0)
RETURN

PROC intro()  
   Close(7)
   Open(7,"K:",4,0)
   init_R()
   init_A()
RETURN


BYTE FUNC remote(); remote char?
   XIO(3,0,13,0,0,"R:")
   IF bcount = 0 THEN
      RETURN(0)
   FI
RETURN(1)

PROC do_remote(); process remote
   BYTE char
   char = GetD(3)
   PutD(2,char)
RETURN

BYTE FUNC local() ; local char?
RETURN($FF - ch)

PROC do_local(); process local
   BYTE char 
   char = GetD(7)
   IF char = 127 THEN     ;tab
      char = 9
   ELSEIF char = 125 THEN ;left curl
      char = 123
   ELSEIF char = 255 THEN ;right curl
      char = 125
   ELSEIF char = 96 THEN  ;tilde
      char = 126
   ELSEIF char = 126 THEN ; delete
      char = 127
   FI
   PutD(3,char)
RETURN

PROC main()
   intro()
   DO
      IF remote() THEN
         do_remote()
      ELSEIF local() THEN
         do_local()
      FI
   OD
RETURN
```
  
