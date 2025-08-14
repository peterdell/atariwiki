# Simple Blitter Routine  
  
this is the BETA Version of a simple Blitter Routine for Mirko Sobe (AtariXLE, BOSS X).  
  
Use attached ATR Image. There is a demo Turbo Basic PGM on the Image. The ML-Routine is really simple. All Memory Calculations must be done in Basic or in the programmers brain ;)  
  
To Move Memory from high to low address, use a 16 Bit negative value in the "bytes_per_row_in_frambuffer" parameter. So -40 becomes (40 EXOR $FFFF) + 1 = $FFD8  
  
__USAGE__: {{{x=USR(<addr of mlroutine> , sourceaddr, destaddr, bytes_in_rows, lines, bytes_per_row_in_frambuffer)}}}  
  
where  
- __sourceaddr__ is the Source Address (like DPEEK(88))  
- __destaddr__ is the Destination Address  
- __bytes_in_row__ is the number of bytes in a row to copy  
- __lines__ is the numbers of lines to copy  
- __bytes_per_row_in_framebuffer__ is the number of bytes per line in the framebuffer (40 for Graphics 0 and 8, $FFD8 for negative = -40)  
  
## Disk  
  
- [BLITTR.ATR](attachments/BLITTR.ATR)  
  
## Source (Bibo Assembler)  
  
```
01000             .LI OFF
01010 **********************
01020 **                  **
01030 ** SIMPLE BLITTER   **
01040 ** (C) 2004 CAS     **
01050 ** FOR MIRKO SOBE   **
01060 ** VERSION 1.0      **
01070 **                  **
01080 **********************
01090 ;
01100          .OR $600
01110 ;
01120          .OF "D:BLITTER.COM"
01130 ;
01140 SRCADR   =   $00
01150 DSTADR   =   $06
01160 BASRC    =   $D4
01170 LEN      =   $0400
01180 LINES    =   $0401
01190 LENFB    =   $0402
01200 ;
01210 BASIC    PLA
01220          CMP #5
01230          BEQ CPY
01240 ERROR
01250          LDX #$0
01260          STA BASRC+1
01270          LDX #$80
01280          STA BASRC
01290          RTS
01300 ;
01310 CPY
01320          PLA
01330          STA SRCADR+1
01340          PLA
01350          STA SRCADR
01360          PLA
01370          STA DSTADR+1
01380          PLA
01390          STA DSTADR
01400 ;
01410          PLA
01420          PLA
01430          STA LEN
01440          PLA
01450          PLA
01460          STA LINES
01470          PLA
01480          STA LENFB+1
01490          PLA
01500          STA LENFB
01510 ;
01520 CPYL     LDY LEN
01530          DEY
01540 .1
01550          LDA (SRCADR),Y
01560          STA (DSTADR),Y
01570          DEY
01580          BPL .1
01590 .2
01600          DEC LINES
01610          BEQ END
01620          CLC
01630          LDA SRCADR
01640          ADC LENFB
01650          STA SRCADR
01660          LDA SRCADR+1
01670          ADC LENFB+1
01680          STA SRCADR+1
01690 .3
01700          CLC
01710          LDA DSTADR
01720          ADC LENFB
01730          STA DSTADR
01740          LDA DSTADR+1
01750          ADC LENFB+1
01760          STA DSTADR+1
01770          CLC
01780 .4       BCC CPYL    ; ALWAYS
01790 ;
01800 END
01810          LDA #0
01820          STA BASRC+1
01830          LDA #1
01840          STA BASRC
01850          RTS
01860 ------------------------------

```
  
## Demo Program (Turbo Basic)  
  
```
1010 DIM X$($70)
1020 X$="<mlcode routine>" 
1040 CLS 
1050 ? "BLITTER DEMO"
1060 ? "GR.0"
1070 GET A
1080 GRAPHICS 0
1090 FOR U=1 TO 16
1100   FOR I=1 TO 30:? U;:NEXT I
1110 NEXT U
1120 ? :? " UP..."
1130 FOR U=1 TO 20
1140   X=USR(ADR(X$),DPEEK(88)+40*10+10,DPEEK(88)+40*9+10,10,14,40)
1150 NEXT U
1160 ? :? "<KEY>":GET A
1170 ? " AND DOWN "
1180 FOR U=1 TO 20
1190   X=USR(ADR(X$),DPEEK(88)+40*19+25,DPEEK(88)+40*20+25,10,14,$FFD8)
1200 NEXT U
1210 GET A
1220 GRAPHICS 15
1230 OPEN #1,4,0,"D:MZM.PIC"
1240 BGET #1,DPEEK(88),7680
1250 CLOSE #1
1260 ? "SCROLLUP <KEY>"
1270 GET A
1280 FOR U=1 TO 40
1290   X=USR(ADR(X$),DPEEK(88)+40*10+10,DPEEK(88)+40*9+10,14,40,40)
1300 NEXT U
1310 ? "ZOOM EFFEKT! <KEY>":GET A
1320 FOR U=1 TO 180
1330   X=USR(ADR(X$),DPEEK(88)+20+40,DPEEK(88)+20,10,U,40)
1340 NEXT U
1350 ? " FILL/CLEAR BLOCK"
1360 GET A
1370 X=USR(ADR(X$),DPEEK(88)+14,DPEEK(88)+54,8,192,40)
1380 ? " FILL/CLEAR SCREEN"
1390 GET A
1400 X=USR(ADR(X$),DPEEK(88),DPEEK(88)+40,40,192,40)
1410 ? "<KEY>":GET A
1420 OPEN #1,4,0,"D:MZM.PIC"
1430 BGET #1,DPEEK(88),7680
1440 CLOSE #1
1450 ? "SCROLLDOWN  <KEY>"
1460 GET A
1470 FOR U=1 TO 40
1480   X=USR(ADR(X$),DPEEK(88)+40*129+10,DPEEK(88)+40*130+10,14,40,$FFD8)
1490 NEXT U
1500 ? "ZOOM EFFEKT! <KEY>":GET A
1510 FOR U=1 TO 180
1520   X=USR(ADR(X$),DPEEK(88)+20+179*40,DPEEK(88)+20+180*40,10,U,$FFD8)
1530 NEXT U
```
  
  
  
