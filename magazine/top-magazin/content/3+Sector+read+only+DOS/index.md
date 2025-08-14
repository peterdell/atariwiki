### 3SDOS - 3Sector Read-Only DOS  
  
- Assembler: BiboAssembler 1.21  
- License: GNU Public License, http://www.gnu.org  
- Author: Carsten Strotmann  
- Version: 0.8  
- Description: Mini-Read-Only DOS 2.x compatible  
  
## Why?  
  
Why I've written this DOS? I had a BASIC Cassette program. The program consists of two files, ==part1.bas== and ==part2.bas== .  
The first part initializes a new character-set and the starts the second part via the CLOAD command.  
  
The second part was really large. Because the cassette load take some time, I would like to have a disk version. But with a normal DOS loaded (MyDOS, ATARI DOS 2.x, 3, DOS XL, Turbo DOS, I tried almost all), there was only some byte free memory left. Too less to run the programm.  
  
So I tested serveral game-dos. (btw, thanks to Matthias Reichl for the new GPL Release of MyPicoDos, [http://www.horus.com/~hias/atari/](http://www.horus.com/~hias/atari/)). But the game-dos I own don't install a "D:" CIO Handler, they just load the file and start it. That is ok for one-part files, but it didn't work with my two-part file.  
  
So I wrote 3SDOS. It's 384 Bytes long and fits into the first 3 bootsectors. With this, the basic-cassette program works! And it has 4k free space.  
  
## Limitations:  
  
- only read operations  
- "open file" and "get byte" CIO commands  
- only finds files in the first directory sector ($169), so only the first 8 directory entries work  
- no checks  
- slower that normal dos load, but dos starts very fast!  
- maybe buggy  
  
## Future development  
  
- Autoload and Start Basic program in the first Directory entry, for real Basic-Boot-Disks  
- keep it in 3 sectors (SD)  
  
## Download  
  
- See attachments for an empty DOS DISK (SD)  
  
## FAQ  
  
- How to write the DOS to a new Disk?  
- copy sector 1-3 from a 3SDOS Disk to the new Disk  
- or, take the source and write a setup program :-)  
  
```
00010    .LI OFF
00020 *************************
00030 *                       *
00040 * 3SECTOR DOS 3SDOS     *
00050 * A LOW MEMORY DOS 2.X  *
00060 *                       *
00070 * READ ONLY VERSION     *
00080 *                       *
00090 * (C) 2003 C. STROTMANN *
00100 * LICENSED UNDER GPL    *
00110 *                       *
00120 *************************
00130 ;
00140 ; SIO CONTROL BLOCK
00150 ;
00160 DDEVIC   =   $0300
00170 DUNIT    =   $0301
00180 DCMND    =   $0302
00190 DSTATS   =   $0303
00200 DBUF     =   $0304
00210 DTIMLO   =   $0306
00220 DBYT     =   $0308
00230 DAUX1    =   $030A
00240 DAUX2    =   $030B
00250 ;
00260 ; ZERO PAGE REGISTERS
00270 ;
00280 ICHIDZ   =   $20
00290 ICDNOZ   =   $21
00300 ICCOMZ   =   $22
00310 ICSTAZ   =   $23
00320 ICBADZ   =   $24
00330 ICBPLZ   =   $26
00340 ICBBLZ   =   $28
00350 ICAX1Z   =   $2A
00360 ICAX2Z   =   $2B
00370 ICSPRZ   =   $2C
00380 ICHIDNOZ =   $2E
00390 ;
00400 ; FLOPPY SIO COMMANDS
00410 ;
00420 RDSEC    =   $52
00430 ;
00440 ; SECTOR SIZE
00450 ;
00460 SECSIZ   = $80
00470 ;
00480 ; SIO STATUSBYTE
00490 ;
00500 DREAD    = $40
00510 ;
00520 ; OS VECTORS
00530 ;
00540 DOSVEC   = $0A
00550 DOSINI   = $0C
00560 SIO      = $E459
00570 CIO      = $E456
00580 PHENTV   = $E486
00590 BIBOMON  = $E471
00600 ;
00610 ; START OF USER MEM
00620 ;
00630 MEMLO    = $02E7
00640 ;
00650 ; SCREEN MEM
00660 SAVMSC   = $58
00670 ;
00680 ; INIT VECTOR
00690 ;
00700 RUNAD    = $02E0
00710 INITAD   = $02E2
00720 ;
00730 ; HANDLER TABLE
00740 ;
00750 HATABS   =   $031A
00760 ;
00770 ; ERROR CODES
00780 ;
00790 ERR_OK   =   $01 ; NO ERROR
00800 ERR_BRK  =   $80 ; BREAK KEY
00810 ERR_EOF  =   $88 ; END OF FILE
00820 ERR_NFND =   $AA ; NOT FOUND
00830 ERR_JOPN =   $A1 ; JUST OPEN
00840 ;
00850 ; HANDLER CHAR "D:"
00860 HNDCHAR  = 'D
00870 ;
00880 ; SECTORS
00890 ;
00900 VTOC     =   $0168
00910 DIR      =   $0169
00920 ;
00930 ; BUFFER 128 BYTE
00940 ;
00950 SECBUF   =   $600
00960 ;
00970 ; FILENAME BUFFER 11 BYTE
00980 ;
00990 FNAME    =   $100
01000 ;
01010 ORG      .OR $700
01020          .OF D:SDOS.COM
01030 ;
01040 DATA
01050 SECCNT   = $D4
01060 BUFCNT   = $D6
01070 BUFEOF   = $D7
01080 DIRCNT   = $D7
01090 CURSEC   = $D8
01100 DIRP     = $DA
01110 ;
01120 ; BOOT HEADER
01130 ;
01140 BOOTH    .HX 00
01150          .HX 03 ; 3 SEC DOS
01160          .DA BOOTH ; STORE ADDR
01170          .DA DOSIN
01180 ;
01190 ; SET MEMLO
01200          LDA #PGMEND
01210          STA MEMLO
01220          LDA /PGMEND
01230          STA MEMLO+1
01240 ;
01250 ; SET RESTART VECTOR
01260          LDA #FHINIT
01270          STA DOSVEC
01280          LDA /FHINIT
01290          STA DOSVEC+1
01300 ;
01310 ; BOOTMESSAGE
01320          JSR PMSG
01330 ;
01340          CLC
01350          RTS
01360 ;
01370 ;
01380 ; DOS INI ROUTINE
01390 ;
01400 DOSIN
01410          JSR FHINIT  ; INIT HANDLER
01420          RTS
01430 ;
01440 ------------------------------
01450 INIT
01460 FHINIT
01470          LDX #0
01480 .1
01490          LDA HATABS,X
01500          BEQ INSTALL
01510          CMP #HNDCHAR
01520          BEQ INSTALL
01530          INX
01540          INX
01550          INX
01560          CPX #$20
01570          BMI .1
01580 ;
01590          RTS
01600 ------------------------------
01610 ; INSTALL HANDLER
01620 ;
01630 INSTALL
01640          LDA #HNDCHAR
01650          STA HATABS,X
01660          LDA #FHTAB
01670          STA HATABS+1,X
01680          LDA /FHTAB
01690          STA HATABS+2,X
01700 RESETS
01710          LDA #DOSIN
01720          STA DOSINI
01730          LDA /DOSIN
01740          STA DOSINI+1
01750          RTS
01760 ------------------------------
01770 SECRD
01780          LDA #$01 ; DISK 1
01790          STA DUNIT
01800          LDA #$31 ; FLOPPY
01810          STA DDEVIC
01820          LDA #RDSEC ; READ
01830          STA DCMND
01840          LDA #DREAD
01850          STA DSTATS
01860          LDA #SECSIZ
01870          STA DBYT
01880          LDA #0
01890          STA DBYT+1
01900          LDA #SECBUF
01910          STA DBUF
01920          LDA /SECBUF
01930          STA DBUF+1
01940          LDA CURSEC
01950          STA DAUX1
01960          LDA CURSEC+1
01970          STA DAUX2
01980 ;
01990          JSR SIO
02000 ;
02010          LDA SECBUF+$7F
02020          STA BUFEOF
02030          DEC SECCNT
02040          LDA SECBUF+$7D
02050          AND #$03
02060          STA CURSEC+1
02070          LDA SECBUF+$7E
02080          STA CURSEC
02090          LDA #$FF
02100          STA BUFCNT
02110          RTS
02120 ------------------------------
02130 FSPECIAL
02140 FSTATUS
02150 SDOSINIT
02160 FCLOSE
02170 OK       LDY ERR_OK
02180 FPUTBYT
02190          RTS
02200 ------------------------------
02210 FOPEN
02220          LDA ICAX1Z ; AUX1
02230          AND #$04   ; READ?
02240          BEQ FCLOSE ;NO WRITE!
02250          LDA #DIR
02260          STA CURSEC
02270          LDA /DIR
02280          STA CURSEC+1
02290          JSR SECRD
02300          LDA #SECBUF
02310          STA DIRP
02320          LDA /SECBUF
02330          STA DIRP+1
02340          LDA #7
02350          STA DIRCNT
02360 ;
02370 ; SEARCH DIR ENTRY
02380 ;
02390 SDIR
02400          LDY #$0F
02410          LDA #$20
02420 .1       STA FNAME,Y
02430          DEY
02440          BPL .1
02450 ;
02460          LDY #0
02470 .2
02480          INY
02490          LDA (ICBADZ),Y
02500          CMP #':
02510          BNE .2
02520 ;
02530          INY
02540          TYA
02550          CLC
02560          ADC ICBADZ
02570          STA ICBADZ
02580          BCC .3
02590          INC ICBADZ+1
02600 .3
02610          LDY #0
02620          LDX #5
02630 .4
02640          LDA (ICBADZ),Y
02650          CMP #'.
02660          BNE .5
02670          LDX #$D
02680          INY
02690 .5
02700          LDA (ICBADZ),Y
02710          STA FNAME,X
02720          INY
02730          INX
02740          CPX #$10
02750          BNE .4
02760 .6
02770          LDY #$F
02780 .7       LDA (DIRP),Y
02790          CMP FNAME,Y
02800          BNE .10
02810          DEY
02820          CPY #4
02830          BNE .7
02840          LDA (DIRP),Y
02850          STA CURSEC+1
02860          DEY
02870          LDA (DIRP),Y
02880          STA CURSEC
02890          DEY
02900          LDA (DIRP),Y
02910          STA SECCNT+1
02920          DEY
02930          LDA (DIRP),Y
02940          STA SECCNT
02950 ;
02960          JSR SECRD
02970          LDY #ERR_OK
02980          RTS
02990 .10
03000          LDA #$10
03010          CLC
03020          ADC DIRP
03030          STA DIRP
03040          BCC .11
03050          INC DIRP+1
03060 .11
03070          DEC DIRCNT
03080          BNE .6
03090          LDY #ERR_NFND
03100          RTS
03110 ;
03120          JMP BIBOMON
03130 ;
03140 ------------------------------
03150 FGETBYT
03160 ;        JMP BIBOMON
03170          LDX BUFEOF
03180          BNE .10
03190          JSR SECRD
03200 .10
03210          LDX SECCNT
03220          CPX #$FF
03230          BNE .20
03240          LDY #ERR_EOF
03250          RTS
03260 .20
03270          INC BUFCNT
03280          DEC BUFEOF
03290          LDX BUFCNT
03300          LDA SECBUF,X
03310          JMP OK
03320 ------------------------------
03330 FHTAB
03340          .DA FOPEN-1
03350          .DA FCLOSE-1
03360          .DA FGETBYT-1
03370          .DA FPUTBYT-1
03380          .DA FSTATUS-1
03390          .DA FSPECIAL
03400          JMP SDOSINIT
03410          .DA #0
03420 PGMEND
03430 ------------------------------
03440 MSG
03450          .AT "    3SDOS (c)2003 CST/PSC "
03460 MSGEND   .HX 00
03470 ------------------------------
03480 PMSG
03490          LDY #$FF
03500 .1       INY
03510          LDA MSG,Y
03520          STA (SAVMSC),Y
03530          CPY #MSGEND-MSG
03540          BNE .1
03550          RTS
03560 ------------------------------
03570          .OR RUNAD
03580          .DA INIT
03590 ------------------------------


```
