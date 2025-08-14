# CC65 Porting Ideas  
  
  
  
## Address Database  
  
Original Distribution Info  
```
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
My contact information:

Ga.per Raj.ek
gape.korn@volja.net

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Program title:

Address Book v1.0

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
File description:

Adress.c        - application main file
Adress.dat - user information
Help.dat        - help file
```
  
## Banner in C  
  
  
```
BANNER is a program makes banners to be printed on the line printer.

To run the program type
& banner

Then respond to the following questions -

output file : sign   The banner will be left in file 'sign'.
(If you just hit return this defaults to 'junk')
dot design : 2      The dots types are designated 0-9 and a-h (see below)
(This defaults to 5)
for a 4x3 dot the standard h & v overlaps are 1,1
h,v overlaps : 1,1   A greater h overlap decreases the banner length.
A greater v overlap decreases the banner width.
(Again, a <return> response gives the std. as default)
dot chars : ZM      'Z' & 'M' will be overprinted.
(Default here is '*O')
text : ab%c^      A banner file with chars "ab%c^" will be created.
(No default here)
print now? yes      The file will be printed.
(Defaults to no)
delete file? yes   The file will be deleted.

There are a few special features...

Banner Special Features

The char <esc> (or cntl-[, "^[") is used as an escape character
to specify special features.  On input type <esc> (or control [)
followed by the special characters listed below.  The <esc> will be
echoed as a dollar sign ('$') but is shown as <esc> below.

<esc>c      Begin capitalization (all letters forced to be caps)
<esc>-c      End capitalization (back to normal UPPER/lower case)
<esc>fNAME<nl>   Accept the contents of the file "NAME" as the text
<esc>u      Begin underlining.
<esc>-u      End underlining.
<esc>043<esc>   Include the char '#' (octal 43)
<esc>35<esc>   Include the char '#' (decimal 35)
<esc><esc>   Include the char <esc> (decimal 27)

Note that banner represents all 128 characters with graphic
equivalents, so chars like <esc> do produce output.

Dot Designs                    xx           xxx
xxx         xxxx          xxxxx
x          xxx          xx           xxx
dot0  1 x 1       dot1  3x2      dot2  4x3       dot3  5x3


xxxx       xxxxxxx        xxxxxxx
xxxxx           xx  xx      xxxxxxxxx       xxx     xxx
xxx xxx          xx     xx      xxxxxxxxx       xx      xx
xxx xxx           xx  xx      xxxxxxxxx       xxx     xxx
xxxxx            xxxx       xxxxxxx        xxxxxxx
dot4  7x4       dot5  8x5      dot6  9x5       dot7  9x5

xxxxxxxxxx       x xx
xxxxxxxxxxxx       xxx x
x   x         xxxxxx      xxxxxxxxxxxxxx       xxxx   x
x xxxxx x        xxxxxxxx      xxxxxxxxxxxxxx        x xxxxxxx x x
x xxxxx x       xxxxxxxxxx      xxxxxxxxxxxxxx       x x xxxxxxx x
x xxxxx x       xxxxxxxxxx      xxxxxxxxxxxxxx        x    xxxx
x xxxxx x        xxxxxxxx       xxxxxxxxxxxx      x xxx
x     x         xxxxxx        xxxxxxxxxx       xx x
dot8  10x6       dot9  10 x 6   dota  14 x 8       dotb  14 x 8

xx         xxxxxxxxxx    x    xx    x
xx  xx  xx        xxxxxxxxxxxx   xxxx  xx  xxxx          xxxxxxxxx
x x xxxx x x       xxxx      xxxx    xxxx    xxxx        x       x
x   xxxxxx   x       xx      xx      xxxxxxxx        x     xxx    x
x   xxxxxx   x       xx      xx      xxxxxxxx        x    x   x    x
x x xxxx x x       xxxx      xxxx    xxxx    xxxx        x     xxx    x
xx  xx  xx        xxxxxxxxxxxx   xxxx  xx  xxxx        x       x
xx         xxxxxxxxxx    x    xx    x          xxxxxxxxx
dotc  14 x 8       dotd  14 x 8   dote  14 x 8       dotf  14 x 8

xxxxxxxx          x
xx    xx  xx         xx
xx     xx   xx        xx
xxxxxxxxx   xx      xxxxxxxxxx
xx   xxxxxxxxx       xxxxxxxxxxx
xx   xx       xx       xxxxxxxxxxx
xx  xx      xx       xxxxxxxxxxx
xxxxxxxx       xxxxxxxx
dotg  14 x 8       doth  14 x 8


Peter S. Langston
Commercial Union Leasing Co
645 Madison Ave
New York, New York, 10022
```
  
