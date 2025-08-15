---
title: Review Action
---
### General Information  
Author: 	Brian Moriarty  
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	ANALOG Computing #16  
---
# A New Language for the Atari!  
Atari users have a surprisingly wide selection of programming languages from which to choose. We've got three dialects of BASIC, four C compilers, eight or nine FORTHS, a pair of Pascals, PILOT, Logo, WSFN, a Lisp interpreter, numerous 6502 assemblers and a couple of hybrids like BASM and Mirth. Not bad for a "game machine," eh?  
  
Leave it to Optimized Systems Software to come up with yet another way to tell your Atari what to do. OSS has been the leading purveyor of alternative operating systems and languages for the Atari since before I can remember. __Action!__ is only the first of a whole new line of OSS products that's been causing quite a stir in the Atari underground. It's been touted as the first programming environment developed specifically for the 6502, and the fastest high-level language available for the Atari. These are pretty strong claims which, after playing with the system for several weeks, appear to be totally justified. As you are about to read.  
  
## New! Improved!  
In syntax and overall structure, __Action!__ bears a strong resemblance to Pascal, C and other members of the Algol family. It's a procedure-oriented language featuring global and local variables, user-definable functions, parameter passing and powerful structures like DO loops, FOR-TO, WHILE, UNTIL and IF-THEN-ELSE. Three basic data types are recognized: 8-bit BYTEs (or CHARacters), 16-bit signed INTegers and 16-bit unsigned CARDinals. The system also supports a variety of extended data types including pointers, subscripted arrays, strings and records.  
```
AND    FI      OR      UNTIL =   (
ARRAY  FOR     POINTER WHILE <>  )
BYTE   FUNC    PROC    XOR   #   .
CARD   IF      RETURN  =     >   [
CHAR   INCLUDE RSH     -     >=  ]
DEFINE INT     SET     *     <   "
DO     LSH     STEP    /     <=  '
ELSE   MOD     THEN    &     $   ;
ELSEIF MODULE  TO      %     <
EXIT   OD      TYPE    !     @

Listing 1.
Reserved keywords
```
__Listing 1__ includes all of the keywords reserved for use by the __Action!__ system. These are used to declare variables, define new procedures and/or functions and to control the operation of the compiler. BASIC veterans will note with alarm the total lack of keywords that do interesting things in and of themselves, like SETCOLOR or DRAWTO. They're missing for a very good reason. Unlike BASIC, __Action!__ does not limit your programming to a limited number of safe little commands. It invites you (indeed, ''forces'' you) to invent the commands you need to solve problems yourself. The keywords in __Listing 1__ are the tools the system gives you to, in effect, write your own language. If this prospect doesn't excite you, maybe BASIC has been holding your hand for too long.  
```
Print   PrintE   PrintD  PrintDE  PrintB    PrintBE 
PrintBD PrintBDE PrintC  PrintCE  PrintCD   PrintCDE 
PrintI  PrintIE  PrintID PrintIDE Put       PutE 
PutD    PutDE    InputS  InputSD  InputMD   Open 
Close   XIO      Note    Point    Graphics  SetColor 
Plot    DrawTo   Fill    Position Sound     SndRst 
SCopy   SCopyS   SAssign StrB     StrC      StrI 
Break   Error    Zero    SetBlock MoveBlock 

Listing 2.
Library procedures.}}}
Don't get the impression that __Action!__ leaves you completely on your own, though. The cartridge includes a library of useful I/O, graphics and system-level routines that you can use to start building more elaborate programs. __Listings 2__ and __3__ will give you an idea of what's available. The resemblance of many __Action!__ library words to Atari BASIC commands is intentional; the kindly folks at OSS want to make your transition from BASIC to __Action!__ as painless as possible. This concern for familiarity unfortunately extends to the __Action!__ graphics library, which offers exactly the same (limited) access to the hardware as Atari BASIC. Other weak points of the cartridge library include inadequate control over memory allocation and a mysterious lack of support for the Atari's built-in floating point math package.
{{{
InputB   InputC InputI InputBD InpuCD InputID 
GetD     Locate Paddle PTrig   Stick  STrig 
SCompare ValB   ValC   ValI    Rand   Peek 
PeekC    Poke   PokeC 

Listing 3.
Library functions.}}}
Most of the elements in an __Action!__ program are delimited by space characters - as many as you like! You don't have to keep track of line numbers, semicolons, brackets or any other nuisances that can make you feet more like a bookkeeper than a programmer. Just follow a few simple rules regarding commas and parentheses, and you're all set. __Action!__'s modern design encourages a wide-open style of program composition, with plenty of freedom regarding the use of blank lines, upper and lower-case characters, indentation, comments and other flourishes that improve readability and make coding more fun.

!!A four-part system.

Internally, the __Action!__ system consists of four distinct modules. There's an ''editor'' for creating and modifying program source text, a ''compiler'' which translates source text into executable machine code, a ''run-time library'' that supports the compiled code (described above), and a ''monitor'' which acts as a switchboard between the other three modules and (if you're using a disk drive) DOS.

A very important distinction between __Action!__ and every other compiled language for the Atari is that these modules do not have to be loaded in separately from disk. All four are tucked away inside the SuperCartridge, safe from accidental erasure and ready whenever you need them. Further, the system is arranged so that your source text and compiled code can reside in memory at the same time. This self-contained design combines the performance of a compiled language with a degree of interactiveness usually associated with an interpreter. A stroll through the modules will show you what I mean.

!!The editor.

Somebody at OSS once told me that the text editor in the __Action!__ cartridge was originally going to be marketed by itself as a word processor. It isn't hard to believe. There are so many features and options in the __Action!__ editor that I can only touch on the most interesting here.

__Action!__'s editor uses your TV as a virtual window into a text area that can extend well beyond the edges of the screen. Unlike the standard Atari screen editor, you can type up to 240 characters on a single line with no cursor wraparound. How? When your cursor reaches the right edge of the screen, the line you're working on (and ''only'' that line) starts to coarse-scroll to the left. You can keep right on typing until a buzzer informs you that you've reached the rightmost position in that line - the right "edge" of the text window. Move your cursor back towards the left, and the line scrolls to the right until you hit the left edge of the window. This design neatly eliminates the usual confusion between "logical" and "physical" lines of text.

Hitting CTRL/SHIFT/">" or "<" instantly moves you to the rightmost or leftmost character in the current line, respectively. You can also change the maximum width of the text window to any convenient value, such as how many characters will fit on your printer.

The __Action!__ editor allows you to create a second text window, co-resident in memory but otherwise completely independent from the main window. The 2-window editing mode is represented visually by a split screen, with the bottom half of the image devoted to the auxiliary window. You can jump back and forth between the two windows and transfer blocks of text if desired; the editor remembers where you were working in each window and automatically returns you to that point when you return. Additionally, you can save, load or delete text in one window without disturbing the contents of the other. That means, for example, that you could load a library of routines into the auxiliary window, review them and copy the ones you need into your main program, which has been in full view the whole time! Sure beats LISTing and ENTERing lines of BASIC, doesn't it?

Other noteworthy capabilities of the __Action!__ editor include global search and replace, instant access to the beginning or end of a file and the ability to delete, move and copy, selected blocks of text. The block move and copy functions are implemented so nicely that I have to tell you about them. When you hit the SHIFT/DELETE keys, the line you're working on disappears, just as with the Atari screen editor. But the line isn't gone forever. It's being held in a buffer, waiting to be moved or copied to anywhere else in your text window(s). Simply move the cursor to a likely spot and hit CTRL/SHIFT/"P" (for paste) to dump the contents of the buffer. Several adjacent lines of text can be sent to the buffer by repeatedly "deleting" them with SHIFT/DELETE. __Action!__'s method of picking up and dropping blocks of text feels very natural if you're used to the Atari screen editor, and it also eliminates the annoyance of losing a line of work by accidentally hitting SHIFT/DELETE. Incidentally, you can automatically undo any changes you have made to a line of text by hitting CTRL/SHIFT/"U" before leaving the fine. Luxurious.

Before you toss out your __AtariWriter__ cartridge, let me point out a couple of small but irritating problems in the __Action!__ editor. There's a feature called tagging which allows you to mark any location in your text by assigning it a unique one-character identifier. You can later return to that point in the text at any time by calling its ID code. It's a good idea that, unfortunately, isn't pulled off particularly well. If you set a tag in a line and change even a single character in that line, the tag disappears. This restriction (which is documented) considerably reduces the usefulness of the tagging option, to say the least.

My other gripe is with the way the cursor appears to flash and jump around the screen when it is being moved up or down, as if it isn't sure where to go next. The solid command line on the bottom of the screen also seems to jerk occasionally as you cursor around. Minor cosmetic points, perhaps, but an unstable cursor seems out of place in this otherwise superb little text editor.

!!The monitor.

After you've put the finishing touches on an __Action!__ program and saved it out to disk, what next? Press the CTRL/SHIFT/"M" keys simultaneously and you'll find yourself staring at a barren white bar across the top of your screen. This is __Action!__'s monitor, the central interface between the editor, compiler, machine and user.

Monitor functions are invoked by typing a one-character code letter. You can select various compilation options, save and load compiled programs, examine the values of variables and memory locations and trace the execution of your programs. You can even use the X (execute) directive to interactively test almost any procedure or function. This capability is very unusual (and useful) in a compiled programming language.

!!The compiler.

Unlike Atari BASIC, which compiles each line of program text as it is typed, __Action!__ requires that your program be explicitly translated into machine code before it can be executed. This isn't nearly as formidable as it sounds. All you have to do is type the letter C from within the __Action!__ monitor.

The compiler accepts source text from either the editor (default), or from a text file saved onto cassette or disk. If you've been using both text windows, __Action!__ will compile only the text in the window you last edited. Compilation is almost unbelievably rapid, especially when the source is the editor. I've never seen __Action!__ take more than a few seconds to compile even a fairly large program that was in the editor. Small programs are compiled before you take your finger off the RETURN key. You can optionally instruct the compiler to list each line of source text to the screen or a printer as it is being compiled. This slows the compilation considerably, however.

A compile error causes the system to display the line where the error occurred, along with an error message number. Surprisingly for an OSS product, there are no English error messages. If you re-enter the editor after a compile error, you'll find the cursor obligingly positioned over the questionable spot in your text.

Successfully compiled code is executed by typing the letter R (run) from within the __Action!__ monitor. If you're accustomed to the leisurely pace of Atari BASIC, get ready for a shock. OSS isn't kidding when they say __Action!__ is fast.

!! How fast is fast?

Execution speed is very important to Atari programmers. Why? Because much of the software written for the Atari relies heavily on graphics, where a few extra machine cycles in the wrong place can make the difference. between a spectacular special effect and an interesting but unmarketable demo. High speed isn't likely to hurt a non-gaphics program, either. This is in accordance with Moriarty's Maxim: ''It is much easier to slow down a computer program than it is to speed it up.''

A number of attempts have been made to devise a universal method for comparing the speed performance of computer languages and hardware. In September of 1981, ''Byte'' magazine published an iterative number-crunching algorithm called the __Sieve of Eratosthenes__, which calculates all of the 1.899 prime numbers between 3 and 16.384.[1] The __Sieve__ has since become the informal industry standard for clocking the speed of microcomputer languages.

__Listing 4__ is an implementation of the __Sieve__ in Atari BASIC. It requires 19.490 jiffies or approximately 5½ minutes to execute on an unmodified 48K Atari 800 system. I recognize that __Listing 4__ is not the most efficient way to write the __Sieve__ in Atari BASIC, but it is the clearest and most portable way, and that's what counts in this application. You might like to try rewriting the __Sieve__ for better speed performance. I've achieved improvements of better than 30% with tricky recoding.

{{{Listing 4.

10 REM * ERATOSTHENES SIEVE
11 DIM FLAG$(8191)
12 POKE 559,0
13 POKE 19,0:POKE 20,0
14 COUNT=0
15 FOR I=1 TO 8191
16 FLAG$(I,I)="T"
17 NEXT I
18 FOR I=0 TO 8190
19 IF FLAG$(I+1,I+1)="F" THEN 27
20 PRIME=I+I+3
21 K=I+PRIME
22 if K>8190 THEN 26
23 FLAG$(K+1, K+1)="F"
24 K=K+PRIME
25 GOTO 22
26 COUNT=COUNT+1
27 NEXT I
28 TIME=PEEK(20)+256*PEEK(19)
29 POKE 559,34
30 ? COUNT;" PRIMES IN"
31 ? TIME;" JIFFIES"
```
Although I love standards, I don't like the __Sieve__. It's not easy for beginners to understand, it takes too long (in BASIC, anyway), and it doesn't test the Atari under real-world conditions, with lots of 6502 processor time being "stolen" by Antic for video DMA. I wanted a benchmark that anybody could appreciate, operating under the kind of DMA conditions an Atari program is likely to find itself up against.  
  
