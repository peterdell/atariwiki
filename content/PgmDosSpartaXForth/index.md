  
# Accessing Sprta DOS from XForth  
  
  
## Source Library SPARTA.F  
  
This is a library of the Basic Sparta DOS Access Routines  
  
- {{{?SPARTA}}} Tests if this is Sparta DOS  
- {{{COMTAB}}} Returns the Address of the COMTAB Datastructure  
- {{{BUFOFF}}} Returns the Address of the BUFOFF (Buffer Offset) Pointer  
- {{{ZCRNAME}}} get the next Filename/Parameter from the commandlinebuffer to acces by FNAME or PARM  
- {{{GETPARM}}} internal Routine, should not be used directly  
- {{{FNAME}}} returns Address and Length of the current Parameter as a Filename (with Dx:)  
- {{{PARM}}} returns Address and Length of the current Parameter (without Dx:)  
- {{{RESETBUF}}} reset the Buffer Pointer to zero, to restart reading of commandline  
- {{{PARAMS}}} returns the number of commandline parameters  
- {{{(TIME)}}} internal routine to access time structure  
- {{{HOUR}}} get the current hour after call to VDTIME  
- {{{MINUTE}}} get the current minute after call to VDTIME  
- {{{SECOND}}} get the current second after call to VDTIME  
  
```
( Sparta DOS routines )

: ?SPARTA ( -- f )
  ( returns 1 if this is Sparta DOS )
  HEX 700 DECIMAL C@ 83 = ;

: COMTAB ( -- addr )
  ( gets CPMTAB base address )
  10 @ ;

: BUFOFF ( -- addr )
  ( adress of bufferoffset )
  COMTAB 10 + ;

: ZCRNAME ( -- )
  ( gets next cmd-line parm to COMFNAME )
  COMTAB 3 + CALL DROP ;

: GETPARM ( addr -- addr n )
  ( gets current parameter, needs address  )
  DUP DUP DUP 28 + SWAP
  DO
    I C@ 155 =
             IF I LEAVE THEN
  LOOP SWAP - ;

: FNAME ( -- addr n )
  ( get next param as filename )
  COMTAB 33 + GETPARM ;

: PARM ( -- addr n )
  ( get next param without Dx: )
  COMTAB 36 + GETPARM ;

: RESETBUF ( -- )
  ( Resets buffer offset )
  0 BUFOFF C! ZCRNAME ;

: PARAMS ( -- n )
  ( number of parameters on the cmd-line )
  RESETBUF
  0 BEGIN
     ZCRNAME PARM SWAP DROP
     DUP IF
          SWAP 1+ SWAP
         THEN
    0= UNTIL
    RESETBUF ;

: (TIME) ( n -- time )
  ( internal routine to access time )
  COMTAB + C@ ;

: HOUR ( -- hh )
  ( get the current hour )
  16 (TIME) ;

: MINUTE ( -- mm )
  ( get the current minute )
  17 (TIME) ;

: SECOND ( -- ss )
  ( get the current seconds )
  18 (TIME) ;

CR ." Sparta DOS Extensions loaded..." CR

```
  
## XFORTH Extension LAUNCH  
  
This can be used to create a new FORTH with is able to start a FORTH Sourcefile from the Sparta-DOS commandline.  
  
__Example__  
```
{{{
( LAUNCH FORTH Source from Sparta DOS )
( Command line                        )

: LAUNCH ( -- )
  PARAMS ( do we have cmdline params? )
  IF     ( yes )
    CR ZCRNAME  ( get next filename )
    FNAME INCLUDED ( and include )
  ELSE
    QUIT ( jump to interpreter )
  THEN ;
```
  
## Testscript for the Sparta DOS Extension (PARAM.F)  
  
This little test script prints the commandline contents. This also shows how to use the commands.  
  
__Usage:__ XFORTHS PARAM.F test1 test2 test3  
```
: SPARTA-TEST
  PARAMS
  IF
   ." PROGRAMM: " FNAME TYPE CR
   PARAMS . ." Commandline Parameter(s)" CR
   PARAMS 1+
   1 DO
   ZCRNAME I . ." PARAM: " PARM TYPE CR
   LOOP
  ELSE
   ." NO PARAMETER" CR
  THEN
;

CR
SPARTA-TEST
MON
```
  
## Script to save a new FORTH with Sparta DOS Extensions  
  
This Script saves the current FORTH image on memory to disk.  
  
To have an extended FORTH follow these steps:  
  
1. start XFORTH  
1. INCLUDE" D1:SPARTA.F"   -- includes the Sparta DOS Extensions  
1. INCLUDE" D1:LAUNCH.F"  -- includes the Launch feature  
1. INCLUDE" D1:MKFRTH.F"  -- saves the new FORTH as "XFORTHS.COM"  
  
```
( MAKEFORTH Script )
( 2001-2003 CAS    )
( for X-FORTH 1.x  )
( and Sparta DOS   )

BASE @         ( SAVE BASE )
HEX            ( switch to Hexadecimal)
CR CR CR       ( print message )
CR ." MAKEFORTH 1.0 "
CR ." ------------- "

CR ." Save current FORTH as "
CR ." XFORTHS.COM"
CR
( Set Last word as init word )
LATEST PFA CFA ABORTINIT !

( Calculate FORTH Memory )
CR ." Forth MemLow " 0 +ORIGIN .
CR ." Last Command and MemHigh "
LATEST DUP .
C +ORIGIN !
HERE ." -> " .
HERE DUP 1C +ORIGIN !
         1E +ORIGIN !

( change Filename here )
FILE" D:XFORTHS.COM" W/O OPEN-FILE
CR ." File Open RC=" .

( create ATARi COM Fileheader )
FFFF 0600 !
02E0 0602 !
02E1 0604 !
0 +ORIGIN DUP 0606 ! 0608 !
1E +ORIGIN @ 1 - 060A !

DUP ( Save fileid)
0600 SWAP
CR ." Write Header RC="
0C SWAP WRITE-FILE .
DUP
0 +ORIGIN SWAP
1E +ORIGIN @ 0 +ORIGIN - SWAP

CR ." Write Forth RC="
WRITE-FILE .

CR ." Close File RC="
CLOSE-FILE .

CR ." Forth saved! "
CR

BASE !            ( restore BASE )
```
  
