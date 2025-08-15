---
title: Read keyboard
---
# reading the keyboard from VolksForth  
  
(Basic taken from "Thomas E. Rowley - Atari Basic spielend lernen")  
  
## Basic Version  
```
10 REM read a keypress
20 PRINT "PRESS ANY KEY"
30 POKE 764,255
35 IF PEEK(764)=255 THEN 35
36 KEY=PEEK(764)
40 CLOSE #1:OPEN #1,4,0,"K:":GET #1,A
50 PRINT "The Key-Code of "; CHR$(A); " is "; KEY
60 GOTO 30
```
  
## volksForth version using direct memory access the same way as the BASIC example does  
```
: GETKEY ( read a keypress )
  ." Press any key" CR
  255 764 C!
  BEGIN
        764 C@
        255 < IF
           764 C@ 
           KEY ." The Key-Code of " DUP EMIT ."  is " . CR
           255 764 C!
        THEN
  REPEAT ;
```
  
alternative, more elegant version using the build in words "KEY?" and "KEY"  
  
```
: GETKEY ( read a keypress )
  ." Press any key" CR
  BEGIN
        KEY? IF
           764 C@ KEY 
           ." The Key-Code of "  DUP EMIT ." is "  . CR
        THEN
  REPEAT ;
 
```
