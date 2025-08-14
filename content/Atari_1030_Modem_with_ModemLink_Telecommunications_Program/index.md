# Atari 1030 Modem with ModemLink Telecommunications Program by Penril ; Copyright (C) 1983 Atari, Inc.  
Atari 1030 Modem with:  
- 300 bps  
- Bell 103/113 modem compatible  
- built-in ModemLink software on rom  
- 2 SIO ports  
## Manual  
- [Atari 1030 Modem-Owner's Guide](http://data.atariwiki.org/DOC/Atari_1030_Modem_Owner_s_Guide.pdf) ; size: 34.8 MB  
## ROM-Image  
- [Atari_1030.rom](attachments/Atari_1030.rom) ; this software was soldered into the modem. With the great work from AtariGeezer from AtariAge it was possible to preserve this rare to find software for generations to come. Thank you AtariGeezer, we owe you very much! :-)  
## BIN-Image  
- [Atari_1030.bin](attachments/Atari_1030.bin) ; same as above in bin-format  
## ATR-Images  
- [Atari_1030.atr](attachments/Atari_1030.atr) ; ATR-Image with 1030 programs and the above roms  
- [Atari_1030_Express_2.1.atr](attachments/Atari_1030_Express_2.1.atr)  
- [Atari_1030_Antic.atr](attachments/Atari_1030_Antic.atr) ; Software on diskette from the review in ANTIC, please see below  
## Image  
![](attachments/Atari_1030-Modemlink.jpg)  
Atari 1030 Modem with ModemLink Telecommunications Program - startscreen  
  
## Review  
- [Review in ANTIC, VOL. 4, NO. 4 from AUGUST 1985](http://www.atarimagazines.com/v4n4/1030modem.html) ; UNLEASHING THE 1030 MODEM, Secrets of its built-in device handler by Russ Wetmore  
Listings from the above review (Programs for use with the Atari 1030, written in BASIC)  
  
__Listing 1:__  
  
```
MF 10 REM MAKEAUTO.BAS
QO 20 REM BY RUSS WETMORE, FOR STAR SYSTEMS SOFTWARE, INC.
BN 30 REM ANTIC PUBLISHING
GA 40 ? "[ESC] [SHIFT] [CLEAR] Press [REVERSE VIDEO]  START  [REVERSE VIDEO] to create":? "AUTORUN.SYS file."
GW 50 IF PEEK(53279)<>6 THEN 50
CG 60 GRAPHICS 2+16:? #6:? #6;"    CREATING":? #6;"AUTORUN.SYS FILE"
XF 70 DATA 255,255,0,6,30,6,162,9,189,21
YK 80 DATA 6,157,0,3,202,16,247,32,89,228
RK 90 DATA 48,4,24,32,12,29,96,88,1,60
OA 100 DATA 64,0,29,2,0,48,11,224,2,225
AZ 110 DATA 2,0,6
OB 120 CLOSE #1: OPEN #1,8,0,"D:AUTORUN.SYS"
MK 130 TRAP 160
KX 140 READ A:? #1;CHR$(A);
NI 150 GOTO 140
IJ 160 CLOSE #1:END
```
__Listing 2:__  
  
```
FS 1 REM MINI-1030
DB 2 REM BY RUSS WETMORE, FOR STAR SYSTEMS SOFTWARE, INC.
UD 3 REM ANTIC PUBLISHING
UP 4 GOSUB 13
HR 5 IF PEEK(1024)=0 THEN 7
QL 6 GET #5,I: IF I>31 THEN ? CHR$(I);
JX 7 IF PEEK(764)<255 THEN GET #4,I:PUT #5,I
QR 8 STATUS #5,I:IF PEEK(747)>127 THEN 5
VS 9 GOTO 10
TX 10 ? :? CHR$(253);"MODEM DISCONNECTED!":FOR I=1 TO 1000:NEXT I:I=USR(58484)
YE 11 ? "ERROR-";PEEK(195):GOTO 10
JS 12 ? "1030 HANDLER HAS NOT BEEN LOADED!":GOTO 10
QJ 13 DIM E$(1),F$(20):GRAPHICS 0:W=710:POKE 709,14:POKE W,0:E$=CHR$(27):? ,"MINI1030":TRAP 12
IC 14 CLOSE #4:CLOSE #5:OPEN #4,4,0,"K:":OPEN #5,12,0,"T:":TRAP 11
RD 15 ? :? "PHONE # ";:INPUT F$:IF F$="" THEN 15
JR 16 POKE 7,1
OI 17 ? #5;E$;"N":REM IF PULSE
HE 18 ? #5;E$;"O":REM IF TONE
IE 19 ? CHR$(28);"DIALING..";F$:? #5;E$;"K";F$
NU 20 STATUS #5,I:IF PEEK(747)<128 THEN 20
AE 21 POKE W,144:? CHR$(125):? "CONNECTED!":? :POKE 7,1:? #5;E$;"Y":POKE 7,0:RETURN
```