Back in Issue 11, I devised a little program that fills a GRAPHICS 24 screen with color, one byte (eight pixels) at a time. It was used to compare a couple of BASIC compilers at the time, but it's equally valid in any run-time environment. My definitive BASIC implementation of this test appears in __Listing 5__. __Screen Fill__, as the program shall henceforth be known, executes in 4.025 jiffies or about 67 seconds on a 48K 800. (Again, improvements are possible, but for the sake of clarity let's stick to __Listing 5__.) I'll be using __Screen-Fill__ in conjunction with the __Sieve__ to judge the performance of every new language I review from now on. So let it be written; so let it be done.  
```
10 REM * SCREEN-FILL BENCHMARK
11 GRAPHICS 24
12 POKE 19,0:POKE 20,0
13 SCREEN=PEEK(88)+256*PEEK(89)
14 FOR I=0 TO 31
15 FOR J=0 TO 239
16 POKE SCREEN+J,255
17 NEXT J
18 SCREEN=SCREEN+240
19 NEXT I
20 TIME=PEEK(20)+256*PEEK(19)
21 GRAPHICS 0
22 PRINT TIME;" JIFFIES"
```
OSS includes a implementation of the __Sieve__ benchmark in their Action! documentation. I rewrote the code slightly to make it match my BASIC implementation more closely; the modified program is shown in __Listing 6__. It executes in 89 jiffies or just under a second and a half. I'll save you a calculation by pointing out that the __Sieve__ runs about 219 times faster in __Action!__ than it does in Atari BASIC.  
```
BYTE RTCLOK=20, ; addr of sys timer
     SDMCTL=559 ; DMA control

BYTE ARRAY FLAGS(8190)

CARD COUNT,I,K,PRIME,TIME

PROC SIEVE()

  SDMCTL=0 ; shut off Antic
  RTCLOK=0 ; only one timer needed

  COUNT=0         ; init count
  FOR I=0 TO 8190 ; and flags
    DO
    FLAGS(I)='T
  OD

  FOR I=0 TO 8190
    DO
    IF FLAGS(I)='T THEN
      PRIME=I+I+3
      K=I+PRIME
      WHILE K<=8190
        DO
        FLAGS(K)='F
        K==+PRIME
      OD
      COUNT==+1
    FI
  OD

  TIME=RTCLOK ; get timer reading
  SDMCTL=34   ; restore screen

  PRINTF("%E %U PRIMES IN",COUNT)
  PRINTF("%E %U JIFFIES",TIME)

RETURN
```
Unconvinced? __Listing 7__ is an __Action!__ implementation of __Screen-Fill__. This demanding little gem executes in 32 jiffies (slightly more than half a second), or 126 times faster than its BASIC counterpart under maximum DMA handicap. And if you cheat by replacing the nested FOR-TO loops with an _Action!_, SETBLOCK procedure in the form:  
```
you'll obtain an execution time of just five jiffies. This is essentially the same amount of time it takes the equivalent machine-language code to do the same job. No other high-level Atari language that I am aware of can match this kind of speed performance.
{{{Listing 7.

BYTE RTCLOK=20,  ; addr of sys timer
     SAVMSCL=88, ; lsb of screen addr
     SAVMSCH=89, ; msb

     I,J,TIME    ; declare variables

CARD SCREEN

PROC BENCH()

  GRAPHICS(24)
  RTCLOCK=0

  SCREEN=SAVMSCL+256*SAVMSCH

  FOR I=0 TO 31
    DO
    FOR J=0 TO 239
      DO
      POKE(SCREEN+J,255)
    OD
    SCREEN==+240
  OD

  TIME=RTCLOK

  GRAPHICS(0)
  PRINTF("%E %U JIFFIES",TIME)

RETURN
```
  
