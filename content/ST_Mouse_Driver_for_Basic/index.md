---
title: ST Mouse Driver for Basic
---
# ST Mouse Driver for Basic  
  
This is driver for an Atari ST mouse for Atari Basic and Turbo Basic  
  
General Information  
  
Author: Carsten Strotmann   
Assembler: Bibo Assembler   
Published: 04/22/91   
  
Atari Basic or even TurboBasic is way too slow to process the low level data send by an Atari ST Mouse to move a mouse pointer in a usable way.  
  
The ML routine below will read the information from the Atari ST mouse, will paint a mouse cursor until one of the mouse buttons are pressed (with an unmodified Atari ST mouse you can only read one mouse button from an A8, but it is possible to modify an Atari ST mouse in a way that the A8 can read both mouse buttons and the mouse is still usable on an Atari ST).  
  
### Usage:  
  
you load the ML routine MOUSE.COM (from DOS as Autorun.sys or from TurboBasic with BLOAD "D:MOUSE.COM")  
  
then, in your Basic Programm you call the routine at $400  
  
```
100 ...
110 x = USR($400) : REM Turbo Basic
120 ...
```
  
```
100 ...
110 x = usr(1024) : REM Atari Basic
120 ...
```
  
while in the Mouse Routine, your BASIC Programm is stopped. Line 120 will executed when one mouse button has been pressed.  
  
STRIG(0) -- first mouse button  
and  
STRIG(1) -- 2nd mouse button  
  
you can get the information which mouse button has been pressed.  
  
Peek($03FD) will give you the x position of the mouse pointer,  
Peek($03FE) will give you the y position of the mouse pointer  
  
It should be straigghtforward to assemble the Assembler code in any Assembler (Mac/65, ATASm, x-asm ...). With BiboAssembler (also in the Wiki as ATR download) you can just type in the source.  
  
Mirko Sobe from BOSS X has asked me to write a VBI driven Mouse Driver for his BOSS X System. I have that on my to-do list. Such a mouse driver would run an the same time as the basic program.  
  
