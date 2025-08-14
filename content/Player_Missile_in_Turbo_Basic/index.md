# Player Missile in Turbo Basic  
  
## General Information  
  
Author: 	Peter J. Meyer   
Language: 	TURBO-BASIC   
Compiler/Interpreter: 	Turbo Basic 1.5   
Published: 	Oct 2007 in AtariAge   
  
Peter writes:  
  
I had this routine for years that can drive the player missile graphics in Turbo Basic XL. It works in single line mode and works with 5 players. 5th being the combination of 4 missiles. It loads the routine to $B000 (45056), but it can be moved, transfered to a string, or whatever for your purposes. The ML routine uses the Memtop (106, $6A) to match the PMBASE so you can put the player/missile into an area that does not interfere with your program or the background graphics. The ML routine saves the vertical position and size of the last player transfer just under the Missile memory area so it can be quickly erased when the next move is made.  
  
The ML routine is based upon something that was posted in Compute! magazine in the early 80s'. I added support for adding a 5th player and changed the way it erases the old sprite before drawing a new one. Also only supports one line resolution that I commonly use for programs.  
  
The subroutine call usage is:  
  
Z= USR (PMMOVE, Player Number , Source Memory Address, Memory Size, Horizontal Position, Vertical Position )  
  
Player Number can be 1 to 5  
  
  
### MAC65 Assembler Code of PMMOVE.OBJ  
  
```
1000 RAMHIGH = $6A
1010 PMYPOS = $D0
1020 PMBASE = $D1
1030 PMSAVELO = $02
1040 PMSAVEHI = $03
1050 PMNUMBER = $CD
1060 FROMLO = $CE
1070 FROMHI = $CF
1080     *=  $B000
1090 ;
1100     PLA 
1110     CMP #$05
1120     BEQ RIGHT_AMOUNT
1130     TAY 
1140 CLEANSTACK
1150     PLA 
1160     PLA 
1170     DEY 
1180     BPL CLEANSTACK
1190     RTS 
1200 RIGHT_AMOUNT
1210     PLA 
1220     PLA 
1230     CLC 
1240     ADC #$03
1250     CMP #$08
1260     BCC NOCOMBO
1270     LDA #$03
1280 NOCOMBO
1290     TAY 
1300     STA PMNUMBER
1310     CLC 
1320     ADC $6A
1330     STA PMBASE
1340     PLA 
1350     STA FROMHI
1360     PLA 
1370     STA FROMLO
1380     TYA 
1400     ASL A
1410     CLC 
1420     ADC #$EC
1430     STA PMSAVELO
1440     LDA $6A
1450     CLC 
1460     ADC #$02
1470     STA PMSAVEHI
1480     LDY #$00
1490     LDA (PMSAVELO),Y
1500     STA PMYPOS
1510     INY 
1520     LDA (PMSAVELO),Y
1530     TAY 
1540     LDA #$00
1550 CLEARLOOP
1560     STA (PMYPOS),Y
1570     DEY 
1580     BPL CLEARLOOP
1590     PLA 
1600     PLA 
1610     LDY #$01
1620     STA (PMSAVELO),Y
1630     PLA 
1640     PLA 
1650     LDX PMNUMBER
1660     CPX #$04
1670     BCS COMBOSKIP
1680     LDX #$08
1690     CLC 
1700     ADC #$08
1710     STA $CFFC,X
1720     SEC 
1730     SBC #$02
1740     INX 
1750     STA $CFFC,X
1760     SBC #$02
1770     INX 
1780     STA $CFFC,X
1790     SBC #$02
1800     INX 
1810 COMBOSKIP
1820     STA $CFFC,X
1830     PLA 
1840     PLA 
1850     STA PMYPOS
1860     LDY #$00
1870     STA (PMSAVELO),Y
1880     INY 
1890     LDA (PMSAVELO),Y
1900     TAY 
1910     DEY 
1920 DRAWLOOP
1930     LDA (FROMLO),Y
1940     STA (PMYPOS),Y
1950     DEY 
1960     BPL DRAWLOOP
1970     RTS 
1980 ;
1990 ;
2000 ;
2010     PLA 
2020     CMP #$02
2030     BEQ DOCLEAR
2040     TAY 
2050 PGCLRSTK
2060     PLA 
2070     PLA 
2080     DEY 
2090     BPL PGCLRSTK
2100     RTS 
2110 DOCLEAR
2120 PAGEBASE = $D0
2130 PAGEBSHI = $D1
2140 PAGES = $CF
2150     PLA 
2160     STA PAGEBSHI
2170     PLA 
2180     STA PAGEBASE
2190     PLA 
2200     PLA 
2210     TAX 
2220 NEXTPAGE
2230     LDY #$00
2240     TYA 
2250 PGCLRLOOP
2260     STA (PAGEBASE),Y
2270     DEY 
2280     BNE PGCLRLOOP
2290     INC PAGEBSHI
2300     DEX 
2310     BNE PGCLRLOOP
2320     RTS 
```
  
  
### Turbo Basic Demo  
  
```
5 DIM X(5),Y(5),DX(5),DY(5)
10 EXEC INIT
20 FOR N=1 TO 5
30   X(N)=60+INT(RND*120):Y(N)=60+INT(RND*120):DX(N)=-1+INT(RND*2)*2:DY(N)=-1+INT(RND*2)*2
40 NEXT N
50 DO 
60   FOR N=1 TO 5
70     Z=USR(PMMOVE,N,PMBASE,8,X(N),Y(N))
80     X(N)=X(N)+DX(N):IF X(N)<49 OR X(N)>199 THEN DX(N)=-DX(N)
90     Y(N)=Y(N)+DY(N):IF Y(N)<33 OR Y(N)>215 THEN DY(N)=-DY(N)
100   NEXT N
110 LOOP 
8000 ------------------------------
8010 PROC INIT
8020   PMPAGE=184:POKE 106,PMPAGE:GRAPHICS 0:POKE 54279,PMPAGE:POKE 710,0:POKE 712,52
8030   BLOAD "D:PMMOVE.OBJ"
8040   PMBASE=PMPAGE*256
8050   POKE 559,62:POKE 623,17:POKE 704,68:POKE 705,24:POKE 706,136:POKE 707,212:POKE 711,170:POKE 53277,3
8060   PMMOVE=45056
8070   POKE PMBASE,0
8080   MOVE PMBASE,PMBASE+1,2047
8090   FOR N=PMBASE TO PMBASE+7
8100     READ A:POKE N,A
8110   NEXT N
8120 ENDPROC 
8130 DATA 60,126,231,195,195,231,126,60
```