## Pulling the wings off a butterfly.  
  
Once I got a taste of __Action!__'s dizzying speed, I had to find out what was going on inside that demonic little cartridge. So I used the W (write object code) option of the __Action!__ monitor to send a copy of the compiled __Screen-Fill__ benchmark to a disk file. Then I read it back into Ralph Jones' __Ultra Disassembler__ (published by Adventure International), massaged the labels and commented the code to make it correspond to the __Action!__ source text, line by line. The result appears in __Listing 8__.  
  
Assembly programmers will appreciate the extraordinary efficiency of the __Action!__ compiler. The code in __Listing 8__ is totally non-recursive. It uses no special stacks or indirect pointers to control the flow of execution, just pure in-line machine code with an occasional JSR into a cartridge library routine. This is "native mode" compilation at its best: simple, clean, and very, very swift. The output of a typical C or Pascal compiler looks like spaghetti by comparison.  
  
Because compiled __Action!__ programs refer to subroutines that reside inside the __Action!__ cartridge, you can't run a program without the cartridge in place. This may come as a disappointment to users who want to give copies of their latest __Action!__ game to friends who don't have __Action!__ OSS plans to remedy this situation by offering a Personal Run-Time Package to licensed __Action!__ users for around $30. It's a utility that will let you turn any __Action!__ program into a self-standing entity that will run with no help at all from the __Action!__ cartridge, thank you. A commercial run-time package will also be offered for a one-time licensing fee of approximately $300. Both may be available by the time you read this; contact OSS directly for more information.  
  
