# Small DOS 2.5 COM-File loader for Demo  
  
reverse engineered from ABBUC Hobbytronic Demo 1992, done by Benji-Soft (Juergen Schildmann und Stefan Duesterhoeft), maybe based on prior work from Peter Sabbath.  
  
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
  
