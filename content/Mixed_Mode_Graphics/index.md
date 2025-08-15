---
title: Mixed Mode Graphics
---
# Mixed Mode Graphics  
  
General Information  
  
Author: Karl E. Wiegers   
Published: ANALOG   
  
## Mixed Mode Graphics Display  
  
```
0100 ;Mixed-Mode graphics displays
0110 ;in Atari assembly language
0120 ;
0130 ;by Karl E. Wiegers
0140 ;
0150     .OPT NO LIST
0160 ;
0170 OPEN =  $03     ;equates for CIO
0180 PUTREC = $09    ;operations
0190 CLOSE = $0C
0200 DRAW =  $11
0210 EOL =   $9B     ;carriage return
0220 ROWCRS = $54    ;cursor row
0230 COLCRS = $55    ;cursor column
0240 DINDEX = $57    ;graphics mode
0250 SAVMSC = $58    ;screen RAM area
0260 SDMCTL = $022F  ;screen on/off
0270 SDLSTL = $0230  ;starting address
0280 ;                of display list
0290 CRSINH = $02F0  ;disable cursor
0300 ATACHR = $02FB  ;select color reg
0310 ;
0320 ;equates for IOCB #0
0330 ;
0340 ICCOM = $0342   ;command byte
0350 ICBAL = $0344   ;buffer address,
0360 ICBAH = $0345   ;low and high
0370 ICBLL = $0348   ;buffer length,
0380 ICBLH = $0349   ;low and high
0390 ICAX1 = $034A   ;auxiliary byte 1
0400 ICAX2 = $034B   ;auxiliary byte 2
0410 CIOV =  $E456   ;CIO entry point
0420 CONSOL = $D01F  ;console buttons
0430 STRGNO = $CB    ;work byte I need
0440 SCRRAM = $4000  ;screen RAM start
0450 ;
0460 ;Display list starts at address
0470 ;$3F00, screen RAM at $4000
0480 ;
0490     *=  $3F00
0500 DLIST
0510     .BYTE 112,112,112,70,0,$40
0520     .BYTE 6,7,7,7,7,7,7,13,13
0530     .BYTE 13,13,13,13,13,13,13
0540     .BYTE 13,13,13,13,13,13,13
0550     .BYTE 13,13,13,13,13,13,13
0560     .BYTE 13,2,2,2,2,65,0,$3F
0570 ;
0580 ;program begins here
0590 ;
0600     *=  $5000
0610 ;
0620     CLD         ;binary mode!
0630     LDA #0      ;zero current
0640     STA STRGNO  ;text line counter
0650     TAX 
0660 ;
0670 ;zero out screen RAM area
0680 ;
0690 ZERO
0700     STA SCRRAM,X ;loop goes
0710     STA SCRRAM+$0100,X ;256 times
0720     STA SCRRAM+$0200,X ;each line
0730     STA SCRRAM+$0300,X ;does one
0740     STA SCRRAM+$0400,X ;page of RAM
0750     INX 
0760     BNE ZERO
0770 ;
0780 ;open screen device, "S:"
0790 ;
0800     JSR OPENSCREEN
0810     LDA #1      ;turn off cursor
0820     STA CRSINH
0830     LDA DLIST+4 ;tell ANTIC
0840     STA SAVMSC  ;where to find
0850     LDA DLIST+5 ;display memory
0860     STA SAVMSC+1
0870     LDA #0      ;turn off the
0880     STA SDMCTL  ;screen briefly,
0890     LDA #DLIST&255 ;tell ANTIC
0900     STA SDLSTL  ;where to
0910     LDA #DLIST/256 ;find the
0920     STA SDLSTL+1 ;display list,
0930     LDA #34     ;turn screen
0940     STA SDMCTL  ;back on
0950 ;
0960 ;start printing text lines
0970 ;
0980     LDA #1      ;graphics mode 1
0990     STA DINDEX
1000     JSR POSITION ;position cursor
1010     LDX #$60    ;use IOCB #6
1020     LDA #LINE1&255 ;print first
1030     STA ICBAL,X ;line of text,
1040     LDA #LINE1/256 ;in Graphics 1
1050     STA ICBAH,X ;segment
1060     JSR PRINTLINE
1070     LDA #40     ;skip ahead 40
1080     JSR ADDMEM  ;bytes in RAM
1090     LDA #2      ;Graphics mode 2
1100     STA DINDEX
1110     JSR POSITION ;position cursor
1120     LDX #$60    ;use IOCB #6
1130     LDA #LINE2&255 ;print all
1140     STA ICBAL,X ;text lines
1150     LDA #LINE2/256 ;in Graphics 2
1160     STA ICBAH,X ;segment
1170     JSR PRINTLINE
1180     LDA #120    ;go up 120 bytes
1190     JSR ADDMEM  ;in screen RAM to
1200     LDA #7      ;Graphics 7
1210     STA DINDEX  ;segment
1220 ;
1230 ;plot 1st point of rocket ship
1240 ;
1250     LDA #60     ;set coordinates
1260     STA COLCRS  ;of first point
1270     LDA #8      ;to plot for
1280     STA ROWCRS  ;rocket
1290     LDX #$60    ;use IOCB #6
1300     LDA #REG1&255 ;color register 1
1310     STA ICBAL,X
1320     LDA #REG1/256
1330     STA ICBAH,X
1340     JSR PLOTPOINT
1350 ;
1360 ;routine to draw the rocket
1370 ;
1380     LDA #2      ;color register 1
1390     STA ATACHR
1400     LDY #0
1410 POINT ;         loop to plot
1420     LDA XDATA,Y ;points and
1430     STA COLCRS  ;connect them
1440     LDA YDATA,Y ;with lines
1450     STA ROWCRS
1460     TYA 
1470     PHA 
1480     JSR DRAWLINE ;drawing sub.
1490     PLA 
1500     TAY 
1510     INY 
1520     CPY #13     ;done all 13 pts?
1530     BNE POINT   ;no, loop
1540 ;
1550 ;plot points for rocket exhaust
1560 ;
1570     LDX #$60
1580     LDA #REG0&255 ;color reg. 0
1590     STA ICBAL,X
1600     LDA #REG0/256
1610     STA ICBAH,X
1620     LDY #0
1630 POINT2 ;        loop to get
1640     LDA EXHAUSTX,Y ;coordinates
1650     STA COLCRS  ;for points
1660     LDA EXHAUSTY,Y ;from table,
1670     STA ROWCRS
1680     TYA 
1690     PHA 
1700     JSR PLOTPOINT ;plotting sub.
1710     PLA 
1720     TAY 
1730     INY 
1740     CPY #4      ;done 4 pts?
1750     BNE POINT2  ;no, loop
1760 ;
1770 ;add 960 bytes to current screen
1780 ;RAM starting point, 10*96
1790 ;
1800     LDX #10
1810 ADDEMUP
1820     LDA #96
1830     JSR ADDMEM
1840     DEX 
1850     BNE ADDEMUP
1860 ;
1870 ;now in bottom segment, Gr. 0
1880 ;
1890     LDA #0      ;Graphics 0
1900     STA DINDEX
1910     JSR POSITION ;set cursor
1920     LDX #$60    ;use IOCB #6
1930     LDA #LINE3&255 ;print first
1940     STA ICBAL,X ;text line
1950     LDA #LINE3/256 ;in Graphics 0
1960     STA ICBAH,X ;segment
1970     JSR PRINTLINE
1980     JSR POSITION ;print last
1990     LDX #$60    ;text line
2000     LDA #LINE4&255
2010     STA ICBAL,X
2020     LDA #LINE4/256
2030     STA ICBAH,X
2040     JSR PRINTLINE
2050 ;
2060 ;loop until START pressed, then
2070 ;close screen & reopen so blank
2080 ;
2090     LDA #8      ;initialize
2100     STA CONSOL  ;buttons
2110 EXIT
2120     LDA CONSOL  ;value of 6 here
2130     CMP #6      ;means START
2140     BNE EXIT    ;no? try again
2150     LDX #$60    ;close screen
2160     JSR CLOSEANY
2170     JSR OPENSCREEN ;and reopen
2180 END JMP END     ;wait for reset
2190 ;
2200 ;subroutine to open the screen
2210 ;
2220 OPENSCREEN
2230     LDX #$60    ;use IOCB #6
2240     LDA #OPEN   ;command is OPEN
2250     STA ICCOM,X
2260     LDA #SCREEN&255 ;device to open
2270     STA ICBAL,X
2280     LDA #SCREEN/256
2290     STA ICBAH,X
2300     LDA #12     ;no text window
2310     STA ICAX1,X
2320     LDA #0      ;graphics mode 0
2330     STA ICAX2,X
2340     JSR CIOV    ;go do it
2350     RTS 
2360 ;
2370 ;subroutine to close any IOCB
2380 ;
2390 CLOSEANY
2400     LDA #CLOSE  ;close screen
2410     STA ICCOM,X
2420     JSR CIOV
2430     RTS 
2440 ;
2450 ;subroutine to position cursor
2460 ;for next text string to write
2470 ;
2480 POSITION
2490     LDX STRGNO  ;get point number
2500     LDA XPOS,X  ;get x-coordinate
2510     STA COLCRS  ;and store
2520     LDA YPOS,X  ;get y-coordinate
2530     STA ROWCRS  ;and store
2540     INC STRGNO  ;ready for next
2550     RTS         ;point, and exit
2560 ;
2570 ;subroutine to print line up to
2580 ;120 chars long at cursor
2590 ;
2600 PRINTLINE
2610     LDA #120    ;maximum length
2620     STA ICBLL,X ;of text string
2630     LDA #0      ;is 120 chars.
2640     STA ICBLH,X
2650     LDA #PUTREC ;operation is to
2660     STA ICCOM,X ;PUT a RECord
2670     JSR CIOV    ;go do it
2680     RTS 
2690 ;
2700 ;subroutine to add a constant
2710 ;(in accumulator) to current
2720 ;address for start of screen RAM
2730 ;
2740 ADDMEM
2750     CLC 
2760     ADC SAVMSC  ;add constant to
2770     STA SAVMSC  ;low byte & save
2780     BCC NOINC   ;if carry set,
2790     INC SAVMSC+1 ;increment high
2800 NOINC RTS       ;byte,then exit
2810 ;
2820 ;subroutine to plot a point
2830 ;using current color register
2840 ;
2850 PLOTPOINT
2860     LDA #PUTREC
2870     STA ICCOM,X
2880     LDA #1
2890     STA ICBLL,X
2900     LDA #0
2910     STA ICBLH,X
2920     JSR CIOV
2930     RTS 
2940 ;
2950 ;subroutine to draw from last
2960 ;plotted point to current one
2970 ;
2980 DRAWLINE
2990     LDX #$60
3000     LDA #DRAW
3010     STA ICCOM,X
3020     JSR CIOV
3030     RTS 
3040 ;
3050 ;data values needed for opening
3060 ;screen and picking color regs.
3070 ;
3080 SCREEN .BYTE "S"
3090 REG0 .BYTE "A"
3100 REG1 .BYTE "B"
3110 ;
3120 ;tables of X- and Y-positions
3130 ;for lines to be printed
3140 ;
3150 XPOS .BYTE 3,0,5,11
3160 YPOS .BYTE 0,0,1,3
3170 ;
3180 ;text strings to print
3190 ;
3200 LINE1
3210     .BYTE "attack of the",EOL
3220 LINE2
3230     .BYTE "      SUICIDAL      "
3240     .BYTE "                    "
3250     .BYTE "    ROAD-RACING     "
3260     .BYTE "                    "
3270     .BYTE "       ALIENS       "
3280     .BYTE EOL
3290 LINE3
3300     .BYTE "*** Press  START  to"
3310     .BYTE " begin ***",EOL
3320 LINE4
3330     .BYTE "Analog"
3340     .BYTE " Productions",EOL
3350 ;
3360 ;tables of coordinates for
3370 ;drawing silly-looking rocket
3380 ;
3390 XDATA
3400     .BYTE 100,130,100,60,60,95
3410     .BYTE 68,81,60,60,95,68,81
3420 YDATA
3430     .BYTE 8,11,14,14,8,8,0,8
3440     .BYTE 8,14,14,22,14
3450 EXHAUSTX .BYTE 40,46,52,58
3460 EXHAUSTY .BYTE 11,11,11,11

```
  
