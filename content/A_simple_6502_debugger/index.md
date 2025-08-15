---
title: A simple 6502 debugger
---
# PSC Simple Debugger  
  
  
[atari000.png](attachments/atari000.png)  
  
This is a very simple debugger I have written years ago. It has been used to figure out the hotspots of a program or to slow down the program to be examined.  
  
The "BUG.COM" executable will install a VBI with a wait loop. This loop is slowing down the Atari and thus other programs running. It can be adjusted with "START" and "SELECT". In the top line the tool will display the current CPU instruction pointer. This instruction pointer can be copied to the field on the right with the "OPTION" key (e.g. to examine a specific code area with a hardware monitor such as BiboMon, QMeg or Turbo-Freezer).  
  
### Disk  
  
[sbug6502.atr](attachments/sbug6502.atr)  
  
### Source  
  
- [BUG.SRC.pdf](attachments/BUG.SRC.pdf)  
  
```
00010          .LI OFF
00020 ***************************
00030 * PSC DEBUGGER V.1        *
00040 ***************************
00050 ;
00060 CASINI   =   $02
00070 BOOT     =   $09
00080 CONSOL   =   $D01F
00090 SDLST    =   $0230
00100 HLPFLG   =   $2DC
00110 VCOUNT   =   $D40B
00111 BZAHL    =   $238
00120 ;
00130 ; OS ADRESSEN
00140 ;
00150 SETVBV   =   $E45C
00160 XITVBV   =   $E462
00170 ;
00180 ;
00190          .OF "D:BUG.COM"
00200          .OR $400
00210 ;
00220 HLPMEM   .HX 000000000000
00240 DL       .HX 707042
00250          .DA TEXT
00260          .HX 0001
00270 DLEND    .HX 0000
00280 TEXT     .AT "\240–”√≠¬’«¸¡√‘\240®∞∞∞∞∞©Ωæ®∞∞∞∞∞©¸ƒ≈Ã®∞∞∞∞∞©"
00290 DECLO    .HX 10E8640A
00300 DECHI    .HX 27030000
00310 ZIFFER   .AT "00000"
00320 DELAY    .HX 77
00330 ;
00340 ;
00350 ;
00360 ;
00370 X
00380          LDA #X
00390          STA CASINI
00400          LDA /X
00410          STA CASINI+1
00420 ;
00430          LDA BOOT
00440          ORA #$02
00450          STA BOOT
00460 ;
00470          LDA #$04
00480          BIT CONSOL
00490          BNE SETVBI
00500          RTS
00510 ;
00520 SETVBI
00530          LDY #START
00540          LDX /START
00550          LDA #$07
00560          JSR SETVBV
00570          RTS
00580 ;
00590          .OR $0600
00600 ;
00610 START    LDA SDLST+1
00620          CMP /DL
00630          BEQ BUG
00640          LDA SDLST
00650          CLC
00660          ADC #$03
00670          STA DLEND
00680          LDA SDLST+1
00690          ADC #$00
00700          STA DLEND+1
00710          LDA #DL
00720          STA SDLST
00730          LDA /DL
00740          STA SDLST+1
00750 ;
00760 BUG
00770          LDX #6
00780 .1       PLA
00790          STA HLPMEM-1,X
00800          DEX
00810          BNE .1
00820          LDX HLPMEM+1
00830          LDA HLPMEM
00840          JSR BINDEZ
00850 ;
00860 XDSPL
00870          LDX #5
00880          LDY #$12
00890          JSR DSPL2
00900 ;
00910          LDA CONSOL
00920          CMP #6
00930          BNE RESTORE
00940          LDX #5
00950          LDY #$1B
00960          JSR DSPL2
00970 ;
00980 RESTORE
00990 ;
01000          LDX #0
01010 .1       LDA HLPMEM,X
01020          PHA
01030          INX
01040          CPX #6
01050          BNE .1
01060          LDA DELAY
01070          LDX #0
01080          JSR BINDEZ
01090          LDX #5
01100          LDY #$26
01110          JSR DSPL2
01120 DELMIN
01130          LDA CONSOL
01140          CMP #5
01150          BNE DELPL
01160          LDA DELAY
01170          CMP #$10
01180          BMI DELPL
01190          DEC DELAY
01200 DELPL
01210          LDA CONSOL
01220          CMP #3
01230          BNE WAIT
01240          LDA DELAY
01250          CMP #$7B
01260          BPL WAIT
01270          INC DELAY
01280 WAIT
01290          LDA DELAY
01300 .1       CMP VCOUNT
01310          BNE WAIT
01320          JMP XITVBV
01330 ------------------------------
01340 BINDEZ
01350          STA BZAHL
01360          STX BZAHL+1
01370          LDX #4
01380 VORBES
01390          LDA #$10
01400          STA ZIFFER,X
01410          DEX
01420          BPL VORBES
01430          LDX #0
01440 STELLE
01450          LDA BZAHL+1
01460          CMP DECHI,X
01470          BNE TSTHI
01480          LDA BZAHL
01490          CMP DECLO,X
01500 TSTHI
01510          BCC KLEINER
01520          SEC
01530          LDA BZAHL
01540          SBC DECLO,X
01550          STA BZAHL
01560          LDA BZAHL+1
01570          SBC DECHI,X
01580          STA BZAHL+1
01590          INC ZIFFER,X
01600          JMP STELLE
01610 KLEINER
01620          INX
01630          CPX #4
01640          BNE STELLE
01650          CLC
01660          LDA BZAHL
01670          ADC ZIFFER+4
01680          STA ZIFFER+4
01690          RTS
01700 ------------------------------
01710 DSPL2
01720          LDA ZIFFER-1,X
01730          ORA #$80
01740          STA TEXT,Y
01750          DEY
01760          DEX
01770          BNE DSPL2
01780          RTS
01790 ------------------------------
01800          .OR $2E0
01810          .DA X
01820 ------------------------------

```