Another $30 will get you OSS's Programmer's Aid Disk (PAD), a collection of demonstration programs and library routines that wouldn't fit into the already crowded __Action!__ cartridge. The libraries include badly-needed support for player/missile graphics, memory management and floating point math, precisely the weaknesses I noted above. The demo programs are very instructive and help to clarify some of the obscure features of the language. You even get a full-blown game program, written in __Action!__ by our very own Joel Gluck.  
  
The PAD squarely addresses many of the shortcomings of the __Action!__ cartridge and documentation, and is an absolute must for all serious owners of the Action! system. In fact, this material ought to be included with every new system sold, even if it means bumping up the price a bit.  
  
## You can bank on it.  
  
The 16K __Action!__ "SuperCartridge" is a technically interesting device in and of itself. It employs a hardware technique called bank-selecting to make itself "look" like an 8K cartridge. This gives you access to the 8K of RAM between $8000-$9FFF that is de-selected and thus rendered useless by a conventional 16K cartridge, such as __AtariWriter__.  
  
The bottom half of the SuperCartridge ($A000- $AFFF) is divided into three independently addressable 4K banks of ROM, which are automatically switched in and out depending on what part of the system is in use. If your Atari has 48K or more memory, it's even possible to address the 4K bank of RAM that resides "under" this half of the cartridge. OSS's new __DOS XL__ operating system takes advantage of this capacity in a most ingenious manner. Look for a report in a future issue.  
  
