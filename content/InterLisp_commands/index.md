---
title: InterLisp commands
---
# Commands collected and documented by UNIXcoffee928  
  
on [AtariAge](http://www.atariage.com/forums/index.php?showtopic=116093)  
  
```
===============================================================================
INTERLISP LANGUAGE  USAGE
===============================================================================
#                   (equivalent to LISP NUMBERP)
>                   (equivalent to LISP GREATERP)
'                   (cons 'a 'b) ---> produces (A . B) the syntactic abbreviation (quote x)
(                   OPEN PARENS
)                   CLOSE PARENS
*                   (* 8 4)
/                   (/ 8 4)
+                   (+ 8 4)  or (+ a (+ b (+ c)))
AND                 (AND T T) or (AND 1 1) for true
APPEND              ****************** probably adds to an existing file, if not adds to an existing list
APPLY
ASSOC
ATOM
BACKTRACE           (BAKTRACE) Used in error mode to trace
BREAK
CAR
CDR
CLOSE               ****************** BASIC I/O
COL                 ****************** BASIC COLOR - To set the color # for PLOT or DRAW
COND                ****************** Sets up a conditional statement, like if-then-else
CONS                (cons (quote a) (quote b)) ---> produces (A . B)
DEFINE
DEFINEQ             (DEFINEQ LS '(LAMBDA NIL (DIR)))   ---> creates the command 'ls' to be used as (LS), thus providing a disk directory for the default drive.
DIR                 (DIR) or (DIR . D1:)
DRAW                (DRAW 10 10)
EQ                  (EQ 3 3) --> TRUE  (EQ 3 3.0)  --> FALSE  NOTE: (EQ 3 3.0)  --> TRUE (does not distinguish floating point difference)
EVAL                To call a value set with SETQ (EVAL X)
EXP                 (EXP 3) --> 20.0855365 same as BASIC
GET
GO
GR                  (GR 23)
IN#
INT                 (INT -4.5) --> -5  Rounds to integer
LAMBDA
LAST
LENGTH
LIST
LOAD                ****************** to load a file. can't figure out syntax of command yet
LOG                 (LOG 100)
MACRO
MEM                 (MEM) reports 16022 with all RAM settings... not good.
MEMBER              ****************** probably member of a list
NEW                 ****************** not the same as BASIC
NIL                 FALSE
NLAMBDA
NOTE                ****************** BASIC I/O
NSUBR
OBLIST              ****************** guessing object list
OPEN                ****************** BASIC I/O
OR                  (OR F F) or (OR 0 0) for false
PACK                ****************** think its pack all of the atoms, check
PAGE
PEEK                (PEEK 755)
PLOT                (PLOT 7 7)
POINT               ****************** BASIC I/O (POINT 0 0) --->  146  (might be the error # fro undefined handler function)
POKE                (POKE 77 127)
PR#                 ****************** might be BASIC PRINT# command like ?#7
PRIN1
PRIN2
PRINT
PROG
PROGN               ****************** Seems to execute a command, as in  (PROGN (DIR))
QUOTE               (QUOTE "HELLO WORLD") ---> HELLO WORLD   same as '
READ
READA
READC
RESET               (RESET) clears whatever was set with SETQ
RETURN              ****************** seems to b used to return from a subroutine, maybe like gosub
RPLACA
RPLACD
SAVE                ****************** to save a file. can't figure out syntax of command yet
SET
SETCOL              (SETCOL 1 15 15)
SETQ                (SETQ X '10) sets X as 10, to call it in immediate mode type X on a line, to call it in a program: (EVAL X)
SOUND               (SOUND 0 0 0 0)
STICK               (STICK)
STRIG               (STRIG 0)
SUB                 (SUB 8 4)
SUBR                ****************** probably initiatiates a subroutine
T                   TRUE
TAB                 (TAB 10)
TERPRI              (TERPRI) TERminate PRInt line. To output a newline. The TERPRI function prints a new-line to the specified <destination>. This will terminate the current print line for <destination>. NIL is always returned as the result. The <destination> may be a file pointer or a stream. If there is no <destination>, *STANDARD-OUTPUT* is the default.
UNPACK              ****************** think its unpack all of the atoms, check
XIO                 ****************** BASIC I/O



===============================================================================
Edit Commands: NOTE: Editor must be loaded to use these commands.
===============================================================================
EDIT 
E 
EF 
H 
L 
S 
C 
X 
PASTE 
EQUAL 
GETCMD 
MAPCAR 
COMMANDS 
PSET 
SETP 
R 
A 
D 
B 
LI 
RE 
CONZ 
PRE 
I 
DEL 
G 
PP 
P 
PPRINT 
PPAUX 
MULTARGS 
PPARGS 
TABRET 
FORMATS 
LPAR 
BLANK 
RPAR 
LINE-WIDTH 
NCONC 
PU 
LOCK 
UNLOCK 
GETLST
 
===============================================================================
MACLISP add-on Commands: NOTE: MACLISP must be loaded to use these commands.
===============================================================================
FUNCALL 
DEFPROP 
PUTPROP 
NCONC 
GET 
MAPCAR 
EQUAL
DELETE 
SUBST
REVERSE
REMPROP
CONZ
GENSYM 
DEFUN 
MACFNS



===============================================================================
CLISP add-on Commands: NOTE: CLISP must be loaded to use these commands.
===============================================================================
CLISP 
TRANSLATE 
WEIGHT 
OPCODE
```
