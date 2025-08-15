---
title: Pen Music Challenge
---
# Abbuc Music Challenge  
  
The ABBUC Music challenge is a small game used during the ABBUC annual meeting in 2003. We had a MP3 music player with 8 Atari game music tracks. The player is presented with the game while listening to the music and must use a Lightpen to select the 8 tracks on the MP3 player.  
  
The program stores the score in PEN.DAT.  
  
All tracknames with an "*" appended are correct, all others are not correct.  
  
The program changes the default font to make the "*" invisible on the screen.  
  
This game was a quick hack, it is not necessary beautiful code. But it shows how to access the lightpen, how to store data and change a font using X-Forth.  
  
Download ATR: [pen.atr](attachments/pen.atr) (start PEN.COM from DOS)  
  
```
DECIMAL

: CUROFF
  1 752 C! ;
: CURON
  0 752 C! ;

: RTCLOCK 18 C@ 19 C@ 256 * 20 C@ + SWAP ;

: 0. ( n -- )
  ( print number with leading zero )
  DUP 10 <
  IF 48 EMIT 1 .R
  ELSE 2 .R THEN
;

: MINUTES
  RTCLOCK 50 M/ SWAP DROP
  3600 /MOD DROP
    60 /MOD SWAP DROP ;

: TIME RTCLOCK 50 M/ SWAP DROP
  3600 /MOD 0. 58 EMIT
    60 /MOD 0. 58 EMIT
            0.
;

: 2DUP OVER OVER ;
: $ @ ; ( ATARI++ no fetch )
: C$ C@ ;
: .. DUP . CR ;

( Misc Routines )

: POS ( y x -- )
  85 ! 84 C! ;
: @POS ( -- y x )
  84 C@ 85 @ ;
: STRIG0 644 C@ ;

: DELKEY ( k addr -- )
  DUP C@ IF 
    DUP C@ 1 - SWAP C! EMIT
  ELSE
    DROP
  THEN ;

: INKEY ( k addr -- )
  DUP
  C@ 1+ SWAP 2DUP C!
  + ROT SWAP C! ( Store Keyvalue )
;

: GETIN ( addr l -- )
 2DUP BLANKS
 @POS 663 ! 662 C! ( save curs pos )
 667 C!     ( store l )
 DUP 0 SWAP C! ( count byte = 0 )
 665 !      ( store addr )
 BEGIN
   KEY
   DUP DUP
   126 = IF
     665 @ DELKEY
   ELSE
     667 C@ 665 @ C@ - 0 > ( check l )
     IF
       665 @ INKEY 662 C@ 663 @ POS 
       665 @ COUNT TYPE
     ELSE
       DROP
     THEN
   THEN
 155 = UNTIL
;

: CLS 125 EMIT ;

( Lighpen routines and Music Competition )
HEX

: RANDOM ( -- r )
  D20A C@ 100 * D20A C@ + 
;

: RAND ( n -- r )
  RANDOM SWAP MOD ABS ;

9 VARIABLE FNAME 
44 C, 3A C, ( D: )
50 C, 45 C, 4E C, 2E C,
44 C, 41 C, 54 C, 00 C,
 ( Filename D:PEN.DAT )

0 VARIABLE FILEID
0 VARIABLE SELCOUNT
0 VARIABLE NAME 19 ALLOT 9B C,

: SCORE
  NAME 19 + ;
: CLOCK
  NAME 15 + ;

: SCREEN
  0 2C6 C! F 2C5 C! 
  0 52 C!
;
: TITEL
   1 1 POS ." ABBUC RAF ATARI Music Challenge 2003"
   2 1 POS ." ------------------------------------"
;

DECIMAL

: TRACKNAMES
  CLS
  TITEL

  05 01 POS ." PacMan*"
  05 21 POS ." DropZone"
  06 01 POS ." T.G.C.C.R.R"
  06 21 POS ." BallBlazer"
  07 01 POS ." Eidolon*"
  07 21 POS ." Koronis Rift"
  08 01 POS ." Aramroute*"
  08 21 POS ." Captain USA"
  09 01 POS ." Boulder Dash*"
  09 21 POS ." Seven Cities o.G."
  10 01 POS ." Gyruss*"
  10 21 POS ." Master of the Lamp*"
  11 01 POS ." Donkey Kong*"
  11 21 POS ." Asteroids"
  12 01 POS ." Mario Bros."
  12 21 POS ." Atari Pirates"
  13 01 POS ." Flight Simulator"
  13 21 POS ." River Raid*"
  14 01 POS ." Pitfall"
  14 21 POS ." Defender"
  15 01 POS ." Ms PacMan"
  15 21 POS ." Cervi"
  16 01 POS ." Master Blaster"
  16 21 POS ." Arkanoid"
;

: SETFONT
  756 C@ 256 * ( address of int. font )
  32768 1024 CMOVE ( copy to $8000 )
  32768 80 + 8 ERASE ( clear '*' )
  128 756 C! ( enable new font )
;


: NUM2ADDR ( n -- addr )
  12 /MOD 20 * SWAP 5 + 40 * + 
  88 @ + ( add screen address )
;

: EXCHANGE ( n1 n2 -- )
  ( exchanges two track entries )
  NUM2ADDR SWAP NUM2ADDR
  DUP PAD 20 CMOVE  ( n1 -> PAD )
  OVER SWAP 20 CMOVE ( n2 -> n1  )
  PAD SWAP 20 CMOVE ( PAD -> n2 )
;

: SHUFFLE
  20 10 POS ." Tracks werden gemischt"

  60 0 DO
         24 RAND 24 RAND EXCHANGE
       LOOP
;

HEX

: LOGIN
  CLS
  TITEL
  0A 0A POS ." Name:"
  NAME 13 GETIN
;

: LPENH 234 C@ ;
: LPENV 235 C@ ;

: PEN LPENH LPENV ;

DECIMAL

: PEN2CORD ( Calculates Screen Coord )
                  ( for LP )
                  ( y x -- y2 x2 )
  16 - 4 / SWAP
  72 - 4 / SWAP ;

: CORD2ADDR
  40 * + 88 @ + ;

: INVERT ( x y -- )
  CORD2ADDR
  DUP C@ 128 XOR SWAP C!
;

: LTRIG?
  632 C@ 14 = ;

: CONSOL
  53279 C@ 7 XOR ;

: TRACKPEN
    PEN PEN2CORD
    2DUP INVERT 
    23 08 POS TIME
    23 25 POS SELCOUNT @ .
    INVERT
;

: INVSEL
  PEN PEN2CORD SWAP
  20 / 20 * DUP 19 + SWAP
  DO DUP I SWAP INVERT LOOP
  DROP
;

: SELECT
  PEN PEN2CORD CORD2ADDR
  C@ 128 AND
  IF
    SELCOUNT @
    DUP IF 
      1 - SELCOUNT !
      INVSEL
    ELSE
      DROP
    THEN
  ELSE
    SELCOUNT @
    DUP 8 = IF
      DROP
    ELSE
      1 + SELCOUNT !
      INVSEL
    THEN
  THEN
;

: CHOOSE
  20 10 POS ." Waehle die 8 Tracks   "
  21 08 POS ." <START/OPT/SELECT>=ENDE"
  23 02 POS ." Zeit:"
  23 20 POS ." Ausw:"
  BEGIN
    TRACKPEN
    LTRIG? 
    IF 
     SELECT 
    THEN
    CONSOL
    MINUTES 2 =
  OR UNTIL
;

: CLEARSCORE
  0 SCORE ! ;

: CLEARSEL
  0 SELCOUNT ! ;

: GETSCORE
  24 0 DO
   I NUM2ADDR DUP 20 +
   SWAP DO
     I C@ DUP 128 XOR I C! 
       138 = IF
       SCORE C@ 1+ SCORE C!
     THEN
   LOOP
  LOOP
;

: CLEARCLOCK
  18 3 ERASE ;

: GETCLOCK
  18 CLOCK 3 CMOVE ;

: STRIGWAIT
  BEGIN
  STRIG0 0= UNTIL
;
: KEYWAIT
  BEGIN 
    KEY
  155 = UNTIL ;

: OK?
  DUP 0= IF 
    ." [OK]" DROP
  ELSE 
    ." [FAIL] " . 
  THEN
;

: SAVEFILE
  13 10 POS ." Open File  : "
  FNAME 2 + 0 W/O 1+
  OPEN-FILE DUP
  
  170 = IF
    DROP FNAME 2 + 0 W/O OPEN-FILE
  THEN
  OK?
  FILEID !
  14 10 POS ." Write Data : "
  NAME 28 FILEID @ WRITE-FILE OK?
  15 10 POS ." Close File : "
  FILEID @ CLOSE-FILE OK?
  16 10 POS ." Verify File: "
  FNAME 2 + 0 R/O OPEN-FILE OK?
  CLOSE-FILE OK?
;

: RESULT
  CLS
  TITEL
  08 10 POS ." Zeit      : " TIME
  GETCLOCK
  10 10 POS ." Wertung   : "
  SCORE C@ .
  12 10 POS ." Speichern... "
  SAVEFILE 
  20 06 POS ." RETURN fuer naechsten Spieler"
;

: START
  BEGIN
    SCREEN
    CURON
    LOGIN
    CUROFF
    SETFONT
    TRACKNAMES
    SHUFFLE
    CLEARSCORE
    CLEARSEL
    CLEARCLOCK
    CHOOSE
    GETSCORE
    RESULT
    KEYWAIT
  AGAIN
;

." PEN loaded ... "


```
