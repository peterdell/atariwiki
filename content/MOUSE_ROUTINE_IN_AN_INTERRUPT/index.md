# MOUSE ROUTINE IN AN INTERRUPT  
  
  
General Information  
  
Author: John Maris (prepared by Mathy v. Nisselroy)  
Assembler: Mac65  
Published: MegaMagazine 7  
Download: [http://www.mathyvannisselroy.nl/special%20stuff.htm](http://www.mathyvannisselroy.nl/special%20stuff.htm)  
PDF: [mouse.pdf](attachments/mouse.pdf)  
  
## Abstract  
  
OK, here is the text that accompanied the mouse routine I posted  
on alt.binaries.atari. Unfortunately the original file was self  
extracting. So I had to print it out and type it back in. I hope  
somebody will read the stuff below and use it in his or her own  
program. The text and code where written for the Atari 8 bit,  
but the idea should work on other computers too.  
  
~[number](../number/index.md) means that there is a small explanation for those not living in the Atari 8 bit world at the bottom of the text.  
  
Mathy van Nisselroy  
  
## Mouse Routine in an Interrupt  
  
By The Missing Link [1](../1/index.md)  
  
In the last years the mouse became very popular, even on Atari  
8-bit machines. I've seen a lot of routines, but none of them  
were working very good. They took almost all processor time in  
the main loop or they were very slow, etc. I talked to your  
editor [2](../2/index.md) very often about this subject and we were both working  
on a better routine. I decided to put my mouse routine into a  
Pokey [3](../3/index.md) Timer Interrupt....  
  
A few month ago while I was shopping, I got the great idea.  
Finally I knew how to do it. I went home, started MAC65 [4](../4/index.md),  
typed some lines in 10 minutes, and the routine worked great!  
  
The first routine worked in a DLI [5](../5/index.md) and VBI [6](../6/index.md). So I knew that  
it was possible to put a mouse routine in such an interrupt. I  
could even load from disk or play some samples while I was  
playing with the mouse. A few days later Freddy [2](../2/index.md) visited me  
and he was amazed. I showed him my routine and he was surprised  
because of the length and the frequency. The routine was short,  
very fast and worked very good. You should have seen his face  
when I was playing a mouse, while the computer loaded the  
directory into the machine....  
  
Later I told to some other programmers about this routine and now  
we can see a lot of mouse routines which work in an interrupt.  
Most of these routines are still slow or you get a 'flying'  
cursor. If you move the mouse too fast, the cursor will move in  
reversed direction or will even NOT move. After I had seen these  
'f**king' routines I decided to publish my routine on Mega  
Magazine [7](../7/index.md) with some documentation, so everybody can use a  
better mouse routine. I've called it the 'TML Mouse Routine'. The  
routine is public domain, but it would be nice if you let me know  
(or MegaZine [7](../7/index.md)) if you use the routine in one of your products.  
It would be nicer if you mention the creator in your programs....  
  
### How the routine works  
  
Depending on the mouse (ST or AMIGA) you will get 4 numbers if  
you move the mouse horizontal and 4 other numbers for the  
vertical direction. For example: Move the mouse from left to  
right and you will get the numbers (STICK(0 or 1) [8](../8/index.md) ) 1 2 3 4 1  
2 3 4 1 2 3 4 1 2 3 4 etc. (these aren't the right numbers, but  
it is only an example). If you read stick(0) twice, you have two  
numbers and will know in what direction the mouse moved... If you  
get a 1 and a 2, the mouse was moved to the right and if you get  
a 2 and a 1, the mouse was moved to the left. You can do the same  
thing for the vertical direction.  
  
Now you can create a very big routine with compares, etc., but  
that will take a lot of time and you have to check the stick very  
often (Freddy did such a routine in the main loop and there was  
no time left for any other action), I have made a interrupt  
routine which checked the mouse 800 times in a second. This  
routine worked like all routines, get a new value from the mouse,  
compare it to the old value and do some action. This routine was  
also large and didn't work very good. The trick is the use of an  
'action table'. Get the old value shift it to the left two times  
and add the new value. Now you will have a unique value between 0  
and 15. Use this value as index for the table.  
  
An example:  
  
Old value = 2 (shifted 2x makes 8)  
  
New value = 1 (add to 8)  
  
Index value = 9  
  
Earlier I wrote that a 2 and a 1 was a movement to the left, so  
we have to decrease the X-pointer. Position 9 will be a 255 in  
the index tabel.  
  
Old value = 1 (shifted 2x makes 4)  
  
New value = 2 (add to 4)  
  
Index value = 6  
  
Numbers 1 and 2 is a movement to the right, we have to increase the  
X-pointer. We have to put on the sixth position in the index  
table a 1.  
  
Conclusion: Now we have only to shift the old value 2 times, add  
the new value, use it as index, and add the value we've got to  
the X-position. We can do the same for the Y-position. This is a  
very fast routine which takes just some time. But still, this is  
not the final one....  
  
Sometimes you will get the same value. (old = 1 and new = 1) This  
means that there was no mouse action or a very very fast action  
in unknown direction. Do nothing, so put 0 in your index table on  
position (1+4=5).  
  
The same for 1 and 3. Of course, there must have been some  
action, but you can't know what kind of action. It is two steps  
if the mouse is moved to the right, but also two steps if the  
mouse was moved to the left. So no action on (3+4=7) in your  
index table.  
  
The last part was the most important part of this textfile. If  
you don't know what kind of action there was, even if you are  
sure that there was some action, do nothing! If you do anything  
you will get a reversed mouse or a 'flying' one.  
  
On the backside of this disk you will find a pre-screen of my new  
texteditor. You can play with it, open some windows, etc., but  
that's all. Just an example. You can also find the mouse-source  
on this disk. It's in MAC65 [4](../4/index.md) format. This one is public  
domain. Use it have a lot of fun, as long as you remember that  
you took it from this great magazine [7](../7/index.md) and remember who wrote  
the routine. See you next time!  
  
[1](../1/index.md) John Maris, founder of A.N.G.  
  
[2](../2/index.md) Freddy Offenga, editor of [7](../7/index.md)  
  
[3](../3/index.md) Sound chip of the Atari 8bit computer  
  
[4](../4/index.md) MAC65: Assembler software  
  
[5](../5/index.md) DLI: small piece of software that tells the graphics co-processor (ANTIC) in the Atari 8 bit what to do  
  
[6](../6/index.md) VBI: Vertical Blank Interrupt.  
  
[7](../7/index.md) Mega Magazine or just MegaZine: A disk magazine for the Atari 8 bit computer. Seven issues appeared, then they stopped.  
  
[8](../8/index.md) STICK (0) or STICK (1): an Atari BASIC command used to read  
joystick ports pins 1 through 4.  
  
For those who wanna look at the code, the PIA, which controls the joysticks in the Atari, is placed at $D300-$D303. Should the source use a different address between $D300 and $D3FF, just substract 4 off this number untill  
you get in the above mentioned range. BTW apart from the  
occasional SPACE and capital, I changed nothing about this text.  
  
```
1000 ;MOUSE ROUTINE IN A DLI
1010 ; MAKE YOUR OWN DL WITH
1020 ;INTERUPT ENABLE, ETC.
1030 ;OR YSE THE INTERUPT IN
1040 ;POKEY TIME INTERUPT!
1050 ;
1060 ;PUBLIC DOMAIN 1994
1070 ;PUBLISHED ON MEGAMAGAZINE
1080 ;             POKEY MAGZINE
1090 ;             THE BEST OF...
1100 ;
1110 ;WRITTEN BY THE MISSING LINK
1120 ;
1130 ;OLDX = OLD X-VALUE MOUSE
1140 ;OLDY = OLD Y-VALUE MOUSE
1150 ;MXAS = X POSITION FOR CURSOR
1160 ;MMAXX=MAXIMUM X-SCREEN-POS
1170 ;MMAXY=MAXIMUM Y-SCREEN-POS
1180 ;MMINX=MINIMUM X-SCREEN-POS
1190 ;MMINY=MINIMUM Y-SCREEN-POS
1191 ;
1200 ;SET INTERRUPTPOINTER
1210     LDA # <MOUSE
1220     STA 512
1230     LDA # >MOUSE
1240     STA 513
1250 ;INIT MOUSE ROUTINE
1260     JSR MOUSEON
1270 ;INIT VBI ROUTINE FOR CURSOR
1280     LDA #6
1290     LDX # >VBI
1300     LDY # <VBI
1310     JSR $E45C
1320 ;ENDLESS LOOP
1330 DO  JMP DO
1340 ;
1350 ;
1360 ;THE MOUSEROUTINE
1370 MOUSE
1380     PHA 
1390     TXA 
1400     PHA 
1410     TYA 
1420     PHA 
1430 MOUSEA
1440     LDA $D300   ;
1450     LSR A       ;MOUSE ON
1460     LSR A       ;PORT 1
1470     LSR A       ;
1480     LSR A       ;
1490     PHA         ;SAVE VALUE
1500     AND #3      ;GET X-VALUE
1510     ORA OLDX    ;
1520     TAX         ;
1530     AND #3      ;MAKE X-INDEX
1540     ASL A       ;
1550     ASL A       ;
1560     STA OLDX    ;SAVE AS OLD
1570     LDY MXAS    ;
1580     LDA MOUSETAB,X ;GET TABLE
1590     BMI MOUSY   ;ACTION? NO!
1600     BNE MOUSE1  ;YES! DECREASE
1610 MOUSE0
1620     INY         ;INCREASE
1630     CPY MMAXX   ;MAXIMUM XAS?
1640     BCC MOUSY   ;NO, EXIT
1650 MOUSE1
1660     DEY         ;DECREASE
1670     CPY MMINX   ;MINIMUM XAS?
1680     BCC MOUSE0  ;YES! INCREASE
1690 MOUSY
1700     STY MXAS    ;STORE XPOINTER
1710     PLA         ;GET MOUSEVALUE
1720     LSR A
1730     LSR A       ;SEE THE ROUTINE
1740     AND #3      ;ON THE XAS. IT
1750     ORA OLDY    ;IS THE SAME!
1760     TAX 
1770     AND #3
1780     ASL A
1790     ASL A
1800     STA OLDY
1810     LDY MYAS
1820     LDA MOUSETAB,X
1830     BMI MOUSEX
1840     BNE MOUSE2
1850 MOUSE1.1
1860     INY 
1870     JMP MOUSE3
1880 MOUSE2
1890     DEY 
1900 MOUSE3
1910     CPY MMINY
1920     BCC MOUSE1.1
1930     CPY MMAXY
1940     BCS MOUSE2
1950 MOUSEX ;        END OF
1960     STY MYAS    ;Y-ROUTINE
1970     PLA         ;RESTORE
1980     TAY         ;A, X & Y
1990     PLA 
2000     TAX 
2010     PLA 
2020     RTI 
2030 ;
2040 ;THE Indextable 0=no action
2050 MOUSETAB
2060     .BYTE 255,1,0,255,0,255,255,1,1,255,255,0,255,0,1,255
2070 ;
2080 ;ENABLE DLI
2090 MOUSEON
2100     LDA #192
2110     STA $D40E
2120     RTS 
2130 ;DISABLE DLI
2140 MOUSEOFF
2150     LDA #64
2160     STA $D40E
2170     RTS 
2180 ;
2190 VBI
2200 ;PUT CURSOR ON SCREEN...
2210     JMP $E45F
2220 ;
2230 ;
```
