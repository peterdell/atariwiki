  
  
# Hobbytronic Demo 2004/2005  
  
Unfinished work  
  
  
See discussion in ABBUC Programmers Forum at http://www.abbuc.de/  
  
Demo-Part "Maurer" (File HT1.COM) can be started from HTWORK.ATR with a Gamedos or from HTLoader or from BiboMon or similar.  
  
## Finished Part: HobbyTronic Loader  
  
```
01000             .LI OFF
01010 ************************
01020 ** HOBBY TRONIC LOADER *
01030 ** 2004 BY C. STROTMANN*
01040 ** FROM HT92 LOADER    *
01050 ************************
01060 ;
01070 RTCLOK   =   $12
01080 SOUNDR   =   $41
01090 ATRACT   =   $4D
01100 NMIEN    =   $D40E
01110 IRQEN    =   $D20E
01120 POKMSK   =   $10
01130 SCOLOR   =   $02C4
01140 SDMCTL   =   $022F
01150 DMACTL   =   $D400
01160 VDSLST   =   $200
01170 COLOR    =   $D016
01180 WSYNC    =   $D40A
01190 DLIST    =   $D402
01200 SDLSTL   =   $0230
01210 CHBASE   =   $D409
01220 CHBAS    =   $02F4
01230 PORTB    =   $D301
01240 DSKIV    =   $E450
01250 VVBLKI   =   $0222
01260 VVBLKD   =   $0224
01270 AUDF1    =   $D200
01280 HPOSPL   =   $D000
01290 SFLNUM   =   $067D   ; FIL#
01300 ;
01310 SYSVBV   =   $E45F
01320 XITVBV   =   $E462
01330 ;
01340 DDEVIC   =   $300
01350 DUNIT    =   $301
01360 DCMND    =   $302
01370 DBUF     =   $304
01380 DBYT     =   $308
01390 DAUX     =   $30A
01400 ;
01410 SIOV     =   $E453
01420 ZMEMPTR  =   $D0
01430 RUNAD    =   $02E0
01440 INITAD   =   $02E2
01450 ;
01460          .OR $0600
01470 ;        .OF D:HTLOAD.COM
01480 ;
01490 SECBUF
01500 BOOTHT
01510          .HX 00
01520 NUMSEC   .HX 08
01530 BASEADR  .HX 0006
01540 INIT     .HX A906
01550 ;
01560          JMP START
01570 ------------------------------
01580 DL
01590          .HX 7070707070
01600          .HX 7070707070
01610          .HX 707070F070
01620          .HX 42
01630          .DA TEXT
01640          .HX 70707041
01650          .DA DL
01660 ------------------------------
01670 TEXT
01680          .AT "          BOOTBLOCK STILL OK :)         "
01690 ------------------------------
01700 COLTAB
01710          .HX C2C2C4C4C6C6C8C8
01720          .HX CACACCCCCCCCCACA
01730          .HX C8C8C6C6C4C4C2C2
01740 SPARE    .HX 00
01750 ------------------------------
01760 START
01770          LDA #0
01780          STA RTCLOK+2
01790          STA RTCLOK+1
01800          STA NMIEN   ; NMI OFF
01810          STA SCOLOR+1
01820          LDA #DLI
01830          STA VDSLST  ; SET DLI
01840          LDA /DLI
01850          STA VDSLST+1
01860          LDA #DL
01870          STA SDLSTL
01880          LDA /DL
01890          STA SDLSTL+1
01900          LDA #$C0
01910          STA NMIEN   ; NMI ON
01920 WAIT
01930          LDA RTCLOK+2
01940          CMP #$64
01950          BNE WAIT
01960          JMP DEMOLOAD
01970 ------------------------------
01980 DLI
01990          PHA         ;SAV ACCU
02000          TXA
02010          PHA         ;SAV X
02020          LDX #0
02030 .1
02040          LDA COLTAB,X
02050          STA WSYNC
02060          STA COLOR+2
02070          STA COLOR+4
02080          INX
02090          CPX #$19
02100          BNE .1
02110          PLA
02120          TAX
02130          PLA
02140          RTI
02150 ------------------------------
02160 MEMPTR   .DA $0600
02170 NUMBYT   .HX 7F
02180 SECTOR   .HX 0000
02190 STARTADR .HX 0000
02200 ENDADR   .HX 0000
02210 DEMOCNT  .HX 00
02220 DIRBUF
02230 DIRFLG   .HX 00
02240 FILELEN  .HX 0000
02250 STARTSEC .HX 0000
02260 FILENAME .HX 0000000000000000
02270          .HX 00000000000000
02280 DEMOFLG  .HX 00
02290 FILENUM  .HX 00
02300          .HX 40      ; ??
02310 ------------------------------
02320 DL2      .HX 7042
02330          .DA TEXT2
02340          .HX 41
02350          .DA DL2
02360 ------------------------------
02370 TEXT2
02380          .AT " HOBBYTRONIC DEMO 2004 LOADING ...      "
02390 ------------------------------
02400 READSEC
02410          LDA #$31
02420          STA DDEVIC
02430          LDA #$1
02440          STA DUNIT
02450          LDA #$52    ; READ
02460          STA DCMND
02470          LDA MEMPTR
02480          STA DBUF
02490          LDA MEMPTR+1
02500          STA DBUF+1
02510          LDA NUMBYT
02520          STA DBYT
02530          LDA NUMBYT+1
02540          STA DBYT+1
02550          LDA SECTOR
02560          STA DAUX
02570          LDA SECTOR+1
02580          STA DAUX+1
02590 ;
02600          JSR SIOV
02610 ;
02620          RTS
02630 ------------------------------
02640 SECOFF   .HX 00
02650 ;
02660 GETBYTSEC    ; GET NEXT BYTE
02670              ; FROM SECTOR
02680          LDY SECOFF
02690          LDA SECBUF,Y
02700          PHA
02710          INC SECOFF
02720          LDA SECOFF
02730          CMP #$7D    ; DATA IN SECTOR
02740          BNE .1
02750          LDA #0
02760          STA SECOFF
02770          JSR SECCHAIN
02780 .1
02790          PLA
02800          RTS
02810 ------------------------------
02820 BUF
02830 ------------------------------
02840          .OR $780
02850 DEMOLOAD
02860          JMP INITDL
02870 ------------------------------
02880 GETCOMHEAD
02890          JSR GETBYTSEC
02900          STA STARTADR
02910          JSR GETBYTSEC
02920          STA STARTADR+1
02930 ;
02940          LDA STARTADR
02950          CMP #$FF
02960          BNE .1
02970          LDA STARTADR+1
02980          CMP #$FF
02990          BNE .1
03000 ;
03010          JSR GETBYTSEC
03020          STA STARTADR
03030          JSR GETBYTSEC
03040          STA STARTADR+1
03050 .1
03060          JSR GETBYTSEC
03070          STA ENDADR
03080          JSR GETBYTSEC
03090          STA ENDADR+1
03100 ;
03110          LDA STARTADR
03120          STA ZMEMPTR
03130          LDA STARTADR+1
03140          STA ZMEMPTR+1
03150          LDA RUNAD
03160          BNE .2
03170          LDA RUNAD+1
03180          BNE .2
03190 ;
03200          LDA STARTADR
03210          STA RUNAD
03220          LDA STARTADR+1
03230          STA RUNAD+1
03240 .2
03250          RTS
03260 ------------------------------
03270 SECCHAIN
03280          LDX #$7D
03290          LDA SECBUF,X
03300          AND #3
03310          STA SECTOR+1
03320          INX
03330          LDA SECBUF,X
03340          STA SECTOR
03350          JMP READSEC
03360 ------------------------------
03370 DLIRTI    RTI
03380 ------------------------------
03390 MINIDL
03400          .HX 7041
03410          .DA MINIDL
03420 ------------------------------
03430 INITDL
03440          LDA #MINIDL
03450          STA SDLSTL
03460          STA DLIST
03470          LDA /MINIDL
03480          STA SDLSTL+1
03490          STA DLIST+1
03500 ; FRAME BLACK
03510          LDA #0
03520          STA SCOLOR+4
03530          STA COLOR+4
03540 ; IO SOUND ETC
03550          STA SOUNDR
03560          STA ATRACT
03570          STA SDMCTL
03580          STA DMACTL
03590 ; RESET FONT
03600          LDA #$E0
03610          STA CHBASE
03620          STA CHBAS
03630 ;
03640          LDX #5
03650 .1
03660          STA SCOLOR,X
03670          STA COLOR,X
03680          DEX
03690          BPL .1
03700 ;
03710          STA IRQEN
03720          STA NMIEN
03730          STA POKMSK
03740          SEI
03750          LDA PORTB
03760          ORA #3
03770          STA PORTB   ; ROM ON
03780 ;
03790          LDA #$40
03800          STA IRQEN
03810          STA POKMSK
03820          CLI
03830 ;
03840          LDA #0
03850          STA SCOLOR+2
03860          STA SCOLOR+4
03870 ;
03880          LDA #$E
03890          STA COLOR+1
03900          STA SCOLOR+1
03910 ;
03920          LDA #SYSVBV
03930          STA VVBLKI
03940          LDA #XITVBV
03950          STA VVBLKD
03960 ;
03970          LDA /SYSVBV
03980          STA VVBLKI+1
03990          STA VVBLKD+1
04000 ;
04010          LDA #DLIRTI
04020          STA VDSLST
04030          LDA /DLIRTI
04040          STA VDSLST+1
04050 ;
04060          LDA #DL2
04070          STA SDLSTL
04080          LDA /DL2
04090          STA SDLSTL+1
04100 ;
04110 NOSOUND
04120          LDX #7
04130          LDA #0
04140 .1
04150          STA AUDF1,X
04160          STA HPOSPL,X
04170          DEX
04180          BPL .1
04190 CLRSTACK
04200          PHA
04210          LDX #0
04220 .1
04230          LDA #0
04240          STA $100,X
04250          INX
04260          BNE .1
04270 ;
04280          LDA #$FF
04290          STA $1FF
04300 .2
04310          PLA
04320          BEQ .2
04330 ;
04340          LDA #$60
04350          STA NMIEN   ; VBI OFF
04360          LDA #$22
04370          STA SDMCTL
04380          STA DMACTL  ; DMA ON
04390          JSR DSKIV
04400 ;
04410          LDA #0
04420          STA RUNAD
04430          STA RUNAD+1
04440          STA INITAD
04450          STA INITAD+1
04460          STA DEMOFLG
04470 READDIR
04480          LDA #$69
04490          STA SECTOR
04500          LDA #1
04510          STA SECTOR+1
04520          JSR READSEC
04530          LDA DEMOCNT
04540          ASL
04550          ASL
04560          ASL
04570          ASL         ; * 16
04580          TAX
04590          LDY #0
04600 .1
04610          LDA SECBUF,X
04620          STA DIRBUF,Y
04630          INX
04640          INY
04650          CPY #$10
04660          BNE .1
04670 ;
04680          LDA STARTSEC
04690          STA SECTOR
04700          LDA STARTSEC+1
04710          STA SECTOR+1
04720          JSR READSEC
04730 ;
04740          LDA #0
04750          STA SECOFF
04760          JSR GETCOMHEAD
04770          LDA SFLNUM
04780          AND #$FC
04790          STA FILENUM
04800          JMP GETSEG
04810 ------------------------------
04820 LOADDEMO
04830          JSR GETCOMHEAD
04840 ;
04850 GETSEG
04860          JSR GETBYTSEC
04870          PHA
04880          LDA SFLNUM
04890          AND #$FC
04900          CMP FILENUM
04910          BEQ .1
04920          PLA
04930          JMP NEXTDEMO
04940 .1
04950          PLA
04960          LDY #0
04970          STA (ZMEMPTR),Y
04980          LDA ZMEMPTR+1
04990          CMP ENDADR+1
05000          BNE .2
05010          LDA ZMEMPTR
05020          CMP ENDADR
05030          BEQ .4
05040 .2
05050          INC ZMEMPTR
05060          BNE .3
05070          INC ZMEMPTR+1
05080 .3
05090          JMP GETSEG
05100 .4
05110          LDA STARTADR+1
05120          CMP #2
05130          BNE DISPATCH
05140          LDA STARTADR
05150          CMP #$E2
05160          BNE DISPATCH
05170 ;
05180          LDA ZMEMPTR
05190          PHA
05200          LDA ZMEMPTR+1
05210          PHA
05220          JSR JINITAD
05230          PLA
05240          STA ZMEMPTR+1
05250          PLA
05260          STA ZMEMPTR
05270 ;
05280 DISPATCH
05290          LDA DEMOFLG
05300          BNE NEXTDEMO
05310          LDA SFLNUM
05320          AND #3
05330          BNE LOADDEMO
05340          LDA SFLNUM+1
05350          BNE LOADDEMO
05360          LDA SECOFF
05370          CMP SFLNUM+2
05380          BCS NEXTDEMO
05390          INC DEMOFLG
05400          JMP LOADDEMO
05410 ------------------------------
05420 NEXTDEMO
05430          INC DEMOCNT
05440          LDA DEMOCNT
05450          CMP #4
05460          BNE .1
05470          LDA #0
05480          STA DEMOCNT
05490 .1
05500          JMP (RUNAD)
05510 ------------------------------
05520 JINITAD
05530          JMP (INITAD)
05540 ------------------------------
```
  