## Calculators  
  
### calc.c  
Powerfull arithmetik calculator with variables and functions. Compiles, but needs work on static local variables.  
  
### calculator.c  
This source needs a mathlib. Mathlib is not available to cc65 this time. Anyone interested in writing one?  
  
### rpncalch.c  
A RPN Calculator. Compiles. Needs some finishing work.  
  
### dc.c  
Desk calculator. Supports +,,* and / on integer and floating point. Compiles, but needs work.  
  
### rpn.c  
This is a program to emulate an RPN (Reverse Polish Notation) calculator with full functions of an HP-67, but with unlimited stack and program space.  
  
  
## Screen Editor in C  
  
A Screen Editor in C, similar to Wordstar. Code from 1982, with 68k Assembler parts. Needs more work.  
  
  
## The Game Gomoku  
  
Gomoku is played on a square board labelled with letters across the top and numbers down the side.  Moves are entered as  
"letter-number" of the desired spot.  
  
e.g.  "j10" is a play in the center of a 19x19 board.  
  
The object of the game is to get 5 (and only 5) plays in a row. Players alternate making moves on the board until one has five (not six) in a row.  (note that a stalemate is possible, especially on small boards.)  
  
The program learns to play by analysing its losses and watching out for them in the future.  Consequently it will play rather badly at first, knowing only that it has lost if you get five in a row.  But it will be happy to lose to you since it can only learn what you show it.  
  
Type "?" in place of your move to reprint the board.  
  
  
  
## The game of Mancala in C  
  
  
Readme:  
  
README for Bill's Mancala  
  
OK, I saw Scott Sauyet's post in rec.games.abstract about Mancala and  
decided to write a computer program to play against to get a feel for the  
game.  I know it sucks, but I played it a few times and it beats me when it  
looks ahead two moves so I don't care.  
To compile:  
gcc -O2 mancala.c ab.c rnd.c -o mancala  
  
To run:  
mancala <player 1 lookahead> <player 2 lookahead>  
  
where lookahead of 0 means a human plays.  Player 1 is the top row, player 2 is the bottom.  For example.  
  
  
| | |   | |  
|mancala |0 |2   |means you go first, and the computer looks ahead 2 moves.|  
|mancala |4 |0   |means you go second, and the computer looks ahead 4 moves.|  
|mancala |3 |3   |Watch the computer play itself!|  
|mancala |7 |1   |Watch how badly a smart computer beats a dumb one!|  
  
  
ABOUT THE PROGRAM  
ab.c is the alpha-beta search engine.  It doesn't prune or extend the searches of interesting paths.  
  
