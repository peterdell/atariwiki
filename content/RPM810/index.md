---
title: RPM810
---
### Program to measure 810 disk speed  
  
General Information  
  
Author: 	Carl D. Howe   
Language: 	BASIC   
Compiler/Interpreter: 	Atari Basic   
Published: 	28 Oct 1981 19:35:38 EST (Wednesday)   
  
## How to use  
  
The following is my DSKRPM program that I described in a previous message. It is not entirely deterministic; I assume that this is because of heterodyning between BASIC execution and the disk rotation. However, I have not really verified this fact; if anyone has any ideas any ideas, please let me know.  
  
Carl cdh@BBN-UNIX  
  
P.S. The proper number to get is about 292 RPM.  
  
```
01 LET READS=25
05 DIM BUF$(256),PROG$(20)
10 GOSUB 2000:GOSUB 1000
15 P1=PEEK(18):P2=PEEK(19):P3=PEEK(20)
20 FOR I=1 TO READS
30 GOSUB 1000
40 NEXT I
43 Q1=PEEK(18):Q2=PEEK(19):Q3=PEEK(20)
45 BGTIME=P1*65536+P2*256+P3
50 DNTIME=Q1*65536+Q2*256+Q3
60 PRINT 3600*READS/(DNTIME-BGTIME);" RPM"
70 GOTO 10
1000 REM THIS IS THE READ SECTOR ROUTINE
1010 DCB=3*256
1030 POKE DCB+1,1
1040 POKE DCB+2,5*16+2
1050 HIADDR=INT(ADR(BUF$)/256)
1060 LOWADDR=ADR(BUF$)-HIADDR*256
1070 POKE DCB+4,LOWADDR
1080 POKE DCB+5,HIADDR
1090 POKE DCB+10,1
1100 POKE DCB+11,0
1110 A=USR(B):RETURN 
1900 REM THIS ROUTINE GENERATES A
1902 REM SMALL MACHINE LANGUAGE
1904 REM ROUTINE AS FOLLOWS:
1906 REM PLA
1908 REM JSR DSKINV
1910 REM RTS
2000 B=ADR(PROG$)+1
2010 POKE B,6*16+8
2020 POKE B+1,2*16
2030 POKE B+2,5*16+3
2040 POKE B+3,14*16+4
2050 POKE B+4,6*16
2060 RETURN 
```