## Finished Part: Bitmap Depacker for "Maurer Part"  
  
```
01000          .LI OFF
01010 ******************************
01020 *                            *
01030 * PROGRAMM:DEPACK.SRC        *
01040 * AUTOR   :CARSTEN STROTMANN *
01050 * DATUM   :04.02.04          *
01060 * VERSION :2                 *
01070 * FUER    :HT DEMO 2004      *
01080 *                            *
01090 ******************************
01100 ;
01110 ; CIO KONTROLLBLOCK
01120 ;
01130 ICHID    =   $340
01140 ICDNO    =   $341
01150 ICCOM    =   $342
01160 ICSTAT   =   $343
01170 ICBADR   =   $344
01180 ICPUT    =   $346
01190 ICBLEN   =   $348
01200 ICAUX1   =   $34A
01210 ICAUX2   =   $34B
01220 ;
01230 CIOV     =   $E456
01240 ;
01250 ; COMMANDS
01260 ;
01270 COPN     =   3
01280 CCLOSE   =   12
01290 ;
01300 CONSOL   = $D01F
01310 RTCLOK   = $12
01320 ;
01330 MUSICON  = $0701
01340 MUSICOFF = $0708
01350 ;
01360          .OF D:DEPACK.OBJ
01370          .OR $9200
01380 ;
01390 X        JMP S
01400 ------------------------------
01410 CLOSE
01420          LDX #6*$10
01430          LDA #CCLOSE
01440          STA ICCOM,X
01450 ;
01460          JSR CIOV
01470 ;
01480          RTS
01490 ------------------------------
01500 OPEN
01510          LDX #6*$10
01520          LDA #COPN
01530          STA ICCOM,X
01540          LDA #FN
01550          STA ICBADR,X
01560          LDA /FN
01570          STA ICBADR+1,X
01580          LDA #$0
01590          STA ICAUX1,X
01600          LDA #8   ; GR 8
01610          STA ICAUX2,X
01620 ;
01630          JSR CIOV
01640 ;
01650          RTS
01660 ------------------------------
01670 FN       .DA "S:"
01680          .DA #$9B
01690 ------------------------------
01700 WAIT
01710          LDA #0
01720          STA RTCLOK+1
01730 .1       LDA CONSOL
01740          AND #1
01750          BEQ .2
01760          LDA RTCLOK+1
01770          CMP #7
01780          BNE .1
01790 .2       RTS
01800 ------------------------------
01810 SAVMSC   =   $58
01820 CODE     .HX 00
01830 PICPTR   =   $F0
01840 BUFPTR   =   $F2
01850 PICNUM   .HX 00
01860 PICSTRT  =   $F4
01870 PICEND   =   $F6
01880 ;
01890 DEPACK
01900          LDA #0
01910          STA SDMCTL
01920          LDA SAVMSC
01930          STA PICPTR
01940          LDA SAVMSC+1
01950          STA PICPTR+1
01960 ;
01970          LDY PICNUM
01980          LDA PPCDTA,Y
01990          STA PICSTRT+1
02000          LDA PPCDTA+1,Y
02010          STA PICSTRT
02020 ;
02030          INY
02040          INY
02050 ;
02060          LDA PPCDTA,Y
02070          STA BUFPTR+1
02080          LDA PPCDTA+1,Y
02090          STA BUFPTR
02100 ;
02110          INY
02120          INY
02130          STY PICNUM
02140 ;
02150          LDY #0
02160          LDA (PICSTRT),Y
02170          STA CODE
02180 ;
02190 .1
02200          LDA (BUFPTR),Y
02210          CMP CODE
02220          BNE .2
02230 ;
02240          LDA BUFPTR
02250          SEC
02260          SBC #3
02270          STA BUFPTR
02280          BCS .3
02290          DEC BUFPTR+1
02300 ;
02310 .3
02320          LDY #1
02330          LDA (BUFPTR),Y
02340          TAX
02350          INY
02360          LDA (BUFPTR),Y
02370          PHA
02380 ;
02390          LDY #0
02400 .4
02410          PLA
02420          STA (PICPTR),Y
02430          PHA
02440          LDA PICPTR
02450          CLC
02460          ADC #1
02470          STA PICPTR
02480          BCC .5
02490          INC PICPTR+1
02500 .5
02510          DEX
02520          BNE .4
02530 ;
02540          PLA
02550          SEC
02560          BCS .6     ;IMMER
02570 ;
02580 .2
02590          STA (PICPTR),Y
02600          LDA PICPTR
02610          CLC
02620          ADC #1
02630          STA PICPTR
02640          BCC .7
02650          INC PICPTR+1
02660 ;
02670 .7
02680          LDA BUFPTR
02690          SEC
02700          SBC #1
02710          STA BUFPTR
02720          BCS .8
02730          DEC BUFPTR+1
02740 ;
02750 .6
02760 .8
02770          LDA BUFPTR+1
02780          CMP PICSTRT+1
02790          BNE .1
02800          LDA BUFPTR
02810          CMP PICSTRT
02820          BNE .1
02830 ;
02840          LDA #54
02850          STA SDMCTL
02860          RTS
02870 ------------------------------
02880 SDMCTL   =   $22F
02890 SCOLOR0  =   $2C4
02900 SCOLOR1  =   $2C5
02910 SCOLOR2  =   $2C6
02920 SCOLOR4  =   $2C8
02930 ;
02940 S
02950          JSR CLOSE
02960          JSR OPEN
02970          JSR BL_OFF
02980          JSR MUSICON
02990          LDA #$0F
03000          STA SCOLOR2
03010          LDA #0
03020          STA SCOLOR1
03030          STA PICNUM
03040 .1       JSR DEPACK
03050          JSR BL_ON
03060 ;
03070          JSR WAIT
03080          JSR BL_OFF
03090          LDA PICNUM
03100          CMP #40
03110          BNE .1
03120          JSR MUSICOFF
03130          RTS
03140 ------------------------------
03150 PPCDTA
03160          .HX 3206438D ; START
03170          .HX 43944B45 ; BILD 1
03180          .HX 4B4C544C ; BILD 2
03190          .HX 54535DA9 ; BILD 3
03200          .HX 5DB065E1 ; BILD 4
03210          .HX 65E86F07 ; BILD 5
03220          .HX 6F0E7803 ; BILD 6
03230          .HX 780A80EE ; BILD 7
03240          .HX 80F588C1 ; BILD 8
03250          .HX 88C891CA ; BILD 9
03260 ------------------------------
03270 VCOUNT   =   $D40B
03280 WSYNC    =   $D40A
03290 DMACTL   =   $D400
03300 SDLSTL   =   $230
03310 COLOR    =   $D016
03320 VDSLST   =   $200
03330 ;
03340 ;
03350 ;
03360 C1       .HX 00
03370 C2       .HX 00
03380 ;
03390 BL_ON
03400          LDA #61
03410          STA C1
03420          STA C2
03430 .1       JSR BLEND
03440          INC C2
03450          DEC C1
03460          BNE .1
03470          RTS
03480 BL_OFF
03490          LDA #0
03500          STA C1
03510          LDA #122
03520          STA C2
03530 .1
03540          JSR BLEND
03550          INC C1
03560          DEC C2
03570          LDA C2
03580          CMP #62
03590          BNE .1
03600          RTS
03610 ------------------------------
03620 BLEND
03630 .1
03640          LDA VCOUNT
03650          BNE .1
03660          LDA SCOLOR4
03670          LDY #3
03680 .2
03690          STA COLOR,Y
03700          DEY
03710          BPL .2
03720 ;
03730          LDA C1
03740 .3
03750          CMP VCOUNT
03760          BNE .3
03770 ;
03780          LDY #3
03790 .4
03800          LDA SCOLOR0,Y
03810          STA COLOR,Y
03820          DEY
03830          BPL .4
03840 ;
03850          LDA C2
03860 .5
03870          CMP VCOUNT
03880          BNE .5
03890 ;
03900          LDA SCOLOR4
03910          LDY #3
03920 .6
03930          STA COLOR,Y
03940          DEY
03950          BPL .6
03960 ;
03970 ;
03980          RTS
03990 ------------------------------
04000 INIT
04010          .OR $2E2
04020          .DA S
04030 ------------------------------
```
  