```
00010			 .LI OFF
00020 ******************************
00030 *									 *
00040 * PROGRAMM:MOUSE ROUTINE	  *
00050 * AUTOR	:CARSTEN STROTMANN *
00060 * DATUM	:22.04.91			 *
00070 * VERSION :04.00				 *
00080 * FUER	 :ALLGEMEIN			*
00090 *									 *
00100 ******************************
00110 ;
00120 ; SYSTEM REGISTER
00130 ;
00140 XM		 =	$03FD
00150 YM		 =	$03FE
00160 SETVBV	=	$E45C
00170 SYSVBV	=	$E45F
00180 XITVBV	=	$E462
00190 SDMCTL	=	$022F
00200 PMBASE	=	$D407
00210 VCOUNT	=	$D40B
00220 GRACTL	=	$D01D
00230 PORTA	 =	$D300
00240 STICK0	=	$0278
00250 STRIG0	=	$0284
00260 STRIG1	=	$0285
00270 HPOS0	 =	$D000
00280 PCOL0	 =	$02C0
00290 GPRIOR	=	$026F
00300 ;
00310 ;
00320			 .OR $0400
00330			 .OF "D:MOUSE.COM"
00340 ;
00350 ;
00360 BS
00370			 PLA			BASIC !
00380			 PLA
00390			 PLA
00400			 STA PCOL0
00410 X		  LDA #$78
00420			 STA PMBASE
00430			 LDA #$3A
00440			 STA SDMCTL
00450			 LDA #2
00460			 STA GRACTL
00470			 STA GPRIOR
00480			 LDX /PLAYVBI
00490			 LDY #PLAYVBI
00500			 LDA #7
00510			 JSR SETVBV
00520 LOOP	  JMP RUN
00530 ------------------------------
00540 PLAYVBI
00550			 LDA XM
00560			 CLC
00570			 ADC #49
00580			 STA HPOS0
00590			 LDX #0
00600			 TXA
00610 .1		 STA $7C00,X
00620			 INX
00630			 BNE .1
00640			 LDX YM
00650			 LDY #0
00660 .2		 LDA PLAYTAB,Y
00670			 STA $7C20,X
00680			 INX
00690			 INY
00700			 CPY #11
00710			 BNE .2
00720			 JMP XITVBV
00730 ------------------------------
00740 END
00750			 RTS
00760 ------------------------------
00770 PLAYTAB
00780			 .HX 0080C0E0F0E0E0B0
00790			 .HX 101000
00800 XT		 .HX 0020301000
00810 YT		 .HX 80C0400080
00820 REG		.HX 00
00830 REG2	  .HX 00
00840 XX		 .HX 00
00850 YY		 .HX 00
00860 ------------------------------
00870 STICK
00880			 LDA STICK0
00890			 TAY
00900			 CMP #15
00910			 BEQ .5
00920			 TYA
00930			 AND #2
00940			 BEQ .1
00950			 LDA YM
00960			 BEQ .1
00970			 DEC YM
00980 .1
00990			 TYA
01000			 AND #1
01010			 BEQ .2
01020			 LDA YM
01030			 CMP #191
01040			 BEQ .2
01050			 INC YM
01060 .2
01070			 TYA
01080			 AND #8
01090			 BEQ .3
01100			 LDA XM
01110			 BEQ .3
01120			 DEC XM
01130 .3
01140			 TYA
01150			 AND #4
01160			 BEQ .4
01170			 LDA XM
01180			 CMP #159
01190			 BEQ .4
01200			 INC XM
01210 .4
01220			 LDA VCOUNT
01230			 BNE .4
01240 .5
01250			 RTS
01260 ------------------------------
01270			 .OR $0600
01280 RUN
01290			 JSR STRIG
01300			 LDA PORTA
01310			 AND #$30
01320			 STA REG
01330			 JSR XFRAG
01340			 JSR XALG
01350			 LDA PORTA
01360			 AND #$C0
01370			 STA REG2
01380			 JSR YFRAG
01390			 JSR YALG
01400			 JMP RUN
01410 XALG
01420			 JSR STICK
01430			 JSR STRIG
01440			 LDA PORTA
01450			 AND #$30
01460			 CMP REG
01470			 BEQ YALG
01480			 LDX XX
01490			 INX
01500			 CMP XT,X
01510			 BNE .1
01520			 LDA XM
01530			 CMP #159
01540			 BEQ .2
01550			 INC XM
01560			 JMP .2
01570 .1		 LDX XX
01580			 DEX
01590			 CMP XT,X
01600			 BNE .2
01610			 LDA XM
01620			 BEQ .2
01630			 DEC XM
01640 .2		 RTS
01650 YALG
01660			 JSR STICK
01670			 JSR STRIG
01680			 LDA PORTA
01690			 AND #$C0
01700			 CMP REG2
01710			 BEQ XALG
01720			 LDX YY
01730			 INX
01740			 CMP YT,X
01750			 BNE .1
01760			 LDA YM
01770			 CMP #191
01780			 BEQ .2
01790			 INC YM
01800			 JMP .2
01810 .1		 LDX YY
01820			 DEX
01830			 CMP YT,X
01840			 BNE .2
01850			 LDA YM
01860			 BEQ .2
01870			 DEC YM
01880 .2		 RTS
01890 ------------------------------
01900 XFRAG
01910			 LDX #4
01920 .1		 LDA XT,X
01930			 CMP REG
01940			 BEQ .2
01950			 DEX
01960			 BNE .1
01970 .2		 STX XX
01980			 RTS
01990 ------------------------------
02000 YFRAG
02010			 LDX #4
02020 .1		 LDA YT,X
02030			 CMP REG2
02040			 BEQ .2
02050			 DEX
02060			 BNE .1
02070 .2		 STX YY
02080			 RTS
02090 ------------------------------
02100 STRIG
02110			 LDA STRIG0
02120			 BNE .1
02130			 PLA
02140			 PLA
02150			 JMP END
02160 .1		 LDA STRIG1
02170			 BNE .2
02180			 PLA
02190			 PLA
02200			 JMP END
02210 .2		 RTS
02220 ------------------------------
```
