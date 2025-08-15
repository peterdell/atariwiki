---
title: Bugfix for the Cassette Handler
---
  
  
Fixes bugs in tape handler (except when in DOS menu-- but you can't use C: there --DOS checks for that)  
  
Thoms Newton, 1/23/1983  
  
Feel free to give copies to any person or club  
  
The program uses the INIT vector, so you should be able to append about anything else to it--like the RS-232 driver patch.  
  
```
1000 REM **************************
1010 REM ** BUGFIX--disk version **
1020 REM **************************
1030 REM
1040 REM Fixes bugs in tape handler
1050 REM (except when in DOS menu--
1060 REM but you can't use C: there
1070 REM anyway--DOS checks for that)
1080 REM
1090 REM Thoms Newton, 1/23/1983
1100 REM
1110 REM
1120 REM Feel free to give copies
1130 REM to any person or club
1140 REM
1150 REM The program uses the INIT
1160 REM vector, so you should be
1170 REM able to append about
1180 REM anything else to it--like
1190 REM the RS-232 driver patch.
1200 REM
1210 DIM A$(1)
1220 PRINT "BUGFIX -- writes AUTORUN.SYS file"
1230 PRINT "that fixes cassette handler bugs."
1240 PRINT:PRINT
1250 PRINT "Do you want to create the file (Y/N)"
1260 INPUT A$:IF LEN(A$)=0 THEN 1260
1270 IF A$="N" OR A$="n" THEN END
1280 IF A$<>"Y" AND A$<>"y" THEN 1240
1290 REM
1300 REM Create AUTORUN.SYS file
1310 RESTORE
1320 SUM=0
1330 OPEN #1,8,0,"D:AUTORUN.SYS"
1340 FOR X=1 TO 247
1350 READ Y:SUM=SUM+Y:PUT #1,Y
1360 NEXT X
1370 CLOSE #1
1380 IF SUM<>25560 THEN PRINT "There are some typos in the DATA."
1390 IF SUM<>25560 THEN XIO 33,#1,0,0,"D:AUTORUN.SYS"
1400 END
1410 REM
1420 REM Program/loading addresses
1430 REM
1440 REM All lines except the last
1450 REM should have eight numbers
1460 REM
1470 DATA 255,255,252,28,145,29,165,12
1480 DATA 141,20,29,165,13,141,21,29
1490 DATA 165,10,141,63,29,165,11,141
1500 DATA 64,29,76,22,29,32,0,0
1510 DATA 169,19,133,12,169,29,133,13
1520 DATA 169,41,133,10,169,29,133,11
1530 DATA 76,65,29,8,72,138,72,174
1540 DATA 145,29,169,64,157,27,3,169
1550 DATA 228,157,28,3,104,170,104,40
1560 DATA 76,0,0,169,243,141,231,2
1570 DATA 169,29,141,232,2,162,15,189
1580 DATA 64,228,157,146,29,202,16,247
1590 DATA 8,216,24,173,146,29,105,1
1600 DATA 141,205,29,173,147,29,105,0
1610 DATA 141,206,29,40,169,162,141,146
1620 DATA 29,169,29,141,147,29,162,0
1630 DATA 189,26,3,201,67,240,5,232
1640 DATA 232,232,208,244,142,145,29,169
1650 DATA 146,157,27,3,169,29,157,28
1660 DATA 3,24,96,0,162,29,242,29
1670 DATA 234,8,72,165,43,141,242,29
1680 DATA 165,42,41,8,141,241,29,240
1690 DATA 23,169,35,141,15,210,169,40
1700 DATA 141,8,210,169,0,141,4,210
1710 DATA 141,6,210,169,255,141,13,210
1720 DATA 104,40,32,0,0,8,72,173
1730 DATA 241,29,240,24,173,242,29,48
1740 DATA 19,169,60,141,2,211,169,160
1750 DATA 141,1,210,141,3,210,141,5
1760 DATA 210,141,7,210,104,40,96,0
1770 REM
1780 REM The original object code had
1790 REM 0,224,2,225,2,252,28
1800 REM which I changed (the RUN
1810 REM vector ==> an INIT vector)
1820 REM
1830 DATA 0,226,2,227,2,252,28
```
---
  
This program creates an autoboot tape that patches the cassette handler.  To load the tape, hold the START button down when you turn the power on.  When you hear the beep, press PLAY, then RETURN.  
  
Thomas Newton, 1/23/1983  
  
You are encouraged to give copies to any person or club.  
  
  
```
1000 REM **************************
1010 REM ** BUGFIX--tape version **
1020 REM **************************
1030 REM
1040 REM This program creates an
1050 REM autoboot tape that patches
1060 REM the cassette handler.  To
1070 REM load the tape, hold the
1080 REM START button down when you
1090 REM turn the power on.  When
1100 REM you hear the beep, press
1110 REM PLAY, then RETURN.
1120 REM
1130 REM Thomas Newton, 1/23/1983
1140 REM
1150 REM You are encouraged to give
1160 REM copies to any person or club.
1170 REM
1180 DIM PROG$(191),PAD$(65)
1190 RESTORE:SUM=0:PAD$(1,1)=CHR$(0):PAD$(64,64)=CHR$(0):PAD$(2,65)=PAD$
1200 FOR X=1 TO 191
1210 READ Y:SUM=SUM+Y:PROG$(X,X)=CHR$(Y)
1220 NEXT X
1230 IF SUM<>17627 THEN PRINT "There is a typo in the DATA.":END
1240 PRINT "Press RECORD and PLAY, then RETURN"
1250 OPEN #1,8,128,"C:":REM short IRGs
1260 PRINT #1;PROG$;:PRINT #1;PAD$;:CLOSE #1
1270 REM the above was possible because BASIC prints strings at m.l. speed
1280 END
1290 REM
1300 REM autoboot program data
1310 REM
1320 REM prepared from object file
1330 REM by removing load and run
1340 REM addresses and filling in
1350 REM the space left by the DS
1360 REM with zeroes
1370 REM
1380 DATA 0,2,0,7,13,7,169,60
1390 DATA 141,2,211,24,96,169,191,141
1400 DATA 232,2,169,7,141,232,2,162
1410 DATA 15,189,64,228,157,94,7,202
1420 DATA 16,247,8,216,24,173,94,7
1430 DATA 105,1,141,153,173,95,7
1440 DATA 105,0,141,154,7,40,169,110
1450 DATA 141,94,7,169,7,141,95,7
1460 DATA 162,0,189,26,3,201,67,240
1470 DATA 5,232,232,232,208,244,142,93
1480 DATA 7,169,94,157,27,3,169,7
1490 DATA 157,28,3,24,96,0,0,0
1500 DATA 0,0,0,0,0,0,0,0
1510 DATA 0,0,0,0,0,0,234,8
1520 DATA 72,165,43,141,190,7,165,42
1530 DATA 41,8,141,189,7,240,23,169
1540 DATA 35,141,15,210,169,40,141,8
1550 DATA 210,169,0,141,4,210,141,6
1560 DATA 210,169,255,141,13,210,104,40
1570 DATA 32,0,0,8,72,173,189,7
1580 DATA 240,24,173,190,7,48,19,169
1590 DATA 60,141,2,211,169,160,141,1
1600 DATA 210,141,3,210,141,5,210,141
1610 DATA 7,210,104,40,96,0,0
```
  