## Lose Parts: Blend Effect  
  
```
00120 VCOUNT   =   $D40B
00130 WSYNC    =   $D40A
00140 DMACTL   =   $D400
00150 SDMCTL   =   $22F
00160 SCOLOR   =   $2C4
00170 SDLSTL   =   $230
00180 COLOR    =   $D016
00190 VDSLST   =   $200
00200 ;
00230 ;
00270 ;
00280 C1       .HX 00
00290 C2       .HX 00
00300 ;
00310 BL_ON
00320          LDA #61
00330          STA C1
00340          STA C2
00350 .1       JSR BLEND
00360          INC C2
00370          DEC C1
00380          BNE .1
00390          RTS
00400 BL_OFF
00410          LDA #0
00420          STA C1
00430          LDA #122
00440          STA C2
00450 .1
00460          JSR BLEND
00470          INC C1
00480          DEC C2
00490          LDA C2
00500          CMP #62
00510          BNE .1
00520          RTS
00530 ------------------------------
00540 BLEND
00550 .1
00560          LDA VCOUNT
00570          BNE .1
00580          LDA SCOLOR+4
00590          LDY #3
00600 .2
00620          STA COLOR,Y
00630          DEY
00640          BPL .2
00650 ;
00660          LDA C1
00670 .3
00680          CMP VCOUNT
00690          BNE .3
00700 ;
00710          LDY #3
00720 .4
00730          LDA SCOLOR,Y
00750          STA COLOR,Y
00760          DEY
00770          BPL .4
00780 ;
00790          LDA C2
00800 .5
00810          CMP VCOUNT
00820          BNE .5
00830 ;
00840          LDA SCOLOR+4
00850          LDY #3
00860 .6
00880          STA COLOR,Y
00890          DEY
00900          BPL .6
00910 ;
00920 ;
00930          RTS
00940 ------------------------------
```
  