The bank-select cartridge is a nearly ideal home for Atari software. It gives the cartridge designer a full 16K to work with, enough room for plenty of bells and whistles. It gives the user an instant-loading, highly reliable environment with up to 40K of workspace. And because three of the memory banks occupy the same 4K address range, a bank-select cartridge is very difficult to pirate. Let's hope that more manufacturers start taking advantage of bank-selecting to enhance the value and security of their products.  
  
## Advice and admiration.  
  
I'm sorry to report that the ''Action! Reference Manual'' doesn't do the language justice. In a commendable attempt to satisfy beginners and experts alike, the ''Manual'' suffers from lack of confidence, uncertain organization and a shortage of good, hard technical data. Thank goodness for the numerous sample programs, which communicate a lot more about the system than the text surrounding them.  
  
Having once written the manual for a new (and mercifully obscure) programming language, I can appreciate the difficulties involved in deciding how much needs to be said, to whom, and in what order. Nevertheless, a new language can only be as good as its documentation. Until somebody sits down, rolls up his or her sleeves and writes an authoritative book about __Action!__, it will have a hard time attaining the wide acceptance it so obviously deserves. I conclude this diatribe by acknowledging that the latest edition of the ''Reference Manual'' (in the small yellow notebook) shows a marked improvement over the first release.  
  
