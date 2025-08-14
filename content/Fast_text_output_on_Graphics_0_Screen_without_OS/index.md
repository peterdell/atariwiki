# Fast text output on Graphics 0 Screen without OS  
  
General Information  
  
Author: Erwin Reuss, Compy Shop   
Assembler: Bibo Assembler   
Published: CSM 3/89   
  
```
00010          .LI OFF
00020 ------------------------------
00030 * Fast Textoutput on         *
00040 * GRAFICS 0 Screen           *
00050 * (P) E.REUSS   CSM 3/89     *
00060 ------------------------------
00140 RETOUT   LDA #$9B
00150 *
00160 CHROUT   STY STOY
00170          STX STOX
00180          JSR CHOUT
00190 .1       LDA $11
00200          BEQ BREAK
00210          LDA $2FF
00220          BMI .1
00230          LDY STOY
00240          LDX STOX
00250          RTS
00260 ;
00270 BREAK    LDA #$80
00280          STA $11
00290          JSR RETOUT
00300          LDX #$FF
00310          STX $2FC
00320 ;>>>>    JMP ...   insert own
00330 ;                  ERROR-
00340 ;                      ROUTINE here
00350 *
00360 STOX     .HX 00
00370 STOY     .HX 00
00380 ------------------------------
00390 EOUT     TAX
00400          LDA $E407
00410          PHA
00420          LDA $E406
00430          PHA
00440          TXA
00450          RTS
00460 ------------------------------
00470 CHOUT    STA $2FB
00480          LDA $2F0
00490          BNE .1
00500          LDA $5D
00510          LDY #0
00520          STA ($5E),Y
00530 .1       JSR CUR1
00540          LDA $2FB
00550          JSR CHR1
00560          LDA $5E
00570          CLC
00580          ADC $55
00590          STA $5E
00600          BCC .2
00610          INC $5F
00620 .2       LDY #0
00630          LDA ($5E),Y
00640          STA $5D
00650          LDX $2F0
00660          BNE .3
00670          EOR #$80
00680 .3       STA ($5E),Y
00690          RTS
00700 ------------------------------
00710 BELL     LDA #$FD
00720          JMP EOUT
00730 ------------------------------
00740 ESCAPE   LDA #1
00750          STA $2FE
00760          RTS
00770 ------------------------------
00780 CHR1     LDX $2FE
00790          BNE CHR2
00800          CMP #$FD
00810          BEQ BELL
00820          CMP #$9B
00830          BEQ NEWLIN
00840          CMP #$1B
00850          BCC CHR2
00860          CMP #$20
00870          BCS CHR2
00880          TAY
00890          LDA TABHI-$1B,Y
00900          PHA
00910          LDA TABLO-$1B,Y
00920          PHA
00930          RTS
00940 *
00950 CHR2     LSR $2FE
00960          STA $70
00970          ASL
00980          ASL
00990          ROL
01000          ROL
01010          AND #3
01020          TAY
01030          LDA TABL1,Y
01040          EOR $70
01050          LDY $55
01060          STA ($5E),Y
01070          INC $55
01080          LDA $55
01090          CMP #$28
01100          BCS NEWLIN
01110          RTS
01120 *
01130 NEWLIN   LDA $52
01140          STA $55
01150 CDOWN    INC $54
01160          LDA $54
01170          CMP #$18
01180          BCC CURPOS
01190          DEC $54
01200          LDA #0
01210          PHA
01220          JSR CURPOS
01230 NLA      LDA $5E
01240          STA $66
01250          LDA $5F
01260          STA $67
01270          LDY #$27
01280          PLA
01290          CLC
01300          ADC #1
01310          CMP #$18
01320          BCS NL1
01330          PHA
01340          JSR CURPOS
01350 NL0      LDA ($5E),Y
01360          STA ($66),Y
01370          DEY
01380          BPL NL0
01390          BMI NLA
01400 NL1      JSR CUR1
01410          LDY $55
01420 POKCHR   LDA #0
01430 .1       STA ($5E),Y
01440          INY
01450          CPY #$28
01460          BCC .1
01470 CLRET    RTS
01480 ------------------------------
01490 CLEFT    DEC $55
01500          LDA $55
01510          CMP $52
01520          BCS CLRET
01530          LDA #$27
01540          STA $55
01550          RTS
01560 ------------------------------
01570 CRIGH    INC $55
01580          LDA $55
01590          CMP #$28
01600          BCC CLRET
01610          LDA $52
01620          STA $55
01630          RTS
01640 ------------------------------
01650 CURUP    LDA $54
01660          BNE CUP1
01670          LDA #$18
01680          STA $54
01690 CUP1     DEC $54
01700 CUR1     LDA $54
01710 CURPOS   STA $5E
01720          ASL
01730          ASL
01740          ADC $5E
01750          PHA
01760          LSR
01770          LSR
01780          LSR
01790          LSR
01800          LSR
01810          STA $5F
01820          PLA
01830          ASL
01840          ASL
01850          ASL
01860          CLC
01870          ADC $58
01880          STA $5E
01890          LDA $5F
01900          ADC $59
01910          STA $5F
01920          RTS
01930 ------------------------------
01940 TABL1    .HX 40206000
01950 ------------------------------
01960 TABLO    .DA #ESCAPE-1 (ESC)
01970          .DA #CURUP-1  (UP)
01980          .DA #CDOWN-1  (DOWN)
01990          .DA #CLEFT-1  (LEFT)
02000          .DA #CRIGH-1  (RIGHT)
02010 TABHI    .DA /ESCAPE-1 (ESC)
02020          .DA /CURUP-1  (UP)
02030          .DA /CDOWN-1  (DOWN)
02040          .DA /CLEFT-1  (LEFT)
02050          .DA /CRIGH-1  (RIGHT)
02060 ------------------------------
```
