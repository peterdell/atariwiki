# Atari COM-File Tracer  
  
  
```
00010 ------------------------------
00020 *  FILE-TRACE ROUTINE V1.0   *
00030 *                            *
00040 *  LAST : 28.01.1988         *
00050 ------------------------------
00060          .LI OFF
00070 ------------------------------
00080 PNT      .EQ $D4
00090 ENDE     .EQ $D6
00100 FLAG     .EQ $CC
00110 ICCOM    .EQ $342
00120 ICBAL    .EQ $344
00130 ICBAH    .EQ $345
00140 ICBLL    .EQ $348
00150 ICBLH    .EQ $349
00160 ICAX1    .EQ $34A
00170 CIOV     .EQ $E456
00180 ------------------------------
00190 START    JSR TEXTOUT
00200          .HX 9B9B9B
00210          .AS "THE FILETRACER:"
00220          .HX 9B
00230          .AS "---------------"
00240          .HX 9B
00250          .AS "FILE>@"
00260          JSR INPUT
00270          LDA FNAME
00280          CMP #$9B
00290          BEQ .2
00300          LDA #':
00310          CMP FNAME+1
00320          BEQ .1
00330          CMP FNAME+2
00340          BEQ .1
00350          LDY #$0C
00360 .0       LDA FNAME,Y
00370          STA FNAME+2,Y
00380          DEY
00390          BPL .0
00400          LDA #'D
00410          STA FNAME
00420          LDA #':
00430          STA FNAME+1
00440 .1       JSR OPEN
00450          JSR TRACE
00460          JSR CLOSE
00470          JMP START
00480 .2       RTS
00490 ------------------------------
00500 TRACE    JSR GET
00510          STA PNT     STARTADR
00520          JSR GET
00530          STA PNT+1
00540          LDA #$FF
00550          CMP PNT
00560          BNE .1
00570          CMP PNT+1
00580          BNE .1
00590          JMP TRACE
00600 .1       JSR GET     ENDADR
00610          STA ENDE
00620          JSR GET
00630          STA ENDE+1
00640 ------------------------------
00650          JSR TEXTOUT
00660          .DA #$9B,"MEM:$@"
00670          LDA PNT
00680          LDX PNT+1
00690          JSR HEX16
00700          JSR TEXTOUT
00710          .DA "-$@"
00720          LDA ENDE
00730          LDX ENDE+1
00740          JSR HEX16
00750          LDA #$20
00760          JSR CHAROUT
00770 ------------------------------
00780          LDA #$00
00790          STA FLAG
00800          LDA PNT+1
00810          CMP #$02
00820          BNE .11
00830          LDA PNT
00840          CMP #$E0
00850          BNE .32
00860          LDA ENDE
00870          CMP #$E3
00880          BCC .31
00890          JSR TEXTOUT
00900          .AS "INIT/@"
00910          LDA #$02
00920          STA FLAG
00930 .31      JSR TEXTOUT
00940          .AS "RUN @"
00950          INC FLAG
00960          INC FLAG
00970          JMP .11
00980 .32      CMP #$E2
00990          BNE .11
01000          JSR TEXTOUT
01010          .AS "INIT@"
01020          LDA #$02
01030          STA FLAG
01040 ------------------------------
01050 .11      LDA PNT+1   WHILE
01060          CMP ENDE+1  P<=E
01070          BNE .12
01080          LDA PNT
01090          CMP ENDE
01100          BEQ .2
01110 .12      BCC .2
01120          JMP TRACE
01130 ------------------------------
01140 .2       JSR GET
01150          INC PNT
01160          BNE .3
01170          INC PNT+1
01180 .3       LDY FLAG
01190          BEQ .4
01200          DEC FLAG
01210          PHA
01220          LDA #$20
01230          JSR CHAROUT
01240          PLA
01250          JSR HEX8
01260 .4       JMP .11
01270 ------------------------------
01280 OPEN     JSR CLOSE
01290          LDA #FNAME
01300          STA ICBAL,X DEV LO
01310          LDA /FNAME
01320          STA ICBAH,X DEV HI
01330          LDA #$03
01340          STA ICCOM,X
01350          LDA #$04
01360          STA ICAX1,X
01370          JSR CIOV
01380          BPL .1
01390          JMP ERROR
01400 .1       RTS
01410 ------------------------------
01420 INPUT    LDA #16
01430          LDX #$00    KANAL # 0
01440          LDY #$05
01450          BPL BGET
01460 ------------------------------
01470 GET      LDA #$00
01480          LDX #$20    KANAL # 1
01490          LDY #$07
01500 ------------------------------
01510 BGET     STA ICBLL,X
01520          LDA #$00
01530          STA ICBLH,X
01540          LDA #FNAME
01550          STA ICBAL,X
01560          LDA /FNAME
01570          STA ICBAH,X
01580          TYA
01590          STA ICCOM,X
01600          JSR CIOV
01610          BPL .1
01620          TYA
01630          PHA
01640          JSR CLOSE
01650          PLA
01660          TAY
01670          CPY #$88
01680          BNE .0
01690          PLA
01700          PLA
01710          RTS
01720 .0       JMP ERROR
01730 .1       RTS
01740 ------------------------------
01750 CLOSE    LDX #$20
01760          LDA #$0C
01770          STA ICCOM,X
01780          JMP CIOV
01790 ------------------------------
01800 * HEX16:
01810 * <A> Register:LO-Byte der Zahl
01820 * <X> Register:HI-Byte der Zahl
01830 ------------------------------
01840 *
01850 HEX16    PHA
01860          TXA
01870          JSR HEX8
01880          PLA
01890 *
01900 HEX8     PHA
01910          LSR
01920          LSR
01930          LSR
01940          LSR
01950          JSR HEX
01960          PLA
01970          AND #$F
01980 *
01990 HEX      CMP #10
02000          BCC .1
02010          CLC
02020          ADC #7
02030 .1       ADC #$30
02040          JMP CHAROUT
02050 ------------------------------
02060 * Textausgeberoutine ueber   *
02070 * Stack. Routine muss mit    *
02080 * JSR aufgerufen werden. Der *
02090 * Text folgt direkt im An-   *
02100 * schluss an das JSR-State-  *
02110 * ment. Der Text muss mit    *
02120 * einer Ende-Kennung (hier   *
02130 * das @-Zeichen) enden. Das  *
02140 * Programm wird ab Textende  *
02150 * fortgefuehrt.              *
02160 ------------------------------
02170 TEXTOUT  PLA
02180          STA $D0
02190          PLA
02200          STA $D1
02210 ------------------------------
02220 .0       INC $D0
02230          BNE .1
02240          INC $D1
02250 .1       LDX #0
02260          LDA ($D0,X)
02270          CMP #'@
02280          BEQ .2
02290          JSR CHAROUT
02300          JMP .0
02310 *
02320 .2       LDA $D1
02330          PHA
02340          LDA $D0
02350          PHA
02360          RTS
02370 ------------------------------
02380 CHAROUT  TAX
02390          LDA $E407
02400          PHA
02410          LDA $E406
02420          PHA
02430          TXA
02440          RTS
02450 ------------------------------
02460 ERROR    PLA         POP
02470          PLA
02480          TYA
02490          PHA
02500          JSR TEXTOUT
02510          .HX 9B9B
02520          .AS "˝ERROR #$@"
02530          PLA
02540          JSR HEX8
02550          LDA #$9B
02560          JSR CHAROUT
02570          JMP START
02580 ------------------------------
02590 FNAME    .AS "D1:12345678.123"
02600 ------------------------------
02610          .OR $2E0
02620          .DA START
```
