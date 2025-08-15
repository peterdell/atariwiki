---
title: C Style Strings
---
# C Style Strings  
  
General Information  
  
Author: 	John DiMarco   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	3. September 1987   
%%tabbedSection  
%%tab-english  
When I first purchased an Action!  
cartridge, I was favourably impressed  
with the clarity, power, and - most  
especially - with the speed of the  
language and the compiler. But I  
have come across what I consider to  
be two major shortcomings with the  
language which have made it less than  
wonderful. Firstly, nested function  
calls are prohibited. This makes  
it necessary to store function  
results in temporary variables for  
use in subsequent function calls.  
This makes source code unnecessarily  
lengthy and can detract from its  
clarity. Secondly, because the first  
byte of an Action! string is the  
length of that string, strings can  
be no longer than 255 characters.  
This detracts from the usefulness of  
action strings for storage of any  
large amounts of data. I much prefer  
strings as they are managed in C,  
where a string is any number of  
characters terminated by a null  
(ASCII 0) byte. In C, strings can  
be arbitrarily long, and thus can  
be used for word processor text  
buffers, for example.  
  
There was really nothing I could  
do about Action!'s inability to  
support nested function calls, but  
C-style strings were really quite  
easy to implement in Action!, and  
so I wrote and tested this package  
in a couple of hours. All I did was  
rewrite all the standard Action!  
string functions (Scopy, SCompare,  
SAssign, etc.) and the standard  
input/output routines (<nop>PrintE,  
<nop>InputS, even Open and XIO) to support  
C-style strings rather than Action!  
strings. I also included a couple  
of conversion routines to convert  
Action! strings to C strings and vice  
versa. With this package, it is  
possible to support both Action! and  
C style strings in the same program,  
and convert between them at will.  
  
To include these routines in your  
program, simply add an 'INCLUDE  
"CSTRINGS.ACT"' to the beginning  
of your program.  
  
The routines are as follows:  
  
### PROC AtoC(BYTE ARRAY A,B)  
- This routine assumes that  
A is an Action! string and B is  
a BYTE ARRAY which is at least as  
big as A. It will convert the Action!  
string A to the same string in C  
style format, which it will store in  
B. A should not contain a null.  
(ATASCII 0 or ' ')  
  
  
### PROC CtoA(BYTE ARRAY A,B)  
- This routine assumes A is a  
C style string, and converts it to  
an Action! string which it stores in  
B. The C style string should not be  
longer than 255 characters, otherwise  
only the first 255 characters will  
be converted.  
  
### CARD FUNC AC(BYTE ARRAY A)  
- This routine converts the  
string A from an Action! string to a  
C style string. A should not contain  
a null.  
  
### CARD FUNC CA(BYTE ARRAY A)  
- This routine converts the  
string A from a C style string to an  
Action! string. A should not be  
longer than 255 characters.  
  
### CARD FUNC CSLength(BYTE ARRAY A)  
- Returns the length of the  
C style string A. The NULL byte is  
not included in this figure.  
  
### PROC CPrint, CPrintE, CPrintDE, CPrintD  
- Print out a C style string.  
Any C style string of arbitrary  
length may be printed. Syntax is  
exactly the same as in the Action!  
manual.  
  
### PROC CInputS, CInputSD, CInputMD  
- Input a C style string.  
Only strings of length less than or  
equal to 255 characters may be input.  
Syntax is as in Action! manual.  
  
### PROC COpen, CXIO  
- Open a channel or perform  
an XIO function where the filespec  
is a C style string. Only filespecs  
of length less than or equal to  
255 characters are permitted (but  
why you'd need more, I don't know!)  
Syntax as in Action! manual.  
  
### PROC CSCompare, CSCopy, CSCopyS, CSAssign  
- Compare or copy C style  
strings. Numerical arguments to  
these functions are CARDs rather  
than BYTEs, since C style strings are  
not limited to a length of 255  
characters. Syntax as in Action!  
manual.  
  
