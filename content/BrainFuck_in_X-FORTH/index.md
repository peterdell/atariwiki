---
title: BrainFuck in X-FORTH
---
General Information   
Author: 	Carsten Strotmann   
Language: 	FORTH   
Compiler/Interpreter: 	XFORTH   
Published: 	2003   
  
### BrainF*ck  
  
BF is a very minimalistic language, with only eight commando's, yet it is (theoretically) powerfull enough to compute anything that can be computed (with a Turing Machine). The language operates on an array of memory cells each containing an initially zero integer value. There is a memory pointer which initially points to the first memory cell.  
  
## Resources  
  
Tom Hunt has another [BF implementation](http://cth.dtdns.net/mouse/) for the A8 written in CC65 (see bottom of page).  
  
a new Atari BrainFuck was written by Pawel "Cosi" Piatkowski, [Announcement in Polish](http://atarionline.pl/v01/index.phtml?subaction=showfull&id=1216645285&archive=&start_from=&ucat=1&ct=nowinki), download of atr with English manual and program file [here](http://atarionline.pl/v01/index.phtml?ct=utils&sub=4.+Programowanie&tg=Brainfuck#Brainfuck).  
  
  
- [Wikipedia Entry on BrainF*ck|http://www.wikipedia.org/wiki/Brainfuck_programming_language]  
- [The BrainF*ck Archive|http://esoteric.sange.fi/brainfuck/]  
- [A Page about BrainF*ck|http://home.planet.nl/~faase009/Ha_BF.html]  
- [Another Page about BrainF*ck|http://www.catseye.mb.ca/esoteric/bf/]  
- [Deutsche Infos zu BrainF*ck|http://www.loaderror.org/bf.htm]  
  
## How to use  
Each of the eigth commands consists of a single ASCII character, with the following meaning:  
  
- '>' : move the memory pointer to the next cell,  
- '<' : move the memory pointer to the previous cell,  
- '+' : increment the memory cell under the memory pointer,  
- '-' : decrement the memory cell under the memory pointer,  
- ',' : fills the memory cell under the memory pointer with the ASCII value of next character from the input,  
- '.' : writes the contents of the memory cell under the memory pointer as a character with the corresponding ASCII value,  
- '~['_:_moves_to_the_command_following_the_matching_'~](../'_:_moves_to_the_command_following_the_matching_'~/index.md)', if the memory cell under the memory pointer is zero, and  
- '~]' : moves to the command following the matching '~[', if the memory cell under the memory pointer is not zero.  
  
All commands are executed sequentially, except when specified differently. Other characters are skipped, thus considered as comments. The execution terminates when the end of the program is reached.  
  
This interpreter is written in XFORTH  
  
__Download__: [bf.atr](attachments/bf.atr)  
  
From MyDOS, start BF.COM, then BF" D:filename.BF"  
  
Have fun!  
  
---
  
# Source (X-FORTH)  
  
```
( Brainf*ck in FORTH      )
( 2003, Carsten Strotmann )

CR ." BrainF*ck "

0 VARIABLE IP

: IP+ IP @ 1+ IP ! ;
: IP- IP @ 1 - IP ! ;
: IP@ IP @ C@ ;

: 2DUP DUP DUP ;

: BF+ 2DUP C@ 1+ SWAP C! ;
: BF- 2DUP C@ 1 - SWAP C! ;
: BF> 1+ ;
: BF< 1 - ;
: BF. DUP C@ EMIT ;
: BF, DUP KEY SWAP C! ;
: BF[ DUP C@ 0= IF
        BEGIN IP+ IP@ 93 = UNTIL
      THEN ;
: BF] BEGIN IP- IP@ 91 = UNTIL ;

." .." 

: BFI ( addr -- )
  IP ! BEGIN
    IP@ 93 = IF BF] THEN
    IP@ 91 = IF BF[ THEN
    IP@ 62 = IF BF> THEN
    IP@ 60 = IF BF< THEN
    IP@ 46 = IF BF. THEN
    IP@ 44 = IF BF, THEN
    IP@ 45 = IF BF- THEN
    IP@ 43 = IF BF+ THEN
    IP+
    IP@ 0  = UNTIL ;

." .."

: BF 
  HERE 3000 ERASE 
  HERE 
  BL WORD 1+ BFI ;

." .."
HEX

: BFR
  6000 1000 ERASE
  7000 1000 ERASE
  BEGIN 
    6000 1000 SOURCE-ID @ READ-FILE
    128 < WHILE
    DROP 7000 6000 BFI
  REPEAT
;

." .."

: BF"
  FILE" R/O OPEN-FILE
  128 < IF
    SOURCE-ID !
    BFR
    SOURCE-ID @ CLOSE-FILE
    0 SOURCE-ID !
  ELSE
    ." Error open file"
  THEN ;

." loaded!" CR
```
  
