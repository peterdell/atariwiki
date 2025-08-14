### General Information  
Author: Brian Abbot  
Language: ACTION!  
Compiler/Interpreter: ACTION!  
Published: ANTIC Vol. 3, #7 (11/ 84)  
---
# Demo: Pretty  
  
I've been programming with Action! for a few months now and wrote the following demonstration program, which shows the speed of the Action! language.  This routine puts three thick bars on the screen.  They will rotate upward in 128 unbroken colors while the background colors move down.  
  
  
Try running this in a dark room for best results.  This might be just the thing to show the kid down the street with his brand new Apple IIc.  But don't forget to remind him that his jaw is on the floor.  
```
PROC pretty()
   DEFINE key="Peek(764)<255"
   CARD sc
   BYTE wsync=$D40A,
        vertcnt=$D40B,
        color0=$D01A,
        color1=$D018,
        counter, chgcolor,
        upcolor, i, loop,
        downcolor
   Graphics(23)
   Poke(764,255)
   sc=PeekC(88)
   SetBlock(sc+75*40,40*20,255)
   SetBlock(sc+37*40,40*20,255)
   SetBlock(sc,40*20,255)
   DO
   FOR counter=1 to 9
      DO
      upcolor=chgcolor
      downcolor=chgcolor
         DO
         wsync=0
         color0=downcolor
         color1=upcolor
         upcolor==+1
         downcolor==-1
         UNTIL vertcnt&$80
         OD
      OD
   chgcolor==+1
   UNTIL key
   OD
RETURN
```