### PROC CStrB, CStrC, CStrI  
- Convert a BYTE, CARD, or INT  
to a C style string. Syntax as in Action! manual.  
  
### BYTE/CARD/INT FUNC CValB, CValC, CValI  
- Convert a C style string to  
a BYTE, CARD, or INT. Syntax as in Action! manual.  
  
  
## MISCELLANOUS NOTES: You may easily change the NULL  
byte to some value other than ATASCII  
0 by changing the NULL variable at  
the beginning of the CSTRINGS.ACT  
file. Note, however, that the  
CSCompare routine will not work  
correctly if you do so.  
  
The routines  
use BYTE ARRAY C_TMP(255) as a global  
temporary buffer, and thus no global  
variable of the name C_TMP is  
permitted.  
  
I hope these routines help you in  
making better use of the Action!  
programming language.  
  
Thurs, Sept. 3, 1987.  
  
-- John <nop>DiMarco  
  
UUCP: jdd@csri.toronto.edu  
/%  
%%tab-german  
Programm: CSTRING.ACT   
Autor: John DiMarco   
  
Nachdem ich das erstemal ein ACTION! Modul bekommen hatte, war ich beeindruckt von der Klarheit, Mächtigkeit und - sehr wichtig - von der Geschwindigkeit der Sprache und des Compilers. Aber ich habe zwei Mängel entdeckt, die den Glanz der Sprache ein wenig trüben:  
  
- Erstens: Geschachtelte Funktionsaufrufe sind verboten. Dies macht es notwendig, Funktionsparameter in temporären Variablen zu speichern, um sie in weiteren Funktionsaufrufen zu verwenden. Dies bläht den Sourcecode unnötig auf und macht ihn unübersichtlich.  
  
- Zweitens: Weil im ersten Byte der ACTION!-Strings die Länge des Strings gespeichert ist, können Zeichenketten nicht größer als 255 Zeichen lang sein. Daher kann man keine großen Datenmengen in ACTION!-Strings speichern. Vorzuziehen sind da Zeichenketten, wie sie in der Sprache C vorhanden sind, wo eine Zeichenkette beliebig lang sein kann und mit einem Null (ASCII 0) Byte abschließt.  
  
Es gibt nichts, was ich an der Tatsache ändern kann, um verschachtelte Aufrufe in ACTION! zu realisieren, aber 'C'-Strings sind sehr einfach in ACTION! zu programmieren und so habe ich diese Routinensammlung geschrieben und ausgetestet. Ich habe die Standard String-Routinen (SCopy, SCompare, SAssign, etc.) und die Eingabe/Ausgabe Routinen (PrintE, InputS, auch Open und XIO) umgeschrieben, um 'C'-Strings statt ACTION!-Strings benutzen zu können. Desweiteren gibt es Konvertierungsroutinen, um ACTION!-Strings in 'C'-Strings umzuwandeln und umgekehrt. Das ermöglicht die Benutzung von ACTION!-Strings und 'C'-Strings in einem Programm und die Umwandlung zwischen beiden Arten.  
  
Um diese Routinen in eigene Programme einzubinden, einfach INCLUDE "CSTRINGS.ACT" am Anfang des Programms einfügen.  
  
Die Routinen:  
  
### PROC AtoC (BYTE ARRAY a, b)  
  
- diese Routine erwartet in a einen ACTION!-String und speichert den Inhalt in b als einen 'C'-String gleicher Größe. Der ACTION!-String sollte keine Nullbyte enthalten (ATASCII 0)  
  
### PROC CtoA (BYTE ARRAY a, b)  
  
- diese Routine konvertiert einen 'C'-String (a) in einen ACTION!-String (b). Der 'C'-String sollte nicht länger als 255 Zeichen sein, da sonst nur die ersten 255 Zeichen übernommen werden  
  
### CARD FUNC AC(BYTE ARRAY a)  
  
- diese Routine konvertiert String 'a' von einem ACTION! String in einen 'C'-String. 'a' kann Nullbytes enthalten. (Ergebnis = Pointer auf 'C'-String)  
  