## Lose Parts: RolDLI  
  
```
00010          .LI OFF
00020 ******************************
00030 *                            *
00040 * PROGRAMM:FARB/FONT DLI     *
00050 * AUTOR   :C.STROTMANN       *
00060 * DATUM   :28.09.91          *
00070 * VERSION :00.01             *
00080 * FUER    :RALF T. QUACK     *
00090 *                            *
00100 ******************************
00110 ;
00120 ; OS REGISTER
00130 ;
00140 PRNBUF   =   $3C0
00150 CASBUF   =   $400
00160 HCOLOR2  =   $D018
00170 CHBAS    =   $D409
00180 WSYNC    =   $D40A
00190 NMIEN    =   $D40E
00200 SETVBV   =   $E45C
00210 XITVBV   =   $E462
00211 SYSVBV   =   $E45F
00220 COLCON   =   $2DD   FARBZAEHLER
00230 VDSLST   =   $200
00240 ;
00250 ;
00260 ;
00270          .OR $0600
00280 ;
00290 ;        .OF D:ROLDLI.COM
00300 ;
00310 ;
00320 START
00330          PLA         BASIC !
00340 MSC      LDA #$40
00350          STA NMIEN INTERRUPT AUS
00360          LDA #DLI
00370          STA VDSLST
00380          LDA /DLI
00390          STA VDSLST+1
00400          LDA #$C0
00410          STA NMIEN
00420          LDY #VBI
00430          LDX /VBI
00440          LDA #6
00450          JSR SETVBV
00460          RTS         => BASIC
00470 ;
00480 ------------------------------
00490 ;
00500 VBI
00510          LDA #0

00520          STA COLCON
00530          JMP SYSVBV
00540 ;
00550 ------------------------------
00560 ;
00570 DLI
00580          PHA
00590          TXA
00600          PHA
00610          LDX COLCON
00620          LDA PRNBUF,X
00630          STA WSYNC
00640          STA HCOLOR2
00650          LDA CASBUF,X
00660          STA CHBAS
00670          INC COLCON
00680          PLA
00690          TAX
00700          PLA
00710          RTI
00720 ;
00730 ------------------------------
00740 ;
```
## Lose Parts: Blend Effect 1  
  
