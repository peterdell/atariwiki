---
title: VFHandbuchChapter5
---
# Input / Output in Volks-FORTH  
  
  
## Input / output commands in VolksFORTH  
  
All input and output words (__KEY__ __EXPECT__ __EMIT__ __TYPE__ etc.) are vectorized in the people-FORTH, ie when called, the code field address of the associated command is taken from a table and executed. It is included in the system table wine named DISPLAY, which provides for the output to the screen terminal.  
  
This method of vectorization offers significant benefits:  
  
- Nit-vectorization of the input can e.g. switch with one stroke of the keyboard on the input of a modem.  
- The output can vectorization with a new table, the total expenditure to another device (eg a printer) will be conducted without having to change the output commands themselves.  
- In a word (__DISPLAY__, __PRINT__) can all be changed spending habits. Is there such a (((print a list display))) will be issued a screen on a printer, and then falls back to the screen. So you need a new word, such PRINTERLIST to define.  
  
A new table is created with the word __OUTPUT: __. The definition can output with (((view:)) look). __OUTPUT: __ Expected to issue a list of words, with must, be completed.  
  
Beipsiel:  
```
Output:> PRINTER
   pemit pcr ptype pdel PPAG pat pat? ;
```
  
For a new table named __> PRINTER__ is created. With a later call to PRINTER__ __> is the address of this table in the Uservariable __OUTPUT__  
written. From now leads __EMIT__ from a __PEMIT__, a __PTYPE__ __TYPE__ etc.  
  
The order of words after __OUTPUT: __  
userEMIT userCR userType userdel Userpage userAT userAT?  
must necessarily be met. Accordingly, the input-vectorization is handled.  
  
### Input / output terminal on  
  
The state-FORTH has a number of constants which serve to improve readability:  
  
- [C / row ](../_characters-per-row/index.md)  
- [C / col ](../_characters-per-column/index.md)  
- [C / dis ](../_characters-per-display/index.md)  
- [C / l ](../_characters-per-line/index.md)  
- [L / s ](../_lines-per-screen/index.md)  
- [Bl](../Bl/index.md)  
- [# Esc ](../_number-escape/index.md)  
- [# Cr ](../_number-carriage-return/index.md)  
- [# Lf ](../_number-linefeed/index.md)  
- [# Bel ](../_number-bell/index.md)  
- [# Bs ](../_number-backspace/index.md)  
- [Standardized / o ](../_standard_input-output/index.md)  
- [Inputkol](../Inputkol/index.md)  
- [Outputkol](../Outputkol/index.md)  
- [Area](../Area/index.md)  
- [Areakol](../Areakol/index.md)  
- [] Terminal  
- [Window](../Window/index.md)  
- [Full](../Full/index.md)  
- [Curat? ](../_Cursor-at-question/index.md)  
- [Cur! ](../_Cursor-store/index.md)  
- [Setpage](../Setpage/index.md)  
- [@ Video ](../_video-fetch/index.md)  
- [Savevideo](../Savevideo/index.md)  
- [Restorevideo](../Restorevideo/index.md)  
- [Catt](../Catt/index.md)  
- [List](../List/index.md)  
- [(Page ](../_paren-page/index.md)  
- [Page](../Page/index.md)  
- [(Del ](../_paren-delete/index.md)  
- [Del](../Del/index.md)  
- [(Cr ](../_paren-carriage-return/index.md)  
- [Cr](../Cr/index.md)  
- [? Cr ](../_question-carriage-return/index.md)  
- [(At ](../_paren-us/index.md)  
- [(At? ](../_Paren-at-question/index.md)  
- [At](../At/index.md)  
- [At? ](../_At-question/index.md)  
- [Col](../Col/index.md)  
- [Row](../Row/index.md)  
- [] Curoff  
- [Curon](../Curon/index.md)  
- [Curshape](../Curshape/index.md)  
- [Printer](../Printer/index.md)  
- [Print](../Print/index.md)  
- [+ ](../_Print_plus-print/index.md)  
- [Ls! ](../_List-store/index.md)  
  
### Input / output of numbers  
  
The input of numbers is made in the interpretive mode via the keyboard, and basic input words are defined with __number__ __numbers__ and related words. For the issue of numbers again is the lack of typing of FORTH observed - for a specific data format (integer, unsigned, double) is appropriate in each case the operator to select.  
  
- [. ](../_Dot/index.md)  
- [U. ](../_unsigned-dot/index.md)  
- [D ](../_double-dot/index.md)  
- [. R ](../_dot-right-justified/index.md)  
- [U.r ](../_unsigned-dot-right-justified/index.md)  
- [D.r ](../_double-dot-right-justified/index.md)  
  
### Input / output via a port  
  
MS-DOS''''  
- [Pc @ ](../_port-char-fetch/index.md)  
- [PC! ](../_Port-char-store/index.md)  
  
### Enter characters  
  
In FORTH you will always designate a storage area, incorporated into the characters and strings. To do this you usually use a small, 80-character memory area called __PAD__. This note pad - so the German translation of pad used - no fixed memory area and is both the FORTH system and the programmers.  
  
Then I liked you with the text input buffer __TIB__ another important Speicherberelch imagine that ensures the reasonable use of the connected devices. Because the text input via the keyboard vorsichgeht relatively slow, the characters are collected here only in a free space, the buffer __TIB__, and then processed.  
  
- [tib](../tib/index.md)  
- [#tib](../number-tib/index.md)  
- [>tob](../to-tib/index.md)  
- [>in](../to-in/index.md)  
- [pad](../pad/index.md)  
- [input](../input/index.md)  
- [keyboard](../keyboard/index.md)  
- [empty-keys](../empty-keys/index.md)  
- [(key?](../paren-key-question/index.md)  
- [key?](../key-question/index.md)  
- [(key](../paren-key/index.md)  
- [key](../key/index.md)  
- [(decode](../paren-decode/index.md)  
- [(expect](../paren-expect/index.md)  
- [expect](../expect/index.md)  
- [span](../span/index.md)  
- [>expect](../to-expect/index.md)  
- [nullstring?](../nullstring-question?/index.md)  
- [stop?](../stop-question/index.md)  
- [source](../source/index.md)  
- [word](../word/index.md)  
- [parse](../parse/index.md)  
- [name](../name/index.md)  
- [find](../find/index.md)  
- [execute](../execute/index.md)  
- [perform](../perform/index.md)  
- [query](../query/index.md)  
- [interpret](../interpret/index.md)  
- [output](../output/index.md)  
- [display](../display/index.md)  
- [(emit](../paren-emit/index.md)  
- [emit](../emit/index.md)  
- [charout](../charout/index.md)  
- [tipp](../tipp/index.md)  
- [(type](../paren-type/index.md)  
- [type](../type/index.md)  
- [ltype](../long-type/index.md)  
- [space](../space/index.md)  
- [spaces](../spaces/index.md)  