mancala.c is the "hooks" for the search engine and the user interface  
(if you can call it that).  To evaluate the worth of a move it just returns  
the number of stones you got to put in your scoring pit (you can tell I  
didn't try real hard to be clever here).  
  
  
rnd.c is a random number generator I had lying around.  I used it to  
keep the computer from playing _exactly_ the same moves every game.  
  
Let me know what you think!  But be nice...remember, I only spent an hour  
on this.  If I spent two hours it'd be _way_ more impressive.  
  
-Bill (wms@ssd.intel.com)  
  
PS - It plays the rules as Scott posted them.  They were kind of vague;  
for example, what happens when you have no legal move?  The program  
then forces you to pass.  If you don't like this feel free to change it.  
  
  
```
From SSAUYET@eagle.wesleyan.edu Wed Aug 24 22:16:31 1994
Newsgroups: rec.games.abstract
Subject: Mancala (Rules and Request for Variations)
From: SSAUYET@eagle.wesleyan.edu (Scott D. Sauyet)
Date: 23 Aug 94 11:26:32 -0400
Distribution: world
Organization: Society For Pronounceable Acronyms (SFPA)
Nntp-Posting-Host: wesleyan.edu
X-News-Reader: VMS NEWS 1.20Lines: 118

This sentence contains the only use of the word "checkers" in the
entire post.	:-)

Okay, I've heard occasional discussions about mancala here before,
enough that when I heard that they were playing it the next blanket
over on the beach, I knew not only that it was an African game but
that stones were moved from one hole to another over the course of the
game.  I even knew that there were many variants on the game on the
same board.  But I'd never seen it before.

So I watched several games and was invited to try my hand at it.  Now
I'm hooked.  Sometime next month I will make myself a board.  But I
want to know more variations than the one I currently know.  I will
describe below the game I learned; if you know others, please let me
know.

For those who've never seen one, a mancala board is a narrow rectangle
with forteen holes in it -- a large one at either of the shorter ends
and two rows of six smallers ones.  (Are there variations on the
number of holes as well?)  At the beginning of the game there are four
stones in each of the twelve smaller holes.  There are two players.  I
will name them Top and Bottom.  Each owns the larger hole on her right
(called her mancala.)  Here is my ascii version:

				  T1		T2		T3		T4		T5		T6
  -----------------------------------------------------------------
  |		 | O	O | O	O | O	O | O	O | O	O | O	O |		 | 
  |		 |		 |		 |		 |		 |		 |		 |		 | 
  |		 | O	O | O	O | O	O | O	O | O	O | O	O |		 | 
  |		 |-------+-------+-------+-------+-------+-------|		 |
  |		 | O	O | O	O | O	O | O	O | O	O | O	O |		 | 
  |		 |		 |		 |		 |		 |		 |		 |		 | 
  |		 | O	O | O	O | O	O | O	O | O	O | O	O |		 |
  -----------------------------------------------------------------
	  ^		  B6		B5		B4		B3		B2		B1		  ^
	  |__ (belongs to Top)					  (belongs to Bottom) __|

(The labels for the holes are my own invention for recording the game. 
It's actually a simple board with holes carved out.  And when I say
holes, I really mean indentations which hold 15-20 stones, or more in
the case of the mancalas.  And when I say stones, I really mean glass
beads like those that come with a Pente board.)

For convenience, though, I see no need to repeat that ascii board in
exposition, so I will use what I hope is the obvious shorthand:

 |  0- 4- 4- 4- 4- 4- 4	  |
 |	  4- 4- 4- 4- 4- 4- 0  |	(This is the starting position)

The goal of the game is to collect as many of the stones as possible. 
When one player cannot move (i.e. when the six holes on her side are
empty) the game ends and each player gets all the stones on her side
of the board and in her mancala.  Whoever has the most wins. 

A move consists of of removing all the stones from one of the six
normal holes on your side of the board, then, moving counterclockwise,
dropping one stone into each hole you encounter including your own,
but not your opponent's, mancala.  The move ends when you've dropped
all the stones.  If you end the move by dropping one in your mancala
you move again.  If you end the move by dropping the last stone in an
otherwise empty hole on your side of the board you collect all the
stones from the adjacent hole on your opponent's side; you place these
in your mancala.  That's it, the entire set of rules.

Here's a sample opening (with no suggestion that it is good or bad):

 |  0- 4- 4- 4- 4- 4- 4	  | <-- (starting position)
 |	  4- 4- 4- 4- 4- 4- 0  |	Top moves T4

 |  1- 5- 5- 5- 0- 4- 4	  |	The move ended in the mancala -- Top
 |	  4- 4- 4- 4- 4- 4- 0  |	moves again, say T1

 |  2- 0- 5- 5- 0- 4- 4	  |	Now it's Bottom's turn.
 |	  5- 5- 5- 5- 4- 4- 0  |	Bottom moves B5

 |  2- 0- 5- 5- 0- 4- 4	  |	Ended in the mancala, so Bottom again:
 |	  5- 0- 6- 6- 5- 5- 1  |	B1 -- this ends Bottoms turn.

 |  2- 0- 5- 6- 1- 5- 5	  |	This was probably a bad move as it
 |	  5- 0- 6- 6- 5- 0- 2  |	allows Top this one:  T6

 |  7- 1- 6- 7- 2- 6- 0	  |	As this ended on the empty T1, Top
 |	  0- 0- 6- 6- 5- 0- 2  |	collected all the stones from B6

We can easily record mancala games with this system, e.g. the above is
simply T4,T1,B5,B1,T6,??.  For a one-line storage of a position, I
would suggest the following as a recording of the last position shown:
"B|07|01,06,07,02,06,00|00,00,06,06,05,00|02".  Perhaps with ';'
instead of '|'.  The initial 'B' says that it is Bottom's move.

I should note that a player continues to move as long as she continues
to end in her mancala -- she can make many consecutive moves, e.g.
>from this position:

 | 12- 1- 1- 0- 4- 5- 6	  |
 |	  5- 3- 0- 6- 0- 1- 8  |

Top has the following string of moves:  T1, T4, T1, T2, T1, T5, T1,
T6, T1, T2, T1, T3, T1, T2, leaving this won position:

| 30- 1- 0- 0- 2- 1- 0	  |
|	  0- 3- 0- 6- 0- 1- 8  |	

(We know this is won since Top already has more than half of the
stones in her mancala.)

One more note is that 13 is a lucky number in this game.  If you have
a hole with 13 stones and the opponent's adjacent hole has N stones,
by moving the 13 you add N + 2 stones to your mancala -- try it. 
(Remember that you don't drop stone's in your opponent's mancala.)


Well that's the game.  If anyone has made a board, I'd love to hear
about it.  And most importantly, I'd really like to hear about other
games on this board.
 __		  ___	 
(_	c o t  |		Are the last three words of		 ssauyet@eagle
__) a u y e |	this sentence "used or mentioned?"	.wesleyan.edu

```
  
## Towers of Hanoi in C  
  
Example of recursion in C. Sourcecode compiles and runs on ATARI.  
But how about adding some graphical "sugar"?  
  
More on the game:  
  
http://obelix.ee.duth.gr/~apostolo/TowersOfHanoi/  
  
http://www.cut-the-knot.com/recurrence/hanoi.shtml  
  
http://www.mazeworks.com/hanoi/index.htm  
  
  
  
## Mienv and Tierra in C  
  
  
```
Title:          Minev
Version:        1.0
Entered-date:   June 3, 1996
Description:    Semi-clone of Tierra (strictly conforming ANSI C).
Should run on almost any ANSI C system.
Keywords:       Tierra, artifical life, genetic algorithm
Author:         inglesra@frc.com (Raymond Ingles)
sorceror@tir.com (Raymond Ingles)
Maintained-by:  inglesra@frc.com (Raymond Ingles)
sorceror@tir.com (Raymond Ingles)
Primary-site:   ftp.cs.vu.nl
Alternate-site: ftp.hampshire.edu,minix1.hampshire.edu
Original-site:
Platform:       ANSI C
Copying-policy: Public domain


*********************************************************
* MINEV - THE SMALLEST TIERRA-STYLE ALIFE PROGRAM EVER! *
*********************************************************

by Ray Ingles
inglesra@frc.com, sorceror@tir.com

This program is designed to compile and run on *any* ANSI C system, no
matter how minimal. To the best of my knowledge, it uses only ANSI
constructs and exceeds no minimum limits. I haven't found anything smaller
than an 8086 IBM PC running DOS 3.1 to run it on, but it works on that.
(See "TECHNOTE" for a list of tested machines, along with some
benchmarks.)

Minev is public domain software. You can do anything you like with it.
If I actually thought anyone could make money with it, I might put it
under the GPL, but I'm not *that* proud of it. I just hope that someone
out there will find it interesting.

This document assumes you know what Tierra is, and how it works. (If you
don't, read the "INTRO" document first.) It mainly describes the
differences between Tierra and minev. Minev is *not* a 16-bit port of
Tierra - that probably isn't possible. It is a from-scratch
reimplementation, using ideas gleaned from the Tierran literature.

Special note: The power supply on my Minix laptop failed catastrophically
midway into development. I can't absolutely confirm that this will run
on <386 Minix, unfortunately. It runs on an 8086 PC in DOS, though, so I
think it will work out all right. Two possible problems: If minev hangs
on startup, try setting ZERO_SOUP (in consts.h) to 0. Also, if you get
problems with data getting corrupted, try changing NUM_CPUS (also in
consts.h) to a smaller value. Please let me know if you discover any
problems! I will hopefully have my system back up soon.

WHAT GOES WHERE

This distribution includes the following directories and files:

top level:
README.1st     - This file
minev.lsm      - A "Linux Software Map" description of Minev
BUGS           - A list of some known misfeatures of minev

"doc" directory:
INTRO          - An introduction to the basic concepts of Tierra/Minev
TECHNOTE       - Notes on Minev's design and implementation
bench[123].txt - Scripts for benchmarking minev

"genomes" directory:
GENFRMAT  - A short file describing the format of genome files
Various genomes, including:
gen22.gen - One of the smallest genomes possible
gen53.gen - A Minevian parasite
gen82.gen - The original Minevian ancestor

"src" directory:
The source and makefiles for minev (see below: I. "INSTALLING MINEV")

I. INSTALLING MINEV

A. For unix-type systems, just edit the Makefile, uncommenting the
sections appropriate to your machine. Porting (if needed) should be
fairly straightforward if your machine isn't listed, but do read the
"TECHNOTE" (in the 'doc' directory) before you try.

B. For VMS systems, a mimimal "vaxmake.com" file is included. Invoke it
with the command "@vaxmake". (You will have to edit the string at the
beginning to point to the directory you will install minev into. You
can simply remove this line if you don't intend to pass any scripts
to minev on the command line.) Note: testing on VMS has been pretty
minimal; I'd be interested to hear reports of how it works in the
field.

C. For DOS systems, project files for Power C ("minevpow.prj") and
Pacific C ("minevpac.prj") are included. Just go ahead and fire
them up. Pacific C gives a couple warnings (unreachable code, etc.)
but it's safe to just ingnore them.
If you are using some other compiler, you're on your own. You
should be able to use the "tiny" or "small" memory model.

II. USING MINEV

A. There aren't a whole lot of commands for minev. The 'Help' command
is pretty straightforward, and gives you a quick summary of all the
commands available. (Just type 'Help' or '?' at the prompt.)

Here's a sample run:

- How many instructions have been executed
|         - How many slots in the soup are full
|        |   (Includes live organisms and allocated children)
|        |         - How many organisms (CPUs) there are
|        |        |
v        v        v
Insts: 0, Soup: 0, Orgs: 0
>>Init gen82.gen
Seeded soup at address: 10000
Insts: 0, Soup: 82, Orgs: 1
>>Init gen82.gen 0
Seeded soup at address: 0
Insts: 0, Soup: 164, Orgs: 2
>>Go 500
Insts: 5000, Soup: 2290, Orgs: 14
>>Orgs
Insts: 5000, Soup: 2290, Orgs: 14
>>Write mystate
Insts: 5000, Soup: 2290, Orgs: 14
>>Q

First we load the soup with the genome 'gen82.gen'. It has a default
address of 10,000. Then we load another copy of gen82.gen, overriding
the default address and placing it at address 0 in the soup. We then
run the simulator for 500 slices (i.e. 5000 instructions, at the
default value of 10 instructions per timeslice). Next we write out the
genomes that have more than five present (the default threshold to
write out an organism). Finally, we save the current state of the
system (In the file 'mystate.st') and quit.
(Note: ANSI C doesn't know about directories, so neither does
Minev. Any genome file you load must be present in the same directory
as Minev itself, and any output files Minev writes will be in that
directory too.)

B. If you give minev a filename on the command line, minev will read
commands from that file. Otherwise, it will read them from standard
input. Thus, the command 'minev script.txt' will cause minev to
read commands from the file 'script.txt'. A few sample scripts are
provided as benchmarks which you can use to find out how fast your
system is compared to some others I've tested.

C. The opcodes provided, with their default ordering, are as follows:

0x00: nop0  -- No-op zero. Used in templates.
0x01: nop1  -- No-op one. Used in templates.
0x02: pusha -- Push AX register onto stack.
0x03: pushb -- Push BX register onto stack.
0x04: pushc -- Push CX register onto stack.
0x05: pushd -- Push DX register onto stack.
0x06: popa  -- Pop stack into AX register.
0x07: popb  -- Pop stack into AX register.
0x08: popc  -- Pop stack into AX register.
0x09: popd  -- Pop stack into AX register.
0x0a: movii -- Copy the data in [BX+CX] to [AX+CX].
0x0b: inc   -- Increment CX register.
0x0c: dec   -- Decrement CX register.
0x0d: zeroc -- Set CX register to zero.
0x0e: lowc  -- Flip the low-order bit of CX.
0x0f: shl   -- Shift CX left.
0x10: ifz   -- If CX is zero, execute next instruction, otherwise skip.
0x11: jmp   -- Jump outward to nearest template.
0x12: jmpf  -- Jump forward to nearest template.
0x13: jmpb  -- Jump backward to nearest template.
0x14: call  -- Push current address onto stack, jump outward to template.
0x15: ret   -- Pop stack into ip. (Jump to (address on stack)+1.)
0x16: adr   -- Search outward for template, put address following in AX.
0x17: adrb  -- Search forward for template, put address following in AX.
0x18: adrf  -- Search backward for template, put address following in AX.
0x19: mal   -- Allocate soup - prefer address in AX, size in CX, address

0x1a: div   -- Allocate cpu for child, allow parent to allocate another.
0x1b: swap  -- Swap the top two elements on the stack.
0x1c: dup   -- Duplicate the top element on the stack.
0x1d: add   -- Add contents of DX to CX.
0x1e: sub   -- Subtract contents of DX from CX.
0x1f: ifl   -- If the last instruction produced an error, execute the


I'd suggest looking at the actual source code of the opcodes (in
cpuops.c) to know exactly how they work. There are some subtle points
that can give you puzzling behavior - see especially the comment
before the 'call' opcode.
Several genomes of various sizes are included in the 'genomes'
directory. You can craft your own genomes, as well, if you're so
inclined, and see how they evolve. 'Porting' organisms from Tierra
isn't all that complicated. I might even take the time to implement
Tierra's original instruction set if I think anyone on Earth would
care. :-> It's not that hard to do yourself, after all. Or make up your
own opcode set!

D. Minev does absolutely no cataloging of genomes and all that kind of
stuff is left up to the user. You have to tell it when to write out
genomes to disk and then it's up to you to sort through them. The
format of the filenames is ###-###-###.gen, where the first field is
the genome size, the second is the total number in the soup at the time
of output, and the third is the first cpu number minev found that
genome at. (The third field is to make sure the filenames are unique -
if there were, e.g., two different genomes of size 52 with 10 cells
each, they'd be 52-10-xx.gen and 52-10-yy.gen.) Note that if you run
for a while, write out the organisms, then run for a while and save the
organisms again, you could overwrite one of the old genome files. Be
careful. (I'd put things in different directories, but there's no
portable, ANSI C way to do that.)

E. With the soup as small as it is, crowding can be a problem. What
often happens is that when parasites appear, they outcompete the
hosts and drive them to extinction. Then the parasites have no one
to leech off of and they go extinct. By that point, there's nobody
left in the soup and either everything goes extinct or you get lots
of random hash in the soup that never does anything interesting. To
help avoid this, the distance an organism can seach for a template
is pretty small. You can raise this (see 'consts.h', in the 'src'
directory), but you do so at your peril.
```
  
  
  
  
  
## The Game Space Dirt  
  
*original README*  
  
Hi and Assalamu Alaikum  
  
Space Dirt is a small DOS based game .  
The objectives are simple  
1.Clean the space dirt  
2.Hit the dirt making UFO ( or what ever u call it ) from behind  
3.Take the help of the colored pills appearing at random  
  
Can be of a great help for beginners in cpp graphics.  
Use it , abuse it I don't mind !!!!  
  
Rafay  
rafaymansoor@yahoo.com  
  
  
  
## Star Trek Game in C  
  
```
IT IS STARDATE 3421 AND THE FEDERATION IS BEING INVADED
BY A BAND OF KLINGON 'PIRATES' WHOSE OBJECTIVE IS TO TEST
OUR DEFENSES.  IF EVEN ONE SURVIVES THE TRIAL PERIOD,
KLINGON HEADQUARTERS WILL LAUNCH AN ALL-OUT ATTACK.
AS CAPTAIN OF THE FEDERATION STARSHIP 'ENTERPRISE', YOUR
MISSION IS TO FIND AND DESTROY THE INVADERS BEFORE THE TIME
RUNS OUT.

THE KNOWN GALAXY IS DIVIDED INTO 64 QUADRANTS ARRANGED
LIKE A SQUARE CHECKERBOARD, 8 ON A SIDE.  EACH QUADRANT IS
LIKEWISE DIVIDED INTO 64 SECTORS ARRANGED AS AN 8 BY 8 SQUARE.
EACH SECTOR CAN CONTAIN A KLINGON (K), STAR (*), STARBASE (B),
THE ENTERPRISE HERSELF (E), OR EMPTY SPACE (.).  EACH SECTOR
IS ALSO NUMBERED; A STARBASE IN SECTOR 3-5 IS 3 ROWS DOWN
FROM THE TOP OF THE SHORT RANGE SCAN PRINT-OUT, AND 5 SECTORS
TO THE RIGHT.  DOCKING AT A STARBASE IS DONE BY OCCUPYING
AN ADJACENT SECTOR, AND REPROVISIONS YOUR STARSHIP WITH
ENERGY AND PHOTON TORPEDOES, AS WELL AS REPAIRING ALL DAMAGES.

YOUR STARSHIP WILL ACT ON THE FOLLOWING COMMANDS:
COMMAND 1 - WARP ENGINE CONTROL IS USED TO MOVE THE ENTERPRISE.
YOU WILL BE ASKED TO SET THE DISTANCE (MEASURED
IN WARPS), AND THE COURSE FOR THE MOVE.  EACH
MOVE THAT YOU MAKE WITH THE ENTERPRISE FROM
ONE SECTOR TO ANOTHER, OR FROM ONE QUADRANT
TO ANOTHER, COSTS YOU ONE STARDATE (ONE YEAR).
THEREFORE, A 30-YEAR GAME MEANS YOU HAVE
30 MOVES TO WIN IN.

COURSE - A NUMBER FROM 1 TO          4   3   2
8.999 INDICATING A DIR-                \ ' /
ECTION (STARTING WITH                5 - * - 1
A 1 TO THE RIGHT AND IN-               / ' \
CREASING COUNTERCLOCKWISE).          6   7   8
TO MOVE TO THE LEFT, USE A
COURSE OF 5.  (A COURSE OF 3.5 IS HALFWAY BETWEEN
3 AND 4; A COURSE OF 8.75 IS THREE-QUARTERS OF THE
WAY FROM 8 TO 1.)

WARP - ONE WARP MOVES YOU THE WIDTH OF A QUADRANT.
A WARP OF .5 WILL MOVE YOU HALFWAY THROUGH A
QUADRANT; MOVING DIAGONALLY ACROSS A QUADRANT
TO THE NEXT WILL REQUIRE 1.414 WARPS.  WARP 3
WILL MOVE YOU 3 QUADRANTS PROVIDING NOTHING
IN YOUR PRESENT QUADRANT BLOCKS YOUR EXIT.
ONCE YOU LEAVE THE QUADRANT THAT YOU WERE
IN, YOU WILL ENTER HYPERSPACE; COMING OUT
OF HYPERSPACE WILL PLACE YOU RANDOMLY IN
THE NEW QUADRANT.  KLINGONS IN A GIVEN QUADRANT
WILL FIRE AT YOU WHENEVER YOU LEAVE, ENTER,
OR MOVE WITHIN THE QUADRANT.  ENTERING A
COURSE OR WARP OF ZERO CAN BE USED TO RETURN
TO THE COMMAND MODE.

COMMAND 2 - A SHORT RANGE SENSOR SCAN WILL PRINT OUT THE
QUADRANT YOU PRESENTLY OCCUPY SHOWING THE
CONTENT OF EACH OF THE 64 SECTORS, AS WELL
AS OTHER PERTINENT INFORMATION.

COMMAND 3 - THE LONG RANGE SENSOR SCAN SUMMARIZES THE QUADRANT
YOU ARE IN, AND THE ADJOINING ONES.  EACH
QUADRANT IS REPRESENTED AS A 3-DIGIT NUMBER;
THE FIRST (HUNDREDS) DIGIT IS THE NUMBER OF
KLINGONS IN THAT QUADRANT WHILE THE MIDDLE
DIGIT IS THE NUMBER OF STARBASES, AND THE
UNITS DIGIT IS THE NUMBER OF STARS.  AN ENTRY
OF 305 MEANS 3 KLINGONS, NO STARBASES, AND
5 STARS.

COMMAND 4 - FIRE PHASERS; THE PORTION OF THE ENTERPRISE'S
ENERGY THAT YOU SPECIFY WILL BE DIVIDED EVENLY
AMONG THE KLINGONS IN THE QUADRANT AND FIRED
AT THEM.  SURVIVING KLINGONS WILL RETALIATE.
PHASER FIRE BYPASSES STARS AND STARBASES, BUT
IS ATTENUATED BY THE DISTANCE IT TRAVELS.
THE ARRIVING ENERGY DEPLETES THE SHIELD POWER
OF ITS TARGET.  ENERGY IS AUTOMATICALLY DIVERTED
TO THE SHIELDS AS NEEDED, BUT IF YOU RUN OUT
OF ENERGY YOU'LL GET FRIED.

COMMAND 5 - PHOTON TORPEDO CONTROL WILL LAUNCH A TORPEDO
ON A COURSE YOU SPECIFY WHICH WILL DESTROY
ANY OBJECT IN ITS PATH.  RANGE IS LIMITED TO
THE LOCAL QUADRANT.  EXPECT RETURN FIRE FROM
SURVIVING KLINGONS.

COMMAND 6 - THE GALACTIC RECORDS SECTION OF THE SHIP'S
COMPUTER RESPONDS TO THIS COMMAND BY PRINTING
OUT A GALACTIC MAP SHOWING THE RESULTS OF ALL
PREVIOUS SENSOR SCANS.
```
  
  
  
  
  
  
  