### CARD FUNC CA (BYTE ARRAY A)  
  
- diese Routine konvertiert einen 'C'-String in einen ACTION!-String. Der 'C'-String darf länger sein als 255 Zeichen.  
  
### CARD FUNC CSLength (BYTE ARRAY a)  
  
- ermittelt die Länge eines 'C'-Strings abzüglich des NullBytes.  
  
### PROC CPrint, CPrintE, CPrintDE, CPrintD  
  
- Gibt einen 'C'-String aus.  
  
### PROC CInputS, CInputSD, CInputMD  
  
- Liest einen 'C'-String ein. Nur Zeichenketten bis 255 Zeichen können eingelesen werden.  
  
### PROC COpen, CXIO  
  
- Öffnet einen Kanal oder führt eine XIO-Funktion aus. Es werden Zeichenketten bis 255 Zeichen unterstüzt (Warum auch mehr?)  
  
### PROC CSCompare, CSCopy, CSCopyS, CSAssign  
  
- Vergleicht oder Kopiert 'C'-Strings.  Numerische Parameter sind in diesen Funktionen CARD Variablen, da die 'C'-Strings größer als 255 Zeichen sein können.  
  
### PROC CStrB, CStrC, CStrI  
  
- Konvertiert eine BYTE, CARD oder INT Variable in einen 'C'-String  
  
### BYTE/CARD/INT FUNC CValB, CValC, CValI  
  
- wandelt einen 'C'-String in eine numerische Variable um  
  
## Anmerkungen:  
  
Wenn die NULL Variable am Anfang der Routinensammlung in einen anderen Wert als ATASCII 0 geändert wird, so wird die CSCompare Routine keine korrekten Werte liefern.  
  
Die Routinen benutzen eine BYTE ARRAY-Variable namens C_TEMP(255) als globalen temporären Puffer, daher darf keine weitere Variable dieses Namens deklariert werden.  
  
Ich hoffe, diese Routinen werden dir helfen, besseren Gebrauch von der Programmiersprache ACTION! zu machen.  
  
3. September 1987 -- John DiMarco  
  
/%  
/%  
  
