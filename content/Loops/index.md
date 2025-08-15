---
title: Loops
---
# Loops in Forth  
  
%%tabbedSection  
%%tab-english  
I found this small Basic Program in the book "Spielend Programmierer Lernen" from Karl-Heinz Koch:  
  
```
10 PRINT CHR$(125)
15 POKE 82,0
20 FOR ZE=0 TO 20
30 FOR SP=0 TO 39
40 POSITION SP,ZE
50 X=INT(RND(0)*26)+65
60 ? CHR$(X)
70 NEXT SP
80 NEXT ZE
```
  
The Program fills the screen with random characters. It uses two nested loops for this.  
  
```
  $D20A C@ ;

\\ Random Numner 0..n-1
: RANDOM ( n -- 0..n-1 )
  RND $100 * RND + UM* NIP ;

: POS ( x y -- ) \\ Position Cursor
  $54 C! $55 ! ;

: CLS ( -- )  \\ Clear Screen
  &125 EMIT ;

: LMARGN ( n -- ) \\ Set left margin
  &82 C! ;

: LOOP-DEMO
  CLS
  0 LMARGN
  21 0 DO
    40 0 DO
      I J POS
      26 RANDOM 65 + EMIT
    LOOP
  LOOP ;
  }}}
  
LOOP-DEMO is the main program. Words to place the coursor and to read a random number, which both are build in the Atari Basic, need to be added to the VolksFORTH Kernel (this means if a programs does not need these functions, they can be left out to save memory)

The Forth words I and J read the loop indicies. I is the index of the inner loop, J is the index of the outer loop. The Forth Program is done without any variables, all values are passed on the Stack

/%
%%tab-german

Diesmal behandeln wir Schleifen. Dieses kleine Programme habe ich Buch "Spielend Programmierer Lernen" von Karl-Heinz Koch gefunden: 

{{{
10 PRINT CHR$(125)
15 POKE 82,0
20 FOR ZE=0 TO 20
30 FOR SP=0 TO 39
40 POSITION SP,ZE
50 X=INT(RND(0)*26)+65
60 ? CHR$(X)
70 NEXT SP
80 NEXT ZE
```
  
Das Programm schreibt den Bildschirm mit zufälligen Buchstaben voll. Hierzu werden zwei verschachtelte Schleifen benutzt.  
  
In Forth sieht das Programm so aus:  
  
```
: RND ( -- n ) \ Random Number 0-$FF
  $D20A C@ ;

\ Random Numner 0..n-1
: RANDOM ( n -- 0..n-1 )
  RND $100 * RND + UM* NIP ;

: POS ( x y -- ) \ Position Cursor
  $54 C! $55 ! ;

: CLS ( -- )  \ Clear Screen 
  &125 EMIT ;

: LMARGN ( n -- ) \ Set left margin
  &82 C! ;

: LOOP-DEMO
  CLS
  0 LMARGN
  21 0 DO
    40 0 DO
      I J POS
      26 RANDOM 65 + EMIT
    LOOP
  LOOP ;
```
  
LOOP-DEMO ist das eigendliche Programm. Befehle zum Positionieren des Cursors und Erzeugen einer Zufallszahl, welche in Atari-Basic eingebaut sind, befinden sich nicht im volksForth Kern und werden daher im Programm definiert (d.h. auch, bei Programmen, welche diese Befehle nicht benötigen, wird kein Speicherplatz verbraucht)  
  
Die Forth Wörter I und J liefern die Schleifen-Indizes. I liefert den Index der innersten Schleife, J den Index der äußeren Schleife. Das Forth-Programm kommt ganz ohne Variablen aus, da alle Werte über den Stapelspeicher (Stack) übergeben werden.  
  
/%  
/%  