The __Action!__ cartridge itself has gone through a couple of changes since its first appearance in August 1983. You can tell which version you have by using the "?" (display memory) command in the monitor to examine cartridge address $B000. If this byte equals $31 hex, you have the original Version 3.1. A value of $33 indicates Version 3.3, in which a number of minor 3.1 bugs have been corrected. The final version is 3.6 ($36 at $B000), which should be ready soon after you read this. OSS has always been very good about maintaining their products, so you shouldn't have any trouble getting an upgrade if you need one. Consult OSS for prices and availability.  
  
I hope my kvetching about the documentation doesn't scare you away. If sensible, structured code and edge-of-the-art speed are what you crave in a high-level language, __Action!__ is exactly what you need. OSS's hideous orange cartridge joins the ranks of __valFORTH__, __Omnimon!__, __ABC__ and __MAC/65__ as one of the most valuable development tools ever published for the Atari. Congratulations and thanks to Clint Parker and OSS for bringing us such an advanced product. You can expect to see plenty of support for this exciting new language in future issues of __ANALOG__.  
```
0100 ;           DISASSEMBLY OF COMPILED
0110 ;           ACTION! SCREEN-FILL
0120 ;           BENCHMARK (LISTING 7)
0130 ;           -----------------------
0140 ;
0150 ;          DEFINE ADDRESS CONSTANTS
0160 ;          ------------------------
0170 RTCLOK = 20
0180 SAVMSCL = 88
0190 SAVMSCH = 89
0200 ;
0210 ;         GLOBAL VARIABLE STORAGE
0220 ;         -----------------------
0230     *=  ORIGIN
0240 I   *=  *+1     ; reserve 1 byte for
0250 J   *=  *+1     ; each BYTE variable,
0260 TIME *= *+1
0270 SCREEN *= *+2   ; 2 bytes for CARDs
0280 ;
0290 ;         PROC BENCH()
0300 ;         ------------
0310     JMP START
0320 ;
0330 ; If our procedure used local variables,
0340 ; they would have been stored here.
0350 ; That's why the above JMP is included.
0360 ;
0370 ;         GRAPHICS(24)
0380 ;         ------------
0390 START
0400     LDA #24
0410     JSR GRAPHICS
0420 ;
0430 ;         RTCLOK=0
0440 ;         --------
0450     LDY #0
0460     STY RTCLOK
0470 ;
0480 ;         SCREEN=SAVMSCL+256*SAVMSCH
0490 ;         --------------------------
0500     LDA #0
0510     STA TEMP1+1
0520     LDA SAVMSCH ; move SAVMSCH into
0530     STA TEMP1   ; TEMP1
0540     LDA # >256  ; msb of multiplier
0550     TAX 
0560     LDA # <256  ; lsb
0570     JSR MULTIPLY
0580     STA TEMP4
0590     TXA         ; save (256*SAVMSCH)
0600     STA TEMP4+1 ; into TEMP4
0610 ;
0620     CLC 
0630     LDA SAVMSCL ; add SAVMSCL to
0640     ADC TEMP4   ; (256*SAVMSCH) and
0650     STA SCREEN  ; store in SCREEN
0660     LDA #0
0670     ADC TEMP4+1
0680     STA SCREEN+1
0690 ;
0700 ;          FOR I=0 TO 31 DO
0710 ;          ----------------
0720     LDY #0
0730     STY I       ; init I-loop
0740 ILOOP
0750     LDA #31
0760     CMP I       ; reached limit yet?
0770     BCS JINIT   ; no - do another J-loop
0780     JMP GETIME  ; else get timing
0790 ;
0800 ;          FOR J=0 TO 239 DO
0810 ;          -----------------
0820 JINIT
0830     LDY #0
0840     STY J       ; init J-loop
0850 JLOOP
0860     LDA #239
0870     CMP J       ; reached limit yet?
0880     BCS DOPOKE  ; no - poke another byte
0890     JMP ADD240  ; else update screen
0900 ;
0910 ;         POKE(SCREEN+J,255)
0920 ;         ------------------
0930 DOPOKE
0940     CLC 
0950     LDA SCREEN  ; add SCREEN to
0960     ADC J       ; J, and
0970     STA TEMP2   ; save in TEMP2
0980     LDA SCREEN+1
0990     ADC #0
1000     STA TEMP2+1
1010 ;
1020     LDY #255
1030     LDX TEMP2+1
1040     LDA TEMP2   ; poke (SCREEN+J) with
1050     JSR POKE    ; a 255
1060 ;
1070 ;        OD (for J loop)
1080 ;        ---------------
1090     INC J
1100     JMP JLOOP
1110 ;
1120 ;        SCREEN==+240
1130 ;        ------------
1140 ADD240
1150     CLC 
1160     LDA SCREEN  ; add SCREEN and
1170     ADC #240    ; 240; store result
1180     STA SCREEN  ; in SCREEN
1190     LDA SCREEN+1
1200     ADC #0
1210     STA SCREEN+1
1220 ;
1230 ;        OD (for I loop)
1240 ;        ---------------
1250     INC I
1260     JMP ILOOP
1270 ;
1280 ;        TIME=RTCLOK
1290 ;        -----------
1300 GETIME
1310     LDA RTCLOK
1320     STA TIME
1330 ;
1340 ;        GRAPHICS(0)
1350 ;        -----------
1360     LDA #0
1370     JSR GRAPHICS
1380 ;
1390 ;        PRINTF("%E %U JIFFIES",TIME)
1400 ;        ----------------------------
1410     JMP OVER      ; skip over in-line string
1420 STRING
1430     .BYTE 13      ; length of string
1440     .BYTE "%E %U JIFFIES"
1450 OVER
1460     LDA #0        ; msb of TIME
1470     STA TEMP3     ; into TEMP3
1480     LDY TIME      ; lsb into Y
1490     LDX # >STRING ; msb of string addr
1500     LDA # <STRING ; lsb
1510     JSR PRINTF
1520 ;
1530 ;        RETURN
1540 ;        ------
1550     RTS           ; from procedure
1560 ;
1570     RTS           ; back to Action! monitor
```
[1](../1/index.md)*Jim Gilbreath, "A High-Level Language Benchmark." ''Byte'', VI, 9 (September 1981), pp. 180-198.  