```
; C style strings - arbitrary 
; length ending with a null byte
;--------------------------------
; Written Sept 3rd, 1987
; by John DiMarco 
;--------------------------------
; Complete permission is given to 
; duplicate this work, so long as 
; this message is included in any
; duplicate.  

MODULE
BYTE NULL=0
BYTE ARRAY C_TMP(255)

PROC AtoC(BYTE ARRAY A,C)
  ; Convert from Action-style string
  ; to C style string
  ; Assume A,C are defined and 
  ; C is as long as A.
  BYTE i
  FOR i=1 TO A(0) DO
	 C(i-1)=A(i)
  OD		  
  C(A(0))=NULL
RETURN

CARD FUNC AC(BYTE ARRAY A)
  ; Convert an Action-style string
  ; to a C style string
  BYTE i,j
  j=A(0)
  FOR i=1 TO j DO
	 A(i-1)=A(i)
  OD		  
  A(j)=NULL
RETURN (A)
		
CARD FUNC CSLength(BYTE ARRAY C)
  CARD i
  i=0
  WHILE C(i)<>NULL DO
	 i==+1
  OD
RETURN (i) 

CARD FUNC CA(BYTE ARRAY C)
  ; Convert a C style string to an 
  ; Action style string
  BYTE i,j
  j = CSLength(C)
  FOR i=0 TO j-1 DO
	 C(j-i)=C((j-i)-1)
  OD
  C(0)=j
RETURN (C)

PROC CtoA(BYTE ARRAY C,A)
  ; Convert from C style strings to 
  ; Action style strings
  ; Assume C,A are defined and
  ; C is less than 255 bytes long.
  BYTE i
  FOR i=0 TO 255 DO
	 IF C(i)=NULL THEN
		EXIT
	 FI
	 A(i+1)=C(i)
  OD
  A(0)=i
RETURN

PROC CPrintD(BYTE Channel,BYTE ARRAY C)
  CARD i									  
  i=0
  WHILE C(i)<>NULL DO
	 PutD(Channel,C(i)) 
	 i==+1
  OD
RETURN

PROC CPrint(BYTE ARRAY C)
  CPrintD(0,C)
RETURN

PROC CPrintDE(BYTE Channel,BYTE ARRAY C)
  CPrintD(Channel,C)
  PutD(Channel,155) 
RETURN

PROC CPrintE(BYTE ARRAY C)
  CPrintDE(0,C)
RETURN
			  
PROC CInputSD(BYTE Channel,BYTE ARRAY C)
  InputSD(Channel,C_TMP)
  AtoC(C_TMP,C)
RETURN
						
PROC CInputS(BYTE ARRAY C)
  CInputSD(0,C)
RETURN

PROC CInputMD(BYTE Channel, BYTE ARRAY C, BYTE max)
  InputMD(Channel,C_TMP,max)
  AtoC(C_TMP,C)
RETURN

PROC COpen(BYTE channel, BYTE ARRAY filestring, BYTE mode, aux2)
  CtoA(filestring, C_TMP)
  Open(channel, C_TMP, mode, aux2)
RETURN

PROC CXIO(BYTE channel, mystery, cmd, aux1, aux2, BYTE ARRAY filestring)
  CtoA(filestring,C_TMP)
  XIO(channel,mystery,cmd,aux1,aux2,C_TMP)
RETURN

INT FUNC CSCompare(BYTE ARRAY C1,C2)
  INT r1,r2
  CARD i
  i=0
  WHILE C1(i)=C2(i) AND C1(i)<>NULL AND C2(i) <> NULL DO
	 i==+1
  OD		 
  r1=C1(i)
  r2=C2(i)
RETURN (r1-r2) 

PROC CSCopy(BYTE ARRAY DEST,SRC)
  ; Make sure DEST is big enough!!!
  CARD i	 
  BYTE X
  i=0
  DO
	 DEST(i)=SRC(i)
	 IF SRC(i)=NULL THEN
		EXIT
	 FI
	 i==+1
  OD			
RETURN

PROC CSCopyS(BYTE ARRAY DEST,SRC, CARD START,STOP)
  ; Make sure DEST is big enough!!!!
  ; Also make sure START and STOP are
  ; within SRC.
  CARD i		
  i=START
  WHILE SRC(i-1)<>NULL AND i<=STOP DO
	 DEST(i-START)=SRC(i-1)
	 i==+1
  OD
  DEST(i-START)=NULL
RETURN			

PROC CSAssign(BYTE ARRAY DEST,SRC,CARD START,STOP)
  ; Make sure DEST is big enough!!!!
  ; Also make sure START and STOP are
  ; within SRC.
  CARD i
  i=0
  WHILE SRC(i-1)<>NULL AND i<(STOP-START+1) DO
	 DEST(i+START-1)=SRC(i)
	 i==+1
  OD
RETURN

PROC CStrB(BYTE number, BYTE ARRAY C)
  StrB(number,C_TMP)
  AtoC(C_TMP,C)
RETURN

PROC CStrC(CARD number, BYTE ARRAY C)
  StrC(number,C_TMP)
  AtoC(C_TMP,C)
RETURN

PROC CStrI(INT number, BYTE ARRAY C)
  StrI(number,C_TMP)
  AtoC(C_TMP,C)
RETURN
				  
BYTE FUNC CValB(BYTE ARRAY C)
  CtoA(C,C_TMP)
RETURN (ValB(C_TMP))

CARD FUNC CValC(BYTE ARRAY C)
  CtoA(C,C_TMP)
RETURN (ValC(C_TMP))

INT FUNC CValI(BYTE ARRAY C)
  CtoA(C,C_TMP)
RETURN (ValI(C_TMP))
```