```
00010 ******************************
00020 *                            *
00030 * PROGRAMM:BILDEINBLEND      *
00040 * AUTOR   :C.STROTMANN       *
00050 * DATUM   :16.07.89          *
00060 * VERSION :00.01             *
00070 * FUER    :GAME LORDS        *
00080 *                            *
00090 ******************************
00100 ;
00110 ; OS REGISTER
00120 ;
00130 SAVMSC   =   $58    BILDSCHRIMS
00140 RTCLOK   =   $12    RT-CLOCK
00150 SOURCE   =   $F5    QUELLVEKTOR
00160 DESTIN   =   $F7    ZIELVEKTOR
00170 SOURCE2  =   $F9    QUELLZAHLER
00180 RANDOM   =   $D20A  ZUFALLSZAHL
00190 ;
00200 ;
00210          .OR $0600
00220          .OF "D:BLEND.COM"
00230 ;
00240 START
00250          PLA        BASIC !
00260          PLA        SOURCEADR
00270          STA SOURCE+1
00280          PLA
00290          STA SOURCE
00300          LDA #0
00310          STA ZAEHL
00320 LOOP
00330          LDA SOURCE
00340          STA SOURCE2
00350          LDA SOURCE+1
00360          STA SOURCE2+1
00370          LDA SAVMSC
00380          STA DESTIN
00390          LDA SAVMSC+1
00400          STA DESTIN+1
00410          LDY #0
00420          LDX #0
00430 COPY
00440          LDA (SOURCE2),Y
00450          AND RTCLOK+2
00460          ORA (DESTIN),Y
00470          ORA RANDOM
00480          STA (DESTIN),Y
00490          INY
00500          BNE COPY
00510          INC SOURCE2+1
00520          INC DESTIN+1
00530          INX
00540          CPX #30
00550          BNE COPY
00560          INC ZAEHL
00570          LDA ZAEHL
00580          CMP #50
00590          BNE LOOP
00600          RTS
00610 ;
00620 ZAEHL    .HX 00
```
  
