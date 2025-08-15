---
title: 6502 Relocator
---
General Information   
Author: Bob Sander-Cederlof   
Assembler: generic   
Published: APPLE Assembly Line 01/82   
Download: [Apple Assembly Line Archive](http://www.txbobsc.com/aal/)   
  
  
Programs that are already assembled usually must be loaded at a specific memory address to execute properly.  If you want to run it somewhere else, you have a problem.  All the data references, JMP's, and JSR's will have to be examined to see if they need to be modified for the new location.  If you don't have the source code, you can't re-assemble it.  The other way, patching, can be quite a tedious operation!  
  
Fortunately, way back in 1977, the WOZ (Steve Wozniak to you newcomers) wrote a program to do the work automatically.  If you have the Programmer's Aid ROM then you have his RELOCATE program.  You who have Apple II Plusses with the Language Card (also called 16K RAM card) can also use his program, because it is in the INTBASIC file along with Integer BASIC.  (The latter group of people probably don't have the manual, though, because they didn't buy the ROM.)  
  
I would like to see the RELOCATE program made more widely available, but it cannot be used as is unless you have Integer BASIC.  Why?  Because it uses SWEET-16 opcodes.  RELOCATE also is itself tied to running at whatever location it is assembled for, so it can be a little trouble to find a place for it sometimes.  By now you have probably guessed that I have recoded RELOCATE to solve both of these problems!  
  
Paul Schlyter's article elsewhere in this issue of AAL shows RELOCATE put to good use.  You can examine his instructions and learn most of what you need to know to use RELOCATE on your own programs.  Basically, there are four steps:  
  
  
1.  Initialize.  This sets up the control-Y monitor command.  If RELOCATE is on a file, you do this with "BRUN RELOCATE".  
  
2.  Specify the program start and end addresses (where it now is in memory), and the new starting address (where you want it to be relocated to).  This is done with the monitor command:  {code}target<start.end^Y*{code} where "target" is the new starting address, and "start" and "end" are the addresses of the program where it is now.  "^Y" means "control-Y".  The "*" after the control-Y signals RELOCATE that you are in step 2 rather than step 3 or 4.  
  
3.  Specify the FIRST block to be copied "as-is" or to be "relocated" to the destination area.  This is done with the monitor command:  
{code}target<start.end^Y{code} or  {code}target<start.endM{code} where "target" is the starting address in the new area for this block, and "start" and "end" define the block itself.  Note that there is no trailing asterisk this time.  Use control-Y if you want this block relocated, or M if you want it copied as-is.  
  
4.  Specify the NEXT block to be copied as-is or relocated.  You do this with the monitor command: {code}.end^Y{code} or {code}.endM{code} where the target and start addresses are assumed to immediately follow the previously handled block, and "end" specifies the end of this new block.  Use control-Y to relocate the block, or M to copy it as-is.  
  
Obviously, step 4 above is repeated until the whole program has been copied/relocated.  For each block of your program that is to be copied as-is, with no modification at all, you use the "M" command; for each block to be relocated you use the "control-Y" command.  
  
If you need more detailed instructions and explanation, I must refer you to the manual.  The Programmer's Aid #1 Manual is sold at most computer stores separately from the ROM package.  Pages 11-28 explain why and how to use RELOCATE, and pages 80 and 81 contain the assembly listing.  
  
Now here is my new version, which can be BRUN anywhere you have 134 ($86) bytes available.  I have eliminated the SWEET-16 usage; this made the program slightly bigger, and a lot faster.  
  
Lines 1260-1380 are the initialization code.  They build the control-Y vector at $3F8-3FA.  A JMP opcode is stored at $3F8; if you have DOS up this is redundant, but it won't hurt.  Next I have to try to find myself.  That is, where in memory am I (the program RELOCATE) located?  JSR MON.RETURN (which is only an RTS instruction, so it comes right back without doing anything) puts the address of the third byte of the JSR instruction on the stack.  Lines 1290-1370 use that address to compute the address of RELOC, and store it in $3F9 and $3FA.  
  
When you type in a control-Y command, the monitor will now branch to RELOC at line 1400.  Lines 1400-1430 look at the character after the control-Y in the command input buffer; if it is an asterisk, then you are trying to do step 2 above.  If not, then you are on step 3 or 4.  Lines 1440-1500 handle step 2, and lines 1510-1990 handle steps 3 and 4.  
  
The part which used to be coded in SWEET-16 was lines 1690-1880.  The SWEET-16 version took only 14 bytes, while the 6502 code takes 34 bytes.  The 6502 version may take about 100 microseconds to execute, and the SWEET-16 version on the order of 1000 microseconds (for each instruction relocated).  
  
---
  
```
 1000  *
 1010  *		6502 RELOCATION SUBROUTINE
 1020  *
 1030  *		MAY BE LOADED ANYWHERE, AS IT IS SELF-RELOCATABLE
 1040  *
 1050  *		ADAPTED FROM SIMILAR PROGRAM IN PROGRAMMERS AID #1
 1060  *		ORIGINAL PROGRAM BY WOZ, 11-10-77
 1070  *		ADAPTED BY BOB SANDER-CEDERLOF, 12-30-81
 1080  *		(ELIMINATED USAGE OF SWEET-16)
 1090  *
 1100  MON.YSAV	.EQ $34  COMMAND BUFFER POINTER
 1110  MON.LENGTH .EQ $2F  # BYTES IN INSTRUCTION - 1
 1120  MON.INSDS2 .EQ $F88E  DISASSEMBLE (FIND LENGTH OF OPCODE)
 1130  MON.NXTA4  .EQ $FCB4	  UPDATE POINTERS, TEST FOR END
 1140  MON.RETURN .EQ $FF58
 1150  STACK		.EQ $0100	  SYSTEM STACK
 1160  INBUF		.EQ $0200	  COMMAND INPUT BUFFER
 1170  *
 1180  A1	  .EQ $3C,3D
 1190  A2	  .EQ $3E,3F
 1200  A4	  .EQ $42,43
 1210  R1	  .EQ $02,03
 1220  R2	  .EQ $04,05
 1230  R4	  .EQ $08,09
 1240  INST	.EQ $0A,0B,0C
 1250  *
 1260  START  LDA #$4C	  JMP OPCODE
 1270			STA $3F8	  BUILD CONTROL-Y VECTOR
 1280			JSR MON.RETURN	 FIND OUT WHERE I AM FIRST
 1290  START1 TSX
 1300			DEX			 POINT AT LOW BYTE
 1310			SEC			 +1
 1320			LDA STACK,X  LOW BYTE OF START1-1
 1330			ADC #RELOC-START1
 1340			STA $3F9
 1350			LDA STACK+1,X	HIGH BYTE OF START1-1
 1360			ADC /RELOC-START1
 1370			STA $3FA
 1380			RTS
 1390  *
 1400  RELOC  LDY MON.YSAV COMMAND BUFFER POINTER
 1410			LDA INBUF,Y  GET CHAR AFTER CONTROL-Y
 1420			CMP #$AA	  IS IT "*"?
 1430			BNE RELOC2	NO, RELOCATE A BLOCK
 1440			INC MON.YSAV YES, GET BLOCK DEFINITION
 1450			LDX #7		 COPY A1, A2, AND A4
 1460  .1	  LDA A1,X
 1470			STA R1,X
 1480			DEX
 1490			BPL .1
 1500			RTS
 1510  *
 1520  RELOC2 LDY #2		 COPY NEXT 3 BYTES FOR MY USE
 1530  .1	  LDA (A1),Y
 1540			STA INST,Y
 1550			DEY
 1560			BPL .1
 1570			JSR MON.INSDS2  GET LENGTH OF INSTRUCTION
 1580			LDX MON.LENGTH  0=1 BYTE, 1=2 BYTES, 2=3 BYTES
 1590			BEQ .3		 1-BYTE OPCODE
 1600			DEX
 1610			BNE .2		 3-BYTE OPCODE
 1620			LDA INST	  2-BYTE OPCODE
 1630			AND #$0D	  SEE IF ZERO-PAGE MODE
 1640			BEQ .3		 NO (X0 OR X2 OPCODE)
 1650			AND #$08
 1660			BNE .3		 NO (80-FF OPCODE)
 1670			STA INST+2	CLEAR HIGH BYTE OF ADDRESS FIELD
 1680  *
 1690  .2	  LDA R2		 COMPARE ADDR TO END OF SOURCE BLOCK
 1700			CMP INST+1
 1710			LDA R2+1
 1720			SBC INST+2
 1730			BCC .3		 ADDR > SRCEND
 1740			SEC			 COMPARE ADDR TO BEGINNING OF SRC
 1750			LDA INST+1
 1760			SBC R1
 1770			TAY
 1780			LDA INST+2
 1790			SBC R1+1
 1800			BCC .3		 ADDR < SRCBEG
 1810			TAX
 1820			TYA			 ADDR = ADDR-SRCBEG+DESTBEG
 1830			CLC
 1840			ADC R4
 1850			STA INST+1
 1860			TXA
 1870			ADC R4+1
 1880			STA INST+2
 1890  *
 1900  .3	  LDX #0		 COPY MODIFIED INSTRUCTION TO DESTINATION
 1910			LDY #0
 1920  .4	  LDA INST,X	NEXT BYTE OF THIS INSTRUCTION
 1930			STA (A4),Y
 1940			INX
 1950			JSR MON.NXTA4	 ADVANCE A1 AND A4, TEST FOR END
 1960			DEC MON.LENGTH  TEST FOR END OF THIS INSTRUCTION
 1970			BPL .4		 MORE IN THIS INSTRUCTION
 1980			BCC RELOC2	END OF SOURCE BLOCK
 1990			RTS

```
  
---
  
Comment:  
  
Bob Sander-Cederlof | 19.11.2007 at 03:59 PM  
Thank you for republishing my article. The Apple Assembly Line newsletter was published from monthly October 1980 through May 1988. All the issues are available online at http://www.txbobsc.com/aal/  
