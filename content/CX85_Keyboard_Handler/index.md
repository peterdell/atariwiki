---
title: CX85 Keyboard Handler
---
# CX85 Keyboard Handler  
  
General Information  
  
Author: Rich Andrews, Lockport, Il   
Assembler: Mac65   
  
ac65 version  
  
Dissasembled by Rich Andrews, Lockport, Il.  
  
There was no copyright notice in the original  
code but one must assume it is public domain  
and was probably written by Atari Inc.  
(no one else would have bothered!)  
  
  
  
Call thru basic with a X=USR(32512)  
  
once called by Basic do not call again  
  
```
1000	  .TITLE "CX85 NUMERIC KEYPAD HANDLER - Mac65 version"
1010	  .PAGE "Dissasembled by Rich Andrews, Lockport, Il."
1020 ;
1030 ;There was no copyright notice in the original
1040 ; code but one must assume it is public domain
1050 ;and was probably written by Atari Inc.
1060 ;(no one else would have bothered!)
1070 ;once called by Basic do not call again
1080 ;Call thru basic with a X=USR(32512)
1090 ;
1100	  .PAGE "CX-85 EQUATES"
1110 ;******************************
1120 ;System equates used
1130 ;******************************
1140 ATRACT = $4D
1150 VVBLKD = $0224
1160 STRIG0 = $0284
1170 STRIG1 = $0285
1180 CH  =	$02FC
1190 ALLPOT = $D208
1200 PORTA = $D300
1210 SETVBV = $E45C
1220 XITVBV = $E462
1230 ;
1240 ;*****************************
1250 ;End of system equates
1260 ;*****************************
1270 ;The following is the keycode
1280 ;equates which are from CH. As
1290 ;per the Atari hardware manual.
1300 ;*****************************
1310 ;
1320 ;
1330 ESC =	$1C
1340 SPC =	$21
1350 DEL =	$34
1360 Y	=	$2B
1370 ZERO =  $32
1380 ONE =	$1F
1390 TWO =	$1E
1400 THREE = $1A
1410 FOUR =  $18
1420 FIVE =  $1D
1430 SIX =	$1B
1440 SEVEN = $33
1450 EIGHT = $35
1460 NINE =  $30
1470 PERIOD = $22
1480 MINUS = $0E
1490 CR  =	$0C
1500 ;
1510	  .PAGE "CX-85 HANDLER INSTALLATION ROUTINE"
1520 ;******************************
1530 ;This is the start of the installation routine
1540 ;******************************
1550 ;
1560 ;
1570	  .ORG $7F00  ;Start code just below GR.0 screen.
1580	  PLA			;This routine is to be called by basic hence the PLA
1590 ;Remove the PLA instruction for a stand alone file
1600	  LDA VVBLKD  ;Call with X=USR(32512)
1610 ;The installation routine could also be a M/L string with the rest
1620 ;of the code previously loaded in via DOS.
1630	  STA EXIT+1
1640	  LDA VVBLKD+1
1650	  STA EXIT+2
1660	  LDY # <VBICODE
1670	  LDX # >VBICODE
1680	  LDA #$07	 ;Command to reset vbi pointers.
1690	  JSR SETVBV  ;Install vbi routine into interrupt chain.
1700	  RTS			;Return to caller.
1710	  .PAGE "CX85 HANDLER LOOKUP TABLE"
1720 ;******************************
1730 LOOKUP ;		  This is the lookup table.  This portion can be located
1740 ;in a different area in memory than the Main routine or the
1750 ;installation routine.
1760 ;******************************
1770	  .BYTE $0C,ESC
1780	  .BYTE $14,SPC,$10,DEL,$18,Y
1790	  .BYTE $1C,ZERO,$19,ONE,$1A,TWO
1800	  .BYTE $1B,THREE,$11,FOUR,$12
1810	  .BYTE FIVE,$13,SIX,$15,SEVEN
1820	  .BYTE $16,EIGHT,$17,NINE,$1D
1830	  .BYTE PERIOD,$1F,MINUS,$1E
1840	  .BYTE CR
1850	  BRK			;End of table delimiter
1860 ;*****************************
1870 ;By changing the table one could define
1880 ;the keys on the CX85 to mean anything!
1890 ;How about some new functions to be accessed
1900 ;through a wedge of some sort?  Terminal
1910 ;program phone dialer?  Maybe a bookkeeping
1920 ;program? As long as it is a printable
1930 ;character it will work. Rich A.
1940	  .PAGE "CX-85 HANDLER MAIN VBI ROUTINE"
1950 ;*****************************
1960 ;The vbi routine starts here.
1970 ;*****************************
1980 ;This portion can be located anywhere in memory.
1990 ;*****************************
2000 VBICODE
2010	  LDA STRIG1  ;trigger pressed?
2020	  BNE SET2BYE ;no-go clr buffer #2+exit.
2030	  LDA #$00
2040	  STA ATRACT  ;kill attract mode
2050	  LDA PORTA	;lets get some bits
2060	  LSR A		 ;divide by 2
2070	  LSR A		 ;divide it again
2080	  LSR A		 ;ditto
2090	  LSR A		 ;one more time (Sam?)
2100	  STA BUFR1	;now stuff it in buffer 1
2110	  LDA ALLPOT  ;read all the pot lines
2120	  AND #$08	 ;if it is >=8,then make it 0
2130	  EOR #$08	 ;if it is <8 then make it 8
2140	  ASL A		 ;times 2
2150	  ORA BUFR1
2160	  LDY #$00
2170 ;*******************************
2180 FINDIT
2190	  CMP LOOKUP,Y
2200	  BEQ FOUND	;found the code
2210	  INY 
2220	  INY 
2230	  LDX LOOKUP,Y
2240	  BEQ EXIT
2250	  BNE FINDIT
2260 ;******************************
2270 FOUND
2280	  TAX 
2290	  INY 
2300	  LDA LOOKUP,Y
2310	  CMP BUFR2
2320	  BEQ PUTCHR
2330	  STA BUFR2
2340	  STA CH
2350	  LDA #$30
2360	  STA BUFR3
2370	  BNE EXIT	 ;always exit
2380 ;******************************
2390 SET2BYE
2400	  LDA #$C0	 ;when trig1 is not pressed
2410	  STA BUFR2	;read will come back with $C0
2420	  BNE EXIT	 ;always exit
2430 ;******************************
2440 PUTCHR
2450	  LDX BUFR3
2460	  DEX 
2470	  BNE SET3BYE
2480	  STA CH
2490	  LDA #$06
2500	  STA BUFR3
2510	  BNE EXIT
2520 ;*********************
2530 SET3BYE
2540	  STX BUFR3
2550 ;*********************
2560 EXIT
2570	  JMP XITVBV  ;see you next vbi
2580 ;*********************
2590 BUFR1
2600	  .DS 1		 ;reserve 1 byte
2610 ;*********************
2620 BUFR2
2630	  .DS 1		 ;reserve 1 byte
2640 ;*********************
2650 BUFR3
2660	  .DS 1		 ;reserve 1 byte
2670 ;*********************
2680	  .END 
2690 ;The original key layout is as
2700 ;follows
2710 ;-----------------------
2720 ; esc						|
2730 ;		 7 8 9	 -	  |
2740 ;  N	 4 5 6	 r	  |
2750 ;<del>  1 2 3	 e	  |
2760 ;  Y	  0  .	 t	  |
2770 ;							 |
2780 ;-----------------------
2790 ; <eof>
```