## Lose Parts: Blend Effect 2  
  
```
00010          .LI OFF
00020 ******************************
00030 *                            *
00040 * PROGRAMM:BLENDE            *
00050 * AUTOR   :CARSTEN STROTMANN *
00060 * DATUM   :21.09.91          *
00070 * VERSION :0.1               *
00080 * FUER    :KSHOW             *
00090 *                            *
00100 ******************************
00110 ;
00120 VCOUNT   =   $D40B
00130 WSYNC    =   $D40A
00140 DMACTL   =   $D400
00150 SDMCTL   =   $22F
00160 SCOLOR   =   $2C4
00170 SDLSTL   =   $230
00180 COLOR    =   $D016
00190 VDSLST   =   $200
00200 ;
00210          .OR $0600
00220 ;        .OF D:BLFX.COM
00230 ;
00240 S
00250 BLON     JMP BL_ON
00260 BLOFF    JMP BL_OFF
00270 ;
00280 C1       .HX 00
00290 C2       .HX 00
00300 ;
00310 BL_ON
00320          LDA #61
00330          STA C1
00340          STA C2
00350 .1       JSR BLEND
00360          INC C2
00370          DEC C1
00380          BNE .1
00390          RTS
00400 BL_OFF
00410          LDA #0
00420          STA C1
00430          LDA #122
00440          STA C2
00450 .1
00460          JSR BLEND
00470          INC C1
00480          DEC C2
00490          LDA C2
00500          CMP #62
00510          BNE .1
00520          RTS
00530 ------------------------------
00540 BLEND
00550 .1
00560          LDA VCOUNT
00570          BNE .1
00580          LDA SCOLOR+4
00590          LDY #3
00600 .2
00620          STA COLOR,Y
00630          DEY
00640          BPL .2
00650 ;
00660          LDA C1
00670 .3
00680          CMP VCOUNT
00690          BNE .3
00700 ;
00710          LDY #3
00720 .4
00730          LDA SCOLOR,Y
00750          STA COLOR,Y
00760          DEY
00770          BPL .4
00780 ;
00790          LDA C2
00800 .5
00810          CMP VCOUNT
00820          BNE .5
00830 ;
00840          LDA SCOLOR+4
00850          LDY #3
00860 .6
00880          STA COLOR,Y
00890          DEY
00900          BPL .6
00910 ;
00920 ;
00930          RTS
00940 ------------------------------
00950          .OR $0400
00960 ------------------------------
00970 STARTDL
00980          .HX 807070707070
00990          .HX 707070707070
01000          .HX 7070
01010          .HX 42
01020 TXTADR   .DA STARTTXT
01030          .HX 1002
01040          .HX 41
01050          .DA STARTDL
01060 ------------------------------
01070 STARTTXT
01080          .AT "   Now loading...                       "
01090          .AT "       PhoeniX SoftCrew Slideshow       "
01100 ------------------------------
01110 DLINIT
01120          LDA #STARTDL
01130          STA SDLSTL
01140          LDA /STARTDL
01150          STA SDLSTL+1
01160          LDA #DLI
01170          STA VDSLST
01180          LDA /DLI
01190          STA VDSLST+1
01200          RTS
01210 ------------------------------
01220 DLI
01230          PHA
01240          STA WSYNC
01250          LDA #0
01260          STA COLOR+4
01270          LDA #$10

01280          STA COLOR+2
01290          LDA #15
01300          STA COLOR+1
01310          PLA
01320          RTI
01330 ------------------------------
01340 INIT
01350          .OR $02E2
01360          .DA DLINIT
01370 ------------------------------
```
  
