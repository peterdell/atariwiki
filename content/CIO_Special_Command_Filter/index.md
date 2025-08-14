# CIO Filter  
  
  
This is a small ASM Routine that is a Filter Driver for the DOS CIO (D:) Handler. It intercepts the CIO calls and checks for SPECIAL commands.  
  
## Download  
  
ATR-Disc Image: [CIO Filter/FILTER.ATR](../CIO_Special_Command_Filter/index.md)  
  
## Filter Usage  
  
Set start Sector Number  
  
XIO 200,#chan, __sec-high__ , __sec-low__ ,"D:"  
  
- __chan__ - IO Channel  
- __sec-high__ - sectornumber, highbyte  
- __sec-low__ - sectornumber, lowbyte  
  
Set destination memory  
  
XIO 201,#chan, __mem-high__ , __mem-low__ ,"D:"  
  
- __chan__ - IO Channel  
- __mem-high__ - memory, highbyte  
- __mem-low__ - memory, lowbyte  
  
Read sector  
  
XIO 202,#chan, __count-high__ , __count-low__ ,"Dx:"  
  
- __chan__ - IO Channel  
- __count-high__ - sector count, highbyte (not implemented in this version)  
- __count-low__ - sector count, lowbyte (not implemented in this version)  
- __Dx:__ - Diskdrive number  
  
Write sector  
  
XIO 203,#chan, __count-high__ , __count-low__ ,"Dx:"  
  
- __chan__ - IO Channel  
- __count-high__ - sector count, highbyte (not implemented in this version)  
- __count-low__ - sector count, lowbyte (not implemented in this version)  
- __Dx:__ - Diskdrive number  
  
  
## Assembler (Bibo Assembler Source)  
  
