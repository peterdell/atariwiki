---
title: DOS XL 2.30 patch
---
# DOS XL 2.30 patch  
  
Version 2.30p was a newer version to 2.30 to fix two problems.  
  
- In previous versions of DOS XL, if you initialized a disk from the menu, the disk would not boot unless the file MENU.COM was on the disk. To alleviate this problem, type Q to quit the menu. Then type INIT or INITDBL from the command processor. Note: everything on the menu can be done manually from the command processor.  
- If you have a multidrive system and you initialized a disk in a drive other than one, when booted, the disk will always come up with the number of the drive on which it was initialized. To prevent this problem, use D1: as the destination drive.  
  
The patch for DOS XL 2.30 to make it a 2.30p:  
```
OSS Disk Newsletter
Fall 1986
Product News & Info
DOS XL - New-found Bugs

DOS XL Bugs and Fixes
---------------------

BUG: The patch to convert version
2.30 to version 2.30p in our Spring
1984 newsletter didn't work.
FIX: Run the following program and
then use INIT with the "Write DOS.SYS
Only" option to write out the patched
DOS. Make sure that you don't have
DOSXL.SYS (either .SUP or .XL
version) active when you do this.

100 READ CNT:IF CNT=0 THEN END
110 READ START
120 FOR ADDR=START TO START+CNT-1
130 READ BYTE:POKE ADDR,BYTE
135 NEXT ADDR
140 GOTO 100
150 DATA 3,5481,32,1,21
160 DATA 29,5377,141,217,22,169,16
170 DATA 141,23,22,169,23,141,24,22
180 DATA 169,49,141,30,22,169,64,141
190 DATA 12,0,169,21,141,13,0,96
200 DATA 1,7425,112,0

BUG: INIT does not work if you use
drive numbers 4 through 8.
FIX: Run the following program:

10 OPEN #1,12,0,"D:INIT.COM"
20 FOR I=1 TO 116 : GET #1,C : NEXT I
30 PUT #1,ASC("9") : CLOSE #1
```