## Lose Parts: Movie Scoller  
  
```
00010          .LI OFF
00020 ***************************
00030 *    ABSPANN FUER FILM    *
00040 *    TEXT AN $7000        *
00050 *    X=USR($5000)         *
00060 ***************************
00070 ;
00080 ;
00090 ;
00100 VSCROL   =   $D405
00110 SCREEN   =   $3000
00120 SVSCROL  =   $0238
00130 SDLSTL   =   $230
00140 RTCLOK   =   $12
00150 SMADR    =   $F5
00160 MMADR    =   $F7
00170 CPADR    =   $F9
00180 ;
00190 ;
00200          .OR $0600
00210 ;        .OF "D:SCROL.COM"
00220 JMPIN    PLA
00230          JMP START
00240 ;
00250 ;
00260 DL       .HX 707070707070
00270          .HX 62
00280 DLADR    .DA SCREEN
00290          .HX 222222222222
00300          .HX 222222222222
00310          .HX 222222222202
00320          .HX 41
00330          .DA DL
00340 ;
00350 ;
00360 ;
00370 START    LDA #0
00380          STA VSCROL
00390          STA SVSCROL
00400          LDA #DL
00410          STA SDLSTL
00420          LDA /DL
00430          STA SDLSTL+1
00440          LDA #$7000
00450          STA SMADR
00460          LDA /$7000
00470          STA SMADR+1
00480 SCROLL   JSR WVSYNC
00490          JSR WVSYNC
00500          INC SVSCROL
00510          LDA SVSCROL
00520          CMP #8
00530          BEQ .2
00540          STA VSCROL
00550          JMP SCROLL
00560 .2
00570          LDA SMADR
00580          CLC
00590          ADC #40
00600          STA SMADR
00610          BCC .3
00620          INC SMADR+1
00630 .3
00640          LDA #0
00650          STA SVSCROL
00660          STA VSCROL
00670          JSR COPY
00680          JMP SCROLL
00690 ;
00700 ------------------------------
00710 ;
00720 WVSYNC   LDA RTCLOK+2
00730 .1       CMP RTCLOK+2
00740          BEQ .1
00750          RTS
00760 ;
00770 ;  UR COPY
00780 ;
00790 COPY
00800          LDA /SCREEN
00810          STA CPADR+1
00820          LDA #SCREEN
00830          STA CPADR
00840          LDA SMADR
00850          STA MMADR
00860          LDA SMADR+1
00870          STA MMADR+1
00880          LDX #03
00890 .1       LDY #0
00900 .2       LDA (MMADR),Y
00910          STA (CPADR),Y
00920          INY
00930          BNE .2
00940          INC MMADR+1
00950          INC CPADR+1
00960          DEX
00970          BNE .1
00980          RTS
00990 ;
01000 ------------------------------
01010 TEXT
01020          .OR $7000
01030          .BL $3C0,0
01040          .AT "0123456789012345678901234567890123456789"
01050          .AT "                  Regie                 "
01070          .AT "                                        "
01080          .AT "                Kamera                  "
01110          .AT "                                        "
01120          .AT "           Studiokamera                 "
01140          .AT "                                        "
01160          .AT "                                        "
01170          .AT "        Technische Leitung              "
01190          .AT "                                        "
01200          .AT "     Technische Unterstuetzung          "
01240          .AT "                                        "
01250          .AT "                Schnitt                 "
01270          .AT "                                        "
01280          .AT "                Ton                     "
01300          .AT "                                        "
01310          .AT "       Bauten/Buehnenbild               "
01330          .AT "                                        "
01340          .AT "       Abspanntechnik                   "
01350          .AT "        PhoeniX SoftCrew                "
01360          .AT "        Multimedia                      "
01480          .AT "                                        "
01490          .AT "               Maske                    "
01510          .AT "                                        "
01520          .AT "             Stunts                     "
01540          .AT "                                        "
01550          .AT "            Wir danken                  "
01610          .AT "                                        "
01620          .AT "             Fortsetzung:               "
01630          .AT "                                        "
01640          .BL 960,0
01650 ------------------------------
```
  
  
  