```
00010          .LI OFF
00020 ******************************
00030 *                            *
00040 * PROGRAMM:DEVICE FILTER     *
00050 * AUTOR   :CARSTEN STROTMANN *
00060 * DATUM   :09.11.02          *
00070 * VERSION :1                 *
00080 * FUER    :ABBUC/APG         *
00090 *                            *
00100 ******************************
00110 ;
00120 ; SIO CONTROL BLOCK
00130 ;
00140 DDEVIC   =   $0300
00150 DUNIT    =   $301
00160 DCMND    =   $302
00170 DSTATS   =   $303
00180 DBUF     =   $304
00190 DTIMLO   =   $306
00200 DBYT     =   $308
00210 DAUX1    =   $30A
00220 DAUX2    =   $30B
00230 ;
00240 ; ZERO PAGE IOCB
00250 ;
00260 ICHIDZ   =   $20
00270 ICDNOZ   =   $21
00280 ICCOMZ   =   $22
00290 ICSTAZ   =   $23
00300 ICBADZ   =   $24
00310 ICBPLZ   =   $26
00320 ICBLLZ   =   $28
00330 ICAX1Z   =   $2A
00340 ICAX2Z   =   $2B
00350 ICSPRZ   =   $2C
00360 ICHIDNOZ =   $2E
00370 ;
00380 ; SCRATCH ZP BYTES
00390 ; USED DURING INSTALL
00400 HATBV    =   $DA
00410 ;
00420 ; FLOPPY-SIO BEFEHLE
00430 ;
00440 RDSEC    =   $52 ;SECTOR READ
00450 WRTSEC   =   $50 ;SECTOR WRITE
00460 SPDCNF   =   $4B ;CONFIGURATION
00470 JMPNOK   =   $4C ;JUMP
00480 JMPWOK   =   $4D ;JUMP & OK
00490 RDPERC   =   $4E ;PERCOM READ
00500 WRTPERC  =   $4F ;PERCOM WRITE
00510 ;
00520 ; SIO STUSBYTE
00530 ;
00540 DREAD    =   $40
00550 DWRITE   =   $80
00560 ;
00570 ; JUMP VECTORS
00580 ;
00590 SIO      =   $E459
00600 CIO      =   $E456
00610 PHENTV   =   $E486
00620 WARMSV   =   $E474
00630 ;
00640 ; HANDLERTABELLE
00650 ;
00660 HATABS   =   $31A
00670 ;
00680 ; MOEGLICHE FEHLERMELDUNGEN
00690 ;
00700 STOK     =   $01 ;OK
00710 BRKKEY   =   $80 ;BREAK KEY
00720 EOF      =   $88 ;END OF FILE
00730 WDD      =   $A0 ;WRONG DISK
00740 DSKFL    =   $A2 ;DISK FULL
00750 NFND     =   $AA ;NOT FOUND
00760 JOPN     =   $A1 ;JUST OPEN
00770 ;
00780 ; INIT VECTOR
00790 ;
00800 RUNAD    =   $02E0
00810 INITAD   =   $02E2
00820 ;
00830 ; DOSINIT
00840 ;
00850 DOSINI   =   $0C
00860 ;
00870 ; SPEICHERZEIGER
00880 ;
00890 MEMLO    =   $2E7
00900 LOMEM    =   $80
00910 ;
00920 ------------------------------
00930 ;
00940 ORG      .OR $0600
00950          .OF D:FILTER.COM
00960 ;
00970 DOSSPCV  .HX 0000
00980 MEMPTR   .HX 0000
00990 SECPTR   .HX 0000
01000 XSAVE    .HX 00
01010 YSAVE    .HX 00
01020 DDENS    .HX 80
01030 ;
01040 DOSIN
01050          JSR WARMSV
01060          JSR FHINIT
01070          RTS
01080 ------------------------------
01090 INIT
01100          LDA DOSINI
01110          STA DOSIN+1
01120          LDA DOSINI+1
01130          STA DOSIN+2
01140          LDA #DOSIN
01150          STA DOSINI
01160          LDA /DOSIN
01170          STA DOSINI+1
01180 ------------------------------
01190 ; FILTER HANDLER INIT
01200 ; SCANNING DEVICE HANDLER
01210 ; TABLE FOR DOS ENTRY
01220 FHINIT
01230          LDX #0
01240 .1
01250          LDA HATABS,X
01260          BEQ NODOS ; END TABLE
01270          CMP #'D
01280          BEQ INSTALL
01290          INX
01300          INX
01310          INX
01320          CPX #$20
01330          BMI .1
01340 ;
01350 NODOS    RTS
01360 ------------------------------
01370 INSTALL
01380          LDA HATABS+1,X
01390          STA HATBV
01400          LDA HATABS+2,X
01410          STA HATBV+1
01420          LDY #$A ;PTR TO SPECIAL
01430          LDA (HATBV),Y
01440          STA DOSSPCV
01450          LDA #FSPECIAL-1
01460          STA (HATBV),Y
01470          INY
01480          LDA (HATBV),Y
01490          STA DOSSPCV+1
01500          LDA /FSPECIAL-1
01510          STA (HATBV),Y
01520 ;        LDA #PGMEND
01530 ;        STA MEMLO
01540 ;        STA LOMEM
01550 ;        LDA /PGMEND
01560 ;        STA MEMLO+1
01570 ;        STA LOMEM+1
01580          RTS
01590 ------------------------------
01600 FSPECIAL
01610 OLDVEC
01620          STY YSAVE
01630          STX XSAVE
01640          LDX ICAX1Z
01650          LDY ICAX2Z
01660          LDA ICCOMZ
01670          CMP #$C8
01680          BNE .1
01690          JMP SETSEC
01700 .1
01710          CMP #$C9
01720          BNE .2
01730          JMP SETMEM
01740 .2
01750          CMP #$CA
01760          BNE .3
01770          JMP READSEC
01780 .3
01790          CMP #$CB
01800          BNE .4
01810          JMP WRITESEC
01820 .4
01830 .10
01840          LDX XSAVE
01850          LDY YSAVE
01860          LDA DOSSPCV+1
01870          PHA
01880          LDA DOSSPCV
01890          PHA
01900          RTS
01910 ------------------------------
01920 SETMEM
01930          STX MEMPTR+1
01940          STY MEMPTR
01950 CIOOK
01960          LDY #1
01970          RTS
01980 ------------------------------
01990 SETSEC
02000          STX SECPTR+1
02010          STY SECPTR
02020          JMP CIOOK
02030 ------------------------------
02040 READSEC
02050          LDA #RDSEC
02060          STA DCMND
02070          LDA #DREAD
02080          STA DSTATS
02090 DOSIO
02100          LDA ICDNOZ ; DEV #
02110          STA DUNIT
02120          LDA #$31
02130          STA DDEVIC
02140          LDA DDENS
02150          STA DBYT
02160          LDA #0
02170          STA DBYT+1
02180 ;
02190          LDA SECPTR
02200          STA DAUX1
02210          LDA SECPTR+1
02220          STA DAUX1+1
02230          LDA MEMPTR
02240          STA DBUF
02250          LDA MEMPTR+1
02260          STA DBUF+1
02270          LDA #7
02280          STA DTIMLO
02290 ;
02300          JMP SIO
02310 ;
02320 WRITESEC
02330          LDA #WRTSEC
02340          STA DCMND
02350          LDA #DWRITE
02360          STA DSTATS
02370          JMP DOSIO
02380 ------------------------------
02390 PGMEND
02400          .OR RUNAD
02410          .DA INIT
02420 ------------------------------

```
  
## Turbo-BASIC Demo  
  
```
100 ------------------------------
110 REM SIMPLE SECTORCOPY
120 REM SECTOR 1-720, 128 BYT/SEC
130 ------------------------------
140 BRUN "D:FILTER.COM"
150 DIM MEM$(18*$80)
160 MEM=ADR(MEM$)
170 DIM DRIVE$(13)
180 FOR SEC=1 TO 720 STEP 18
190   DRIVE$="D1:"
200   FOR X=0 TO 17
210     XSEC=SEC+X
220     XMEM=MEM+(X*$80)
230     XIO 200,#3,TRUNC(XSEC/$0100),XSEC,DRIVE$
240     XIO 201,#3,TRUNC(XMEM/$0100),XMEM,DRIVE$
250     ? " LESE SEKTOR",XSEC;:? ">",HEX$(XMEM)
260     XIO 202,#3,0,0,DRIVE$
270   NEXT X
280   DRIVE$="D2:"
290   FOR X=0 TO 17
300     XSEC=SEC+X
310     XMEM=MEM+(X*$80)
320     XIO 200,#3,TRUNC(XSEC/$0100),XSEC,DRIVE$
330     XIO 201,#3,TRUNC(XMEM/$0100),XMEM,DRIVE$
340     ? " SCHREIBE SEKTOR",XSEC;:? ">",HEX$(XMEM)
350     XIO 203,#3,0,0,DRIVE$
360   NEXT X
370 NEXT SEC
380 ? " READY!"
```
