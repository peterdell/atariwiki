---
title: ProForth
---
# ProForth for the Apple II (6502 Source, could be adapted to the Atari 8bit)  
  
NAME: EDASM macro used by FDICT.S  
```
 DFB &1
 DCI &2
 IFEQ >*+3
 LST ON
 FAIL 2,'PFA=xxFF'
 FIN
```
  
fdict.s  
```
          LST OFF,NOGen,NOWarn,NOVsym,NOAsym,NOExp
          MACLIB
          ORG $800
SSIZE     EQU 1024
NBUF      EQU 2
BMAG      EQU SSIZE+4*NBUF
BOS       EQU $60
TOS       EQU $DE
N         EQU TOS+8
IP        EQU N+8
W         EQU IP+3
UP        EQU W+2
XSAVE     EQU UP+2
KSWL      EQU $38
TIBX      EQU $0300
MEM       EQU $BF00
UAREA     EQU MEM-128
DAREA     EQU UAREA-BMAG
MLI       EQU $BF00
OUTCH     EQU $FDED
INCH      EQU $FD0C
CROUT     EQU $FD8E
MONITOR   EQU $FF69
ORIG      EQU *
ENTER     JMP COLD+2
          NOP  
REENTER   JMP WARM
          NOP
          DW $0004
          DW $5ED2
          DW NTOP Last NFA
          DW 8 Backspace key
          DW UAREA User start 
          DW TOS Program TOS
          DW $1FF Return TOS
          DW TIBX Terminal input buffer
          DW 31 Name field size max
          DW 1 Warning
          DW TOP FENCE
          DW TOP DP
          DW VLO VOC-LINK
          DW 0
L22       NAME $83,'LIT'
          DW 00
LIT       DW *+2
          LDA (IP),Y
          PHA
          INC IP
          BNE L30
          INC IP+1
L30       LDA (IP),Y
L31       INC IP
          BNE PUSH
          INC IP+1
PUSH      DEX
          DEX
PUT       STA 1,X
          PLA
          STA 0,X
NEXT      LDY #1
          LDA (IP),Y
          STA W+1
          DEY
          LDA (IP),Y
          STA W
          CLC
          LDA IP
          ADC #2
          STA IP
          BCC L54
          INC IP+1
L54       JMP W-1
*
L35       NAME $84,'CLIT'
          DW L22
CLIT      DW *+2
          LDA (IP),Y
          PHA
          TYA
          BEQ L31
SETUP     ASL A
          STA N-1
L63       LDA 0,X
          STA N,Y
          INX
          INY
          CPY N-1
          BNE L63
          LDY #0
          RTS
L75       NAME $87,'EXECUTE'
          DW L35
EXEC      DW *+2
          LDA 0,X
          STA W
          LDA 1,X
          STA W+1
          INX
          INX
          JMP W-1
L89       NAME $86,'BRANCH'
          DW L75
BRAN      DW *+2
          CLC
          LDA (IP),Y
          ADC IP
          PHA
          INY
          LDA (IP),Y
          ADC IP+1
          STA IP+1
          PLA
          STA IP
          JMP NEXT+2
L107      NAME $87,'0BRANCH'
          DW L89
ZBRAN     DW *+2
          INX
          INX
          LDA $FE,X
          ORA $FF,X
          BEQ BRAN+2
BUMP      CLC
          LDA IP
          ADC #2
          STA IP
          BCC L122
          INC IP+1
L122      JMP NEXT
L127      NAME $86,'(LOOP)'
          DW L107
PLOOP     DW L130
L130      STX XSAVE
          TSX
          INC $101,X
          BNE PL1
          INC $102,X
PL1       CLC
          LDA $103,X
          SBC $101,X
          LDA $104,X
          SBC $102,X
PL2       LDX XSAVE
          ASL A
          BCC BRAN+2
          PLA
          PLA
          PLA
          PLA
          JMP BUMP
L154      NAME $87,'(+LOOP)'
          DW L127
PPLOO     DW *+2
          INX
          INX
          STX XSAVE
          LDA $FF,X
          PHA
          PHA
          LDA $FE,X
          TSX
          INX
          INX
          CLC
          ADC $101,X
          STA $101,X
          PLA
          ADC $102,X
          STA $102,X
          PLA
          BPL PL1
          CLC
          LDA $101,X
          SBC $103,X
          LDA $102,X
          SBC $104,X
          JMP PL2
L185      NAME $84,'(DO)'
          DW L154
PDO       DW *+2
          LDA 3,X
          PHA
          LDA 2,X
          PHA
          LDA 1,X
          PHA
          LDA 0,X
          PHA
POPTWO    INX
          INX
POP       INX
          INX
          JMP NEXT
L207      NAME $81,'I'
          DW L185
I         DW R+2
L214      NAME $85,'DIGIT'
          DW L207
DIGIT     DW *+2
          SEC
          LDA 2,X
          SBC #$30
          BMI L234
          CMP #$A
          BMI L227
          SEC
          SBC #7
          CMP #$A
          BMI L234
L227      CMP 0,X
          BPL L234
          STA 2,X
          LDA #1
          PHA
          TYA
          JMP PUT
L234      TYA
          PHA
          INX
          INX
          JMP PUT
L243      NAME $86,'(FIND)'
          DW L214
PFIND     DW *+2
          LDA #2
          JSR SETUP
          STX XSAVE
L249      LDY #0
          LDA (N),Y
          EOR (N+2),Y
          AND #$3F
          BNE L281
L254      INY
          LDA (N),Y
          EOR (N+2),Y
          ASL A
          BNE L280
          BCC L254
          LDX XSAVE
          DEX
          DEX
          DEX
          DEX
          CLC
          TYA
          ADC #5
          ADC N
          STA 2,X
          LDY #0
          TYA
          ADC N+1
          STA 3,X
          STY 1,X
          LDA (N),Y
          STA 0,X
          LDA #1
          PHA
          JMP PUSH
L280      BCS L284
L281      INY
          LDA (N),Y
          BPL L281
L284      INY
          LDA (N),Y
          TAX
          INY
          LDA (N),Y
          STA N+1
          STX N
          ORA N
          BNE L249
          LDX XSAVE
          LDA #0
          PHA
          JMP PUSH
L301      NAME $87,'ENCLOSE'
          DW L243
ENCL      DW *+2
          LDA #2
          JSR SETUP
          TXA
          SEC
          SBC #8
          TAX
          STY 3,X
          STY 1,X
          DEY
          DEC N+3
          DEC 1,X
L313      INY
          BNE LX1
          INC N+3
          INC 1,X
LX1       LDA (N+2),Y
          CMP N
          BEQ L313
          STY 4,X
          LDA 1,X
          STA 5,X
L318      LDA (N+2),Y
          BNE L327
          STY 2,X
          STY 0,X
          LDA 1,X
          STA 3,X
          TYA
          CMP 4,X
          BNE L326
          LDA 1,X
          CMP 5,X
          BNE L326
          INC 2,X
          BNE L326
          INC 3,X
L326      JMP NEXT
L327      PHA
          STY 2,X
          LDA 1,X
          STA 3,X
          INY
          BNE LX2
          INC 1,X
          INC N+3
LX2       PLA
          CMP N
          BNE L318
          STY 0,X
          JMP NEXT
L337      NAME $84,'EMIT'
          DW L301
EMIT      DW XEMIT
L344      NAME $83,'KEY'
          DW L337
KEY       DW XKEY
L351      NAME $89,'?TERMINAL'
          DW L344
QTERM     DW XQTER
L358      NAME $82,'CR'
          DW L351
CR        DW XCR
L365      NAME $85,'CMOVE'
          DW L358
CMOVE     DW *+2
          LDA #3
          JSR SETUP
L370      CPY N
          BNE L375
          DEC N+1
          BPL L375
          JMP NEXT
L375      LDA (N+4),Y
          STA (N+2),Y
          INY
          BNE L370
          INC N+5
          INC N+3
          JMP L370
L386      NAME $82,'U*'
          DW L365
USTAR     DW *+2
          LDA 2,X
          STA N
          STY 2,X
          LDA 3,X
          STA N+1
          STY 3,X
          LDY #16
L396      ASL 2,X
          ROL 3,X
          ROL 0,X
          ROL 1,X
          BCC L411
          CLC
          LDA N
          ADC 2,X
          STA 2,X
          LDA N+1
          ADC 3,X
          STA 3,X
          LDA #0
          ADC 0,X
          STA 0,X
L411      DEY
          BNE L396
          JMP NEXT
L418      NAME $82,'U/'
          DW L386
USLAS     DW *+2
          LDA 4,X
          LDY 2,X
          STY 4,X
          ASL A
          STA 2,X
          LDA 5,X
          LDY 3,X
          STY 5,X
          ROL A
          STA 3,X
          LDA #16
          STA N
L433      ROL 4,X
          ROL 5,X
          SEC
          LDA 4,X
          SBC 0,X
          TAY
          LDA 5,X
          SBC 1,X
          BCC L444
          STY 4,X
          STA 5,X
L444      ROL 2,X
          ROL 3,X
          DEC N
          BNE L433
          JMP POP
L453      NAME $83,'AND'
          DW L418
ANDD      DW *+2
          LDA 0,X
          AND 2,X
          PHA
          LDA 1,X
          AND 3,X
BINARY    INX
          INX
          JMP PUT
L469      NAME $82,'OR'
          DW L453
OR        DW *+2
          LDA 0,X
          ORA 2,X
          PHA
          LDA 1,X
          ORA 3,X
          INX
          INX
          JMP PUT
L484      NAME $83,'XOR'
          DW L469
XOR       DW *+2
          LDA 0,X
          EOR 2,X
          PHA
          LDA 1,X
          EOR 3,X
          INX
          INX
          JMP PUT
L499      NAME $83,'SP@'
          DW L484
SPAT      DW *+2
          TXA
PUSHOA    PHA
          LDA #0
          JMP PUSH
L511      NAME $83,'SP!'
          DW L499
SPSTO     DW *+2
          LDY #6
          LDA (UP),Y
          TAX
          JMP NEXT
L522      NAME $83,'RP!'
          DW L511
RPSTO     DW *+2
          STX XSAVE
          LDY #8
          LDA (UP),Y
          TAX
          TXS
          LDX XSAVE
          JMP NEXT
L536      NAME $82,'     ;S'
          DW L522
SEMIS     DW *+2
          PLA
          STA IP
          PLA
          STA IP+1
          JMP NEXT
L548      NAME $85,'LEAVE'
          DW L536
LEAVE     DW *+2
          STX XSAVE
          TSX
          LDA $101,X
          STA $103,X
          LDA $102,X
          STA $104,X
          LDX XSAVE
          JMP NEXT
L563      NAME $82,'>R'
          DW L548
TOR       DW *+2
          LDA 1,X
          PHA
          LDA 0,X
          PHA
          INX
          INX
          JMP NEXT
L577      NAME $82,'R>'
          DW L563
RFROM     DW *+2
          DEX
          DEX
          PLA
          STA 0,X
          PLA
          STA 1,X
          JMP NEXT
L591      NAME $81,'R'
          DW L577
R         DW *+2
          STX XSAVE
          TSX
          LDA $101,X
          PHA
          LDA $102,X
          LDX XSAVE
          JMP PUSH
L605      NAME $82,'0='
          DW L591
ZEQU      DW *+2
          LDA 0,X
          ORA 1,X
          STY 1,X
          BNE L613
          INY
L613      STY 0,X
          JMP NEXT
L619      NAME $82,'0<'
          DW L605
ZLESS     DW *+2
          ASL 1,X
          TYA
          ROL A
          STY 1,X
          STA 0,X
          JMP NEXT
          DW 0
L632      NAME $81,'+'
          DW L619
PLUS      DW *+2
          CLC
          LDA 0,X
          ADC 2,X
          STA 2,X
          LDA 1,X
          ADC 3,X
          STA 3,X
          INX
          INX
          JMP NEXT
L649      NAME $82,'D+'
          DW L632
DPLUS     DW *+2
          CLC
          LDA 2,X
          ADC 6,X
          STA 6,X
          LDA 3,X
          ADC 7,X
          STA 7,X
          LDA 0,X
          ADC 4,X
          STA 4,X
          LDA 1,X
          ADC 5,X
          STA 5,X
          JMP POPTWO
L670      NAME $85,'MINUS'
          DW L649
MINUS     DW *+2
          SEC
          TYA
          SBC 0,X
          STA 0,X
          TYA
          SBC 1,X
          STA 1,X
          JMP NEXT
L685      NAME $86,'DMINUS'
          DW L670
DMINU     DW *+2
          SEC
          TYA
          SBC 2,X
          STA 2,X
          TYA
          SBC 3,X
          STA 3,X
          JMP MINUS+3
L700      NAME $84,'OVER'
          DW L685
OVER      DW *+2
          LDA 2,X
          PHA
          LDA 3,X
          JMP PUSH
L711      NAME $84,'DROP'
          DW L700
DROP      DW POP
L718      NAME $84,'SWAP'
          DW L711
SWAP      DW *+2
          LDA 2,X
          PHA
          LDA 0,X
          STA 2,X
          LDA 3,X
          LDY 1,X
          STY 3,X
          JMP PUT
L733      NAME $83,'DUP'
          DW L718
DUP       DW *+2
          LDA 0,X
          PHA
          LDA 1,X
          JMP PUSH
L744      NAME $82,'+!'
          DW L733
PSTOR     DW *+2
          CLC
          LDA (0,X)
          ADC 2,X
          STA (0,X)
          INC 0,X
          BNE L754
          INC 1,X
L754      LDA (0,X)
          ADC 3,X
          STA (0,X)
          JMP POPTWO
L762      NAME $86,'TOGGLE'
          DW L744
TOGGL     DW *+2
          LDA (2,X)
          EOR 0,X
          STA (2,X)
          JMP POPTWO
L773      NAME $81,'@'
          DW L762
AT        DW *+2
          LDA (0,X)
          PHA
          INC 0,X
          BNE L781
          INC 1,X
L781      LDA (0,X)
          JMP PUT
L787      NAME $82,'C@'
          DW L773
CAT       DW *+2
          LDA (0,X)
          STA 0,X
          STY 1,X
          JMP NEXT
L798      NAME $81,'!'
          DW L787
STORE     DW *+2
          LDA 2,X
          STA (0,X)
          INC 0,X
          BNE L806
          INC 1,X
L806      LDA 3,X
          STA (0,X)
          JMP POPTWO
L813      NAME $82,'C!'
          DW L798
CSTOR     DW *+2
          LDA 2,X
          STA (0,X)
          JMP POPTWO
L823      NAME $C1,':'
          DW L813
COLON     DW DOCOL
          DW QEXEC
          DW SCSP
          DW CURR
          DW AT
          DW CON
          DW STORE
          DW CREAT
          DW RBRAC
          DW PSCOD
DOCOL     LDA IP+1
          PHA
          LDA IP
          PHA
          CLC
          LDA W
          ADC #2
          STA IP
          TYA
          ADC W+1
          STA IP+1
          JMP NEXT
L853      NAME $C1,'     ;'
          DW L823
          DW DOCOL
          DW QCSP
          DW COMP
          DW SEMIS
          DW SMUDG
          DW LBRAC
          DW SEMIS
L867      NAME $88,'CONSTANT'
          DW L853
CONST     DW DOCOL
          DW CREAT
          DW SMUDG
          DW COMMA
          DW PSCOD
DOCON     LDY #2
          LDA (W),Y
          PHA
          INY
          LDA (W),Y
          JMP PUSH
L885      NAME $88,'VARIABLE'
          DW L867
VAR       DW DOCOL
          DW CONST
          DW PSCOD
DOVAR     CLC
          LDA W
          ADC #2
          PHA
          TYA
          ADC W+1
          JMP PUSH
L902      NAME $84,'USER'
          DW L885
USER      DW DOCOL
          DW CONST
          DW PSCOD
DOUSE     LDY #2
          CLC
          LDA (W),Y
          ADC UP
          PHA
          LDA #0
          ADC UP+1
          JMP PUSH
L920      NAME $81,'0'
          DW L902
ZERO      DW DOCON
          DW 0
L928      NAME $81,'1'
          DW L920
ONE       DW DOCON
          DW 1
L936      NAME $81,'2'
          DW L928
TWO       DW DOCON
          DW 2
L944      NAME $81,'3'
          DW L936
THREE     DW DOCON
          DW 3
L952      NAME $82,'BL'
          DW L944
BL        DW DOCON
          DW $20
L960      NAME $83,'C/L'
          DW L952
CSLL      DW DOCON
          DW 64
L968      NAME $85,'FIRST'
          DW L960
FIRST     DW DOCON
          DW DAREA
L976      NAME $85,'LIMIT'
          DW L968
LIMIT     DW DOCON
          DW UAREA
L984      NAME $85,'B/BUF'
          DW L976
BBUF      DW DOCON
          DW SSIZE
L992      NAME $85,'B/SCR'
          DW L984
BSCR      DW DOCON
          DW 1024/SSIZE
L993      NAME $85,'FSIZE'
          DW L992
FSIZE     DW DOCON
          DW 100
L1000     NAME $87,'+ORIGIN'
          DW L993
PORIG     DW DOCOL
          DW LIT,ORIG
          DW PLUS
          DW SEMIS
L1010     NAME $83,'TIB'
          DW L1000
TIB       DW DOUSE
          DFB $A
L1018     NAME $85,'WIDTH'
          DW L1010
WIDTH     DW DOUSE
                         ;
          DFB $C
L1026     NAME $87,'WARNING'
          DW L1018
WARN      DW DOUSE
          DFB $E
L1034     NAME $85,'FENCE'
          DW L1026
FENCE     DW DOUSE
          DFB $10
L1042     NAME $82,'DP'
          DW L1034
DP        DW DOUSE
          DFB $12
L1050     NAME $88,'VOC-LINK'
          DW L1042
VOCL      DW DOUSE
          DFB $14
L1058     NAME $83,'BLK'
          DW L1050
BLK       DW DOUSE
          DFB $16
L1066     NAME $82,'IN'
          DW L1058
IN        DW DOUSE
          DFB $18
L1074     NAME $83,'OUT'
          DW L1066
OUT       DW DOUSE
          DFB $1A
L1082     NAME $83,'SCR'
          DW L1074
SCR       DW DOUSE
          DFB $1C
L1090     NAME $86,'OFFSET'
          DW L1082
OFSET     DW DOUSE
          DFB $1E
L1098     NAME $87,'CONTEXT'
          DW L1090
CON       DW DOUSE
          DFB $20
L1106     NAME $87,'CURRENT'
          DW L1098
CURR      DW DOUSE
          DFB $22
L1114     NAME $85,'STATE'
          DW L1106
STATE     DW DOUSE
          DFB $24
L1122     NAME $84,'BASE'
          DW L1114
BASE      DW DOUSE
          DFB $26
L1130     NAME $83,'DPL'
          DW L1122
DPL       DW DOUSE
          DFB $28
L1138     NAME $83,'FLD'
          DW L1130
FLD       DW DOUSE
          DFB $2A
L1146     NAME $83,'CSP'
          DW L1138
CSP       DW DOUSE
          DFB $2C
L1154     NAME $82,'R#'
          DW L1146
RNUM      DW DOUSE
          DFB $2E
L1162     NAME $83,'HLD'
          DW L1154
HLD       DW DOUSE
          DFB $30
L1170     NAME $82,'1+'
          DW L1162
ONEP      DW DOCOL
          DW ONE
          DW PLUS
          DW SEMIS
L1180     NAME $82,'2+'
          DW L1170
TWOP      DW DOCOL
          DW TWO
          DW PLUS
          DW SEMIS
L1190     NAME $84,'HERE'
          DW L1180
HERE      DW DOCOL
          DW DP
          DW AT
          DW SEMIS
L1200     NAME $85,'ALLOT'
          DW L1190
ALLOT     DW DOCOL
          DW DP
          DW PSTOR
          DW SEMIS
L1210     DFB $81,$AC ,
          DW L1200
COMMA     DW DOCOL
          DW HERE
          DW STORE
          DW TWO
          DW ALLOT
          DW SEMIS
L1222     DFB $82,'C',$AC C,
          DW L1210
CCOMM     DW DOCOL
          DW HERE
          DW CSTOR
          DW ONE
          DW ALLOT
          DW SEMIS
L1234     NAME $81,'-'
          DW L1222
SUB       DW DOCOL
          DW MINUS
          DW PLUS
          DW SEMIS
L1244     NAME $81,'='
          DW L1234
EQUAL     DW DOCOL
          DW SUB
          DW ZEQU
          DW SEMIS
L1246     NAME $82,'U<'
          DW L1244
ULESS     DW *+2
          LDA 2,X
          CMP 0,X
          LDA 3,X
          SBC 1,X
          TYA
          ROL A
          EOR #1
          STA 2,X
          STY 3,X
          JMP POP
L1254     NAME $81,'<'
          DW L1246
LESS      DW *+2
          SEC
          LDA 2,X
          SBC 0,X
          LDA 3,X
          SBC 1,X
          STY 3,X
          BVC L1258
          EOR #$80
L1258     BPL L1260
          INY
L1260     STY 2,X
          JMP POP
L1264     NAME $81,'>'
          DW L1254
GREAT     DW DOCOL
          DW SWAP
          DW LESS
          DW SEMIS
L1274     NAME $83,'ROT'
          DW L1264
ROT       DW DOCOL
          DW TOR
          DW SWAP
          DW RFROM
          DW SWAP
          DW SEMIS
L1286     NAME $85,'SPACE'
          DW L1274
SPACE     DW DOCOL
          DW BL
          DW EMIT
          DW SEMIS
L1296     NAME $84,'-DUP'
          DW L1286
DDUP      DW DOCOL
          DW DUP
          DW ZBRAN
L1301     DW $4
          DW DUP
L1303     DW SEMIS
L1308     NAME $88,'TRAVERSE'
          DW L1296
TRAV      DW DOCOL
          DW SWAP
L1312     DW OVER
          DW PLUS
          DW CLIT
          DFB $7F
          DW OVER
          DW CAT
          DW LESS
          DW ZBRAN
L1320     DW $FFF1
          DW SWAP
          DW DROP
          DW SEMIS
L1328     NAME $86,'LATEST'
          DW L1308
LATES     DW DOCOL
          DW CURR
          DW AT
          DW AT
          DW SEMIS
L1339     NAME $83,'LFA'
          DW L1328
LFA       DW DOCOL
          DW CLIT
          DFB 4
          DW SUB
          DW SEMIS
L1350     NAME $83,'CFA'
          DW L1339
CFA       DW DOCOL
          DW TWO
          DW SUB
          DW SEMIS
L1360     NAME $83,'NFA'
          DW L1350
NFA       DW DOCOL
          DW CLIT
          DFB $5
          DW SUB
          DW LIT,$FFFF
          DW TRAV
          DW SEMIS
L1373     NAME $83,'PFA'
          DW L1360
PFA       DW DOCOL
          DW ONE
          DW TRAV
          DW CLIT
          DFB 5
          DW PLUS
          DW SEMIS
L1386     NAME $84,'!CSP'
          DW L1373
SCSP      DW DOCOL
          DW SPAT
          DW CSP
          DW STORE
          DW SEMIS
L1397     NAME $86,'?ERROR'
          DW L1386
QERR      DW DOCOL
          DW SWAP
          DW ZBRAN
L1402     DW 8
          DW ERROR
          DW BRAN
L1405     DW 4
L1406     DW DROP
L1407     DW SEMIS
L1412     NAME $85,'?COMP'
          DW L1397
QCOMP     DW DOCOL
          DW STATE
          DW AT
          DW ZEQU
          DW CLIT
          DFB $11
          DW QERR
          DW SEMIS
L1426     NAME $85,'?EXEC'
          DW L1412
QEXEC     DW DOCOL
          DW STATE
          DW AT
          DW CLIT
          DFB $12
          DW QERR
          DW SEMIS
L1439     NAME $86,'?PAIRS'
          DW L1426
QPAIR     DW DOCOL
          DW SUB
          DW CLIT
          DFB $13
          DW QERR
          DW SEMIS
L1451     NAME $84,'?CSP'
          DW L1439
QCSP      DW DOCOL
          DW SPAT
          DW CSP
          DW AT
          DW SUB
          DW CLIT
          DFB $14
          DW QERR
          DW SEMIS
L1466     NAME $88,'?LOADING'
          DW L1451
QLOAD     DW DOCOL
          DW BLK
          DW AT
          DW ZEQU
          DW CLIT
          DFB $16
          DW QERR
          DW SEMIS
L1480     NAME $87,'COMPILE'
          DW L1466
COMP      DW DOCOL
          DW QCOMP
          DW RFROM
          DW DUP
          DW TWOP
          DW TOR
          DW AT
          DW COMMA
          DW SEMIS
L1495     NAME $C1,'['
          DW L1480
LBRAC     DW DOCOL
          DW ZERO
          DW STATE
          DW STORE
          DW SEMIS
L1507     NAME $81,']'
          DW L1495
RBRAC     DW DOCOL
          DW CLIT
          DFB $C0
          DW STATE
          DW STORE
          DW SEMIS
L1519     NAME $86,'SMUDGE'
          DW L1507
SMUDG     DW DOCOL
          DW LATES
          DW CLIT
          DFB $20
          DW TOGGL
          DW SEMIS
L1531     NAME $83,'HEX'
          DW L1519
HEX       DW DOCOL
          DW CLIT
          DFB 16
          DW BASE
          DW STORE
          DW SEMIS
L1543     NAME $87,'DECIMAL'
          DW L1531
DECIM     DW DOCOL
          DW CLIT
          DFB 10
          DW BASE
          DW STORE
          DW SEMIS
L1555     NAME $87,'(    ;CODE)'
          DW L1543
PSCOD     DW DOCOL
          DW RFROM
          DW LATES
          DW PFA
          DW CFA
          DW STORE
          DW SEMIS
L1568     NAME $C5,'     ;CODE'
          DW L1555
          DW DOCOL
          DW QCSP
          DW COMP
          DW PSCOD
          DW LBRAC
          DW SMUDG
          DW SEMIS
L1582     NAME $87,'<BUILDS'
          DW L1568
BUILD     DW DOCOL
          DW ZERO
          DW CONST
          DW SEMIS
L1592     NAME $85,'DOES>'
          DW L1582
DOES      DW DOCOL
          DW RFROM
          DW LATES
          DW PFA
          DW STORE
          DW PSCOD
DODOE     LDA IP+1
          PHA
          LDA IP
          PHA
          LDY #2
          LDA (W),Y
          STA IP
          INY
          LDA (W),Y
          STA IP+1
          CLC
          LDA W
          ADC #4
          PHA
          LDA W+1
          ADC #0
          JMP PUSH
L1622     NAME $85,'COUNT'
          DW L1592
COUNT     DW DOCOL
          DW DUP
          DW ONEP
          DW SWAP
          DW CAT
          DW SEMIS
L1634     NAME $84,'TYPE'
          DW L1622
TYPE      DW DOCOL
          DW DDUP
          DW ZBRAN
L1639     DW $18
          DW OVER
          DW PLUS
          DW SWAP
          DW PDO
L1644     DW I
          DW CAT
          DW EMIT
          DW PLOOP
L1648     DW $FFF8
          DW BRAN
L1650     DW $4
L1651     DW DROP
L1652     DW SEMIS
L1657     NAME $89,'-TRAILING'
          DW L1634
DTRAI     DW *+2
          LDY 0,X
          LDA 2,X
          STA N
          LDA 3,X
          STA N+1
DTR1      DEY
          BMI DTR2
          LDA (N),Y
          CMP #$20
          BEQ DTR1
DTR2      INY
          STY 0,X
          JMP NEXT
L1685     NAME $84,'(.")'
          DW L1657
PDOTQ     DW DOCOL
          DW R
          DW COUNT
          DW DUP
          DW ONEP
          DW RFROM
          DW PLUS
          DW TOR
          DW TYPE
          DW SEMIS
L1701     NAME $C2,'."'
          DW L1685
          DW DOCOL
          DW CLIT
          DFB $22
          DW STATE
          DW AT
          DW ZBRAN
L1709     DW $14
          DW COMP
          DW PDOTQ
          DW WORD
          DW HERE
          DW CAT
          DW ONEP
          DW ALLOT
          DW BRAN
L1718     DW $A
L1719     DW WORD
          DW HERE
          DW COUNT
          DW TYPE
L1723     DW SEMIS
L1729     NAME $86,'EXPECT'
          DW L1701
EXPEC     DW *+2
          STX XSAVE
          LDA 2,X
          STA N
          LDA 3,X
          STA N+1
          JSR $FD6F
          CPX #$4D
          BCC EXPEC1
          LDX #$4C
EXPEC1    LDA #0
          STA $200,X
          INX
          STA $200,X
          INX
          STA $200,X
          INX
          STA $200,X
          TXA
          TAY
EXPEC2    LDA $200,X
          AND #$7F
          STA (N),Y
          DEY
          DEX
          BPL EXPEC2
          LDX XSAVE
          JMP POPTWO
L1788     NAME $85,'QUERY'
          DW L1729
QUERY     DW DOCOL
          DW TIB
          DW AT
          DW CLIT
          DFB 80
          DW EXPEC
          DW ZERO
          DW IN
          DW STORE
          DW SEMIS
L1804     DFB $C1,$80 @
          DW L1788
          DW DOCOL
          DW BLK
          DW AT
          DW ZBRAN
L1810     DW $2A
          DW ONE
          DW BLK
          DW PSTOR
          DW ZERO
          DW IN
          DW STORE
          DW BLK
          DW AT
          DW ZERO,BSCR
          DW USLAS
          DW DROP
          DW ZEQU
          DW ZBRAN
L1824     DW 8
          DW QEXEC
          DW RFROM
          DW DROP
L1828     DW BRAN
L1829     DW 6
L1830     DW RFROM
          DW DROP
L1832     DW SEMIS
L1838     NAME $84,'FILL'
          DW L1804
FILL      DW DOCOL
          DW SWAP
          DW TOR
          DW OVER
          DW CSTOR
          DW DUP
          DW ONEP
          DW RFROM
          DW ONE
          DW SUB
          DW CMOVE
          DW SEMIS
L1856     NAME $85,'ERASE'
          DW L1838
ERASE     DW DOCOL
          DW ZERO
          DW FILL
          DW SEMIS
L1866     NAME $86,'BLANKS'
          DW L1856
BLANK     DW DOCOL
          DW BL
          DW FILL
          DW SEMIS
L1876     NAME $84,'HOLD'
          DW L1866
HOLD      DW DOCOL
          DW LIT,$FFFF
          DW HLD
          DW PSTOR
          DW HLD
          DW AT
          DW CSTOR
          DW SEMIS
L1890     NAME $83,'PAD'
          DW L1876
PAD       DW DOCOL
          DW HERE
          DW CLIT
          DFB 68
          DW PLUS
          DW SEMIS
L1902     NAME $84,'WORD'
          DW L1890
WORD      DW DOCOL
          DW BLK
          DW AT
          DW ZBRAN
L1908     DW $C
          DW BLK
          DW AT
          DW BLOCK
          DW BRAN
L1913     DW $6
L1914     DW TIB
          DW AT
L1916     DW IN
          DW AT
          DW PLUS
          DW SWAP
          DW ENCL
          DW HERE
          DW CLIT
          DFB $22
          DW BLANK
          DW IN
          DW PSTOR
          DW OVER
          DW SUB
          DW TOR
          DW R
          DW HERE
          DW CSTOR
          DW PLUS
          DW HERE
          DW ONEP
          DW RFROM
          DW CMOVE
          DW SEMIS
L1943     NAME $85,'UPPER'
          DW L1902
UPPER     DW DOCOL
          DW OVER
          DW PLUS
          DW SWAP
          DW PDO
L1950     DW I
          DW CAT
          DW CLIT
          DFB $5F
          DW GREAT
          DW ZBRAN
L1956     DW 09
          DW I
          DW CLIT
          DFB $20
          DW TOGGL
L1961     DW PLOOP
L1962     DW $FFEA
          DW SEMIS
L1968     NAME $88,'(NUMBER)'
          DW L1943
PNUMB     DW DOCOL
L1971     DW ONEP
          DW DUP
          DW TOR
          DW CAT
          DW BASE
          DW AT
          DW DIGIT
          DW ZBRAN
L1979     DW $2C
          DW SWAP
          DW BASE
          DW AT
          DW USTAR
          DW DROP
          DW ROT
          DW BASE
          DW AT
          DW USTAR
          DW DPLUS
          DW DPL
          DW AT
          DW ONEP
          DW ZBRAN
L1994     DW 8
          DW ONE
          DW DPL
          DW PSTOR
L1998     DW RFROM
          DW BRAN
L2000     DW $FFC6
L2001     DW RFROM
          DW SEMIS
L2007     NAME $86,'NUMBER'
          DW L1968
NUMBER    DW DOCOL
          DW ZERO
          DW ZERO
          DW ROT
          DW DUP
          DW ONEP
          DW CAT
          DW CLIT
          DFB $2D
          DW EQUAL
          DW DUP
          DW TOR
          DW PLUS
          DW LIT,$FFFF
L2023     DW DPL
          DW STORE
          DW PNUMB
          DW DUP
          DW CAT
          DW BL
          DW SUB
          DW ZBRAN
L2031     DW $15
          DW DUP
          DW CAT
          DW CLIT
          DFB $2E
          DW SUB
          DW ZERO
          DW QERR
          DW ZERO
          DW BRAN
L2041     DW $FFDD
L2042     DW DROP
          DW RFROM
          DW ZBRAN
L2045     DW 4
          DW DMINU
L2047     DW SEMIS
L2052     NAME $85,'-FIND'
          DW L2007
DFIND     DW DOCOL
          DW BL
          DW WORD
          DW HERE
          DW COUNT
          DW UPPER
          DW HERE
          DW CON
          DW AT
          DW AT
          DW PFIND
          DW DUP
          DW ZEQU
          DW ZBRAN
L2068     DW $A
          DW DROP
          DW HERE
          DW LATES
          DW PFIND
L2073     DW SEMIS
L2078     NAME $87,'(ABORT)'
          DW L2052
PABOR     DW DOCOL
          DW ABORT
          DW SEMIS
L2087     NAME $85,'ERROR'
          DW L2078
ERROR     DW DOCOL
          DW WARN
          DW AT
          DW ZLESS
          DW ZBRAN
          DW L2096-*
          DW PABOR
L2096     DW HERE
          DW COUNT
          DW TYPE
          DW PDOTQ
          STR ' ? '
          DW MESS
          DW SPSTO
          DW DROP,DROP
          DW IN
          DW AT
          DW BLK
          DW AT
          DW QUIT
          DW SEMIS
L2113     NAME $83,'ID.'
          DW L2087
IDDOT     DW DOCOL
          DW PAD
          DW CLIT
          DFB $20
          DW CLIT
          DFB $5F
          DW FILL
          DW DUP
          DW PFA
          DW LFA
          DW OVER
          DW SUB
          DW PAD
          DW SWAP
          DW CMOVE
          DW PAD
          DW COUNT
          DW CLIT
          DFB $1F
          DW ANDD
          DW TYPE
          DW SPACE
          DW SEMIS
L2142     NAME $86,'CREATE'
          DW L2113
CREAT     DW DOCOL
          DW LIT,$A800
          DW HERE
          DW ULESS
          DW TWO
          DW QERR
          DW DFIND
          DW ZBRAN
L2155     DW $0F
          DW DROP
          DW NFA
          DW IDDOT
          DW CLIT
          DFB 4
          DW MESS
          DW SPACE
L2163     DW HERE
          DW DUP
          DW CAT
          DW WIDTH
          DW AT
          DW MIN
          DW ONEP
          DW ALLOT
          DW DP
          DW CAT
          DW CLIT
          DFB $FD
          DW EQUAL
          DW ALLOT
          DW DUP
          DW CLIT
          DFB $A0
          DW TOGGL
          DW HERE
          DW ONE
          DW SUB
          DW CLIT
          DFB $80
          DW TOGGL
          DW LATES
          DW COMMA
          DW CURR
          DW AT
          DW STORE
          DW HERE
          DW TWOP
          DW COMMA
          DW SEMIS
L2200     NAME $C9,'[COMPILE]'
          DW L2142
          DW DOCOL
          DW DFIND
          DW ZEQU
          DW ZERO
          DW QERR
          DW DROP
          DW CFA
          DW COMMA
          DW SEMIS
L2216     NAME $C7,'LITERAL'
          DW L2200
LITER     DW DOCOL
          DW STATE
          DW AT
          DW ZBRAN
L2222     DW 8
          DW COMP
          DW LIT
          DW COMMA
L2226     DW SEMIS
L2232     NAME $C8,'DLITERAL'
          DW L2216
DLIT      DW DOCOL
          DW STATE
          DW AT
          DW ZBRAN
L2238     DW 8
          DW SWAP
          DW LITER
          DW LITER
L2242     DW SEMIS
L2248     NAME $86,'?STACK'
          DW L2232
QSTAC     DW DOCOL
          DW CLIT
          DFB TOS-2
          DW SPAT
          DW ULESS
          DW ONE
          DW QERR
          DW SPAT
          DW CLIT
          DFB BOS
          DW ULESS
          DW CLIT
          DFB 7
          DW QERR
          DW SEMIS
L2269     NAME $89,'INTERPRET'
          DW L2248
INTER     DW DOCOL
L2272     DW DFIND
          DW ZBRAN
L2274     DW $1E
          DW STATE
          DW AT
          DW LESS
          DW ZBRAN
L2279     DW $A
          DW CFA
          DW COMMA
          DW BRAN
L2283     DW $6
L2284     DW CFA
          DW EXEC
L2286     DW QSTAC
          DW BRAN
L2288     DW $1C
L2289     DW HERE
          DW NUMBER
          DW DPL
          DW AT
          DW ONEP
          DW ZBRAN
L2295     DW 8
          DW DLIT
          DW BRAN
L2298     DW $6
L2299     DW DROP
          DW LITER
L2301     DW QSTAC
L2302     DW BRAN
L2303     DW $FFC2
L2309     NAME $89,'IMMEDIATE'
          DW L2269
          DW DOCOL
          DW LATES
          DW CLIT
          DFB $40
          DW TOGGL
          DW SEMIS
L2321     NAME $8A,'VOCABULARY'
          DW L2309
          DW DOCOL
          DW BUILD
          DW LIT,$A081
          DW COMMA
          DW CURR
          DW AT
          DW CFA
          DW COMMA
          DW HERE
          DW VOCL
          DW AT
          DW COMMA
          DW VOCL
          DW STORE
          DW DOES
DOVOC     DW TWOP
          DW CON
          DW STORE
          DW SEMIS
L2346     NAME $C5,'FORTH'
          DW L2321
FORTH     DW DODOE
          DW DOVOC
          DW $A081
XFOR      DW NTOP
VLO       DW 0
L2357     NAME $8B,'DEFINITIONS'
          DW L2346
DEFIN     DW DOCOL
          DW CON
          DW AT
          DW CURR
          DW STORE
          DW SEMIS
L2369     NAME $C1,'('
          DW L2357
          DW DOCOL
          DW CLIT
          DFB $29
          DW WORD
          DW SEMIS
L2381     NAME $84,'QUIT'
          DW L2369
QUIT      DW DOCOL
          DW ZERO
          DW BLK
          DW STORE
          DW LBRAC
L2388     DW RPSTO
          DW CR
          DW QUERY
          DW INTER
          DW STATE
          DW AT
          DW ZEQU
          DW ZBRAN
          DW L2399-*
          DW PDOTQ
          STR 'OK'
L2399     DW BRAN
          DW L2388-*
          DW SEMIS
L2406     NAME $85,'ABORT'
          DW L2381
ABORT     DW DOCOL
ABORT1    DW SPSTO
          DW DECIM
          DW DR0
          DW CR
          DW PDOTQ
          STR 'APPLE-DAYTON ProFORTH V3.2'
          DW CR
          DW FORTH
          DW DEFIN
          DW QUIT
L2423     NAME $84,'COLD'
          DW L2406
COLD      DW *+2
          LDA #>WARM
          STA $3F9
          LDA #<WARM
          STA $3FA
          LDA #>RESET
          STA $3F2
          LDA #<RESET
          STA $3F3
          EOR #$A5
          STA $3F4
          LDA #$4C
          STA $3EA
          LDA #>MYHOOK
          STA $3EB
          LDA #<MYHOOK
          STA $3EC
          LDA ORIG+$0C
          STA FORTH+6
          LDA ORIG+$0D
          STA FORTH+7
          LDY #$15
          BNE L2433
WARM      LDY #$0F
L2433     LDA ORIG+$10
          STA UP
          LDA ORIG+$11
          STA UP+1
L2437     LDA ORIG+$0C,Y
          STA (UP),Y
          DEY
          BPL L2437
          LDA #$80 NULL prompt if
          STA $33 backspace to far
          JSR MYHOOK
          LDA #<ABORT1
          STA IP+1
          LDA #>ABORT1
          STA IP
          CLD
          LDA #$6C
          STA W-1
          JMP RPSTO+2
RESET     LDA $BF98
          AND #2
          BEQ RESET1
          JSR $C300
RESET1    JMP WARM
MYKEY     JSR $FF58
          CMP #$FF
          BNE MYKEY1
          LDA #$88 DEL=^H
MYKEY1    RTS
MYHOOK    LDA KSWL+1
          CMP #<MYKEY
          BEQ HOOKED
          STA MYKEY+2
          LDA KSWL
          STA MYKEY+1
          LDA #>MYKEY
          STA KSWL
          LDA #<MYKEY
          STA KSWL+1
HOOKED    RTS
L2453     NAME $84,'S->D'
          DW L2423
STOD      DW DOCOL
          DW DUP
          DW ZLESS
          DW MINUS
          DW SEMIS
L2464     NAME $82,'+-'
          DW L2453
PM        DW DOCOL
          DW ZLESS
          DW ZBRAN
L2469     DW 4
          DW MINUS
L2471     DW SEMIS
L2476     NAME $83,'D+-'
          DW L2464
DPM       DW DOCOL
          DW ZLESS
          DW ZBRAN
L2481     DW 4
          DW DMINU
L2483     DW SEMIS
L2488     NAME $83,'ABS'
          DW L2476
ABS       DW DOCOL
          DW DUP
          DW PM
          DW SEMIS
L2498     NAME $84,'DABS'
          DW L2488
DABS      DW DOCOL
          DW DUP
          DW DPM
          DW SEMIS
L2508     NAME $83,'MIN'
          DW L2498
MIN       DW DOCOL
          DW OVER
          DW OVER
          DW GREAT
          DW ZBRAN
L2515     DW 4
          DW SWAP
L2517     DW DROP
          DW SEMIS
L2523     NAME $83,'MAX'
          DW L2508
MAX       DW DOCOL
          DW OVER
          DW OVER
          DW LESS
          DW ZBRAN
L2530     DW 4
          DW SWAP
L2532     DW DROP
          DW SEMIS
L2538     NAME $82,'M*'
          DW L2523
MSTAR     DW DOCOL
          DW OVER
          DW OVER
          DW XOR
          DW TOR
          DW ABS
          DW SWAP
          DW ABS
          DW USTAR
          DW RFROM
          DW DPM
          DW SEMIS
L2556     NAME $82,'M/'
          DW L2538
MSLAS     DW DOCOL
          DW OVER
          DW TOR
          DW TOR
          DW DABS
          DW R
          DW ABS
          DW USLAS
          DW RFROM
          DW R
          DW XOR
          DW PM
          DW SWAP
          DW RFROM
          DW PM
          DW SWAP
          DW SEMIS
L2579     NAME $81,'*'
          DW L2556
STAR      DW DOCOL
          DW USTAR
          DW DROP
          DW SEMIS
L2589     NAME $84,'/MOD'
          DW L2579
SLMOD     DW DOCOL
          DW TOR
          DW STOD
          DW RFROM
          DW MSLAS
          DW SEMIS
L2601     NAME $81,'/'
          DW L2589
SLASH     DW DOCOL
          DW SLMOD
          DW SWAP
          DW DROP
          DW SEMIS
L2612     NAME $83,'MOD'
          DW L2601
MOD       DW DOCOL
          DW SLMOD
          DW DROP
          DW SEMIS
L2622     NAME $85,'*/MOD'
          DW L2612
SSMOD     DW DOCOL
          DW TOR
          DW MSTAR
          DW RFROM
          DW MSLAS
          DW SEMIS
L2634     NAME $82,'*/'
          DW L2622
SSLAS     DW DOCOL
          DW SSMOD
          DW SWAP
          DW DROP
          DW SEMIS
L2645     NAME $85,'M/MOD'
          DW L2634
MSMOD     DW DOCOL
          DW TOR
          DW ZERO
          DW R
          DW USLAS
          DW RFROM
          DW SWAP
          DW TOR
          DW USLAS
          DW RFROM
          DW SEMIS
L2662     NAME $83,'USE'
          DW L2645
USE       DW DOVAR
          DW DAREA
L2670     NAME $84,'PREV'
          DW L2662
PREV      DW DOVAR
          DW DAREA
L2678     NAME $84,'+BUF'
          DW L2670
PBUF      DW DOCOL
          DW LIT
          DW SSIZE+4
          DW PLUS
          DW DUP
          DW LIMIT
          DW EQUAL
          DW ZBRAN
L2688     DW 6
          DW DROP
          DW FIRST
L2691     DW DUP
          DW PREV
          DW AT
          DW SUB
          DW SEMIS
L2700     NAME $86,'UPDATE'
          DW L2678
UPDAT     DW DOCOL
          DW PREV
          DW AT
          DW AT
          DW LIT,$8000
          DW OR
          DW PREV
          DW AT
          DW STORE
          DW SEMIS
L2705     NAME $85,'FLUSH'
          DW L2700
          DW DOCOL
          DW LIT,NBUF+1
          DW ZERO,PDO
L2835     DW LIT,$7FFF,BUFFR
          DW DROP,PLOOP,L2835-*
          DW SEMIS
L2716     NAME $8D,'EMPTY-BUFFERS'
          DW L2705
          DW DOCOL
          DW FIRST
          DW LIMIT
          DW OVER
          DW SUB
          DW ERASE
          DW SEMIS
L2729     NAME $83,'DR0'
          DW L2716
DR0       DW DOCOL
          DW LIT,0,OFSET,STORE
          DW SEMIS
L2740     NAME $83,'DR1'
          DW L2729
DR1       DW DOCOL
          DW FSIZE,OFSET,STORE
          DW SEMIS
L2751     NAME $86,'BUFFER'
          DW L2740
BUFFR     DW DOCOL
          DW USE
          DW AT
          DW DUP
          DW TOR
L2758     DW PBUF
          DW ZBRAN
L2760     DW $FFFC
          DW USE
          DW STORE
          DW R
          DW AT
          DW ZLESS
          DW ZBRAN
L2767     DW $14
          DW R
          DW TWOP
          DW R
          DW AT
          DW LIT,$7FFF
          DW ANDD
          DW ZERO
          DW RSLW
L2776     DW R
          DW STORE
          DW R
          DW PREV
          DW STORE
          DW RFROM
          DW TWOP
          DW SEMIS
L2788     NAME $85,'BLOCK'
          DW L2751
BLOCK     DW DOCOL
          DW OFSET
          DW AT
          DW PLUS
          DW TOR
          DW PREV
          DW AT
          DW DUP
          DW AT
          DW R
          DW SUB
          DW DUP
          DW PLUS
          DW ZBRAN
L2804     DW $34
L2805     DW PBUF
          DW ZEQU
          DW ZBRAN
L2808     DW $14
          DW DROP
          DW R
          DW BUFFR
          DW DUP
          DW R
          DW ONE
          DW RSLW
          DW TWO
          DW SUB
L2818     DW DUP
          DW AT
          DW R
          DW SUB
          DW DUP
          DW PLUS
          DW ZEQU
          DW ZBRAN
L2826     DW $FFD6
          DW DUP
          DW PREV
          DW STORE
L2830     DW RFROM
          DW DROP
          DW TWOP
          DW SEMIS
L2838     NAME $86,'(LINE)'
          DW L2788
PLINE     DW DOCOL
          DW TOR
          DW CSLL
          DW BBUF
          DW SSMOD
          DW RFROM
          DW BSCR
          DW STAR
          DW PLUS
          DW BLOCK
          DW PLUS
          DW CSLL
          DW SEMIS
L2857     NAME $85,'.LINE'
          DW L2838
DLINE     DW DOCOL
          DW PLINE
          DW DTRAI
          DW TYPE
          DW SEMIS
L2868     NAME $87,'MESSAGE'
          DW L2857
MESS      DW DOCOL
          DW WARN
          DW AT
          DW ZBRAN
          DW L2888-*
          DW CLIT
          DFB 4
          DW OFSET
          DW AT
          DW BSCR
          DW SLASH
          DW SUB
          DW DLINE
          DW BRAN
          DW L2891-*
L2888     DW PDOTQ
          STR 'MSG #'
          DW DOT
L2891     DW SEMIS
L2896     NAME $84,'LOAD'
          DW L2868
LOAD      DW DOCOL
          DW BLK
          DW AT
          DW TOR
          DW IN
          DW AT
          DW TOR
          DW ZERO
          DW IN
          DW STORE
          DW BSCR
          DW STAR
          DW BLK
          DW STORE
          DW INTER
          DW RFROM
          DW IN
          DW STORE
          DW RFROM
          DW BLK
          DW STORE
          DW SEMIS
L2924     NAME $C3,'-->'
          DW L2896
          DW DOCOL
          DW QLOAD
          DW ZERO
          DW IN
          DW STORE
          DW BSCR
          DW BLK
          DW AT
          DW OVER
          DW MOD
          DW SUB
          DW BLK
          DW PSTOR
          DW SEMIS
XEMIT     INC UAREA+$1A
          BNE XEMIT1
          INC UAREA+$1B
XEMIT1    LDA 0,X
          STX XSAVE
          ORA #$80
          JSR OUTCH
          LDX XSAVE
          JMP POP
XKEY      STX XSAVE
          JSR INCH
          AND #$7F
          LDX XSAVE
          JMP PUSHOA
XQTER     BIT $C000
          BPL XQTER2
XQTER1    BIT $C010
          BIT $C000
          BMI XQTER1
          INY
XQTER2    TYA
          JMP PUSHOA
XCR       STX XSAVE
          JSR CROUT
          LDX XSAVE
          JMP NEXT
L3050     NAME $85,'(R/W)'
          DW L2924
PRSLW     DW *+2
          LDA 0,X
          STA SETREF
          STA RWREF
          LDA #$CA
          STA RWCOM
          LDA 2,X
          BNE PRSLW1
          LDA #$CB
          STA RWCOM
PRSLW1    LDA 6,X
          STA RWBUF
          LDA 7,X
          STA RWBUF+1
          LDA 4,X
          ASL A
          STA SETPOS+1
          LDA 5,X
          ROL A
          STA SETPOS+2
          ASL SETPOS+1
          ROL SETPOS+2
          JSR MLI
          DB $CE Set file position
          DW SETLIST
          BCS PRSLW2
          JSR MLI
RWCOM     DB 0 Read/write command
          DW RWLIST
PRSLW2    PHA
          TXA
          CLC
          ADC #6
          TAX
          TYA
          JMP PUT
SETLIST   DB 2
SETREF    DB 0
SETPOS    DB 0,0,0
RWLIST    DB 4
RWREF     DB 0
RWBUF     DW 0
RWLEN     DW 1024,0
FCLIST    DB 1,0
BLIST     DFB 4,0,0,0,0,0,0
L3060     NAME $83,'R/W'
          DW L3050
RSLW      DW DOCOL,TOR,DUP,FSIZE,ULESS
          DW ZBRAN,RSLW1-*
          DW ONE,BRAN,RSLW2-*
RSLW1     DW FSIZE,SUB,TWO
RSLW2     DW RFROM,SWAP,PRSLW
          DW DDUP,ZBRAN,RSLW3-*
          DW DOT,LIT,8,ERROR
RSLW3     DW SEMIS
L3202     NAME $C1,"'"
          DW L3060
TICK      DW DOCOL
          DW DFIND
          DW ZEQU
          DW ZERO
          DW QERR
          DW DROP
          DW LITER
          DW SEMIS
L3217     NAME $86,'FORGET'
          DW L3202
FORG      DW DOCOL
          DW TICK,NFA,DUP
          DW FENCE,AT,ULESS,CLIT
          DFB $15
          DW QERR,TOR,VOCL,AT
L3220     DW R,OVER,ULESS
          DW ZBRAN,L3225-*
          DW FORTH,DEFIN,AT,DUP
          DW VOCL,STORE
          DW BRAN,$FFFF-24+1  ;L3220-*
L3225     DW DUP,CLIT
          DFB 4
          DW SUB
L3228     DW PFA,LFA,AT
          DW DUP,R,ULESS
          DW ZBRAN,$FFFF-14+1 ;L3228-*
          DW OVER,TWO,SUB,STORE
          DW AT,DDUP,ZEQU
          DW ZBRAN,$FFFF-39+1 ;L3225-*
          DW RFROM,DP,STORE
          DW SEMIS
L3250     NAME $84,'BACK'
          DW L3217
BACK      DW DOCOL
          DW HERE
          DW SUB
          DW COMMA
          DW SEMIS
L3261     NAME $C5,'BEGIN'
          DW L3250
          DW DOCOL
          DW QCOMP
          DW HERE
          DW ONE
          DW SEMIS
L3273     NAME $C5,'ENDIF'
          DW L3261
ENDIF     DW DOCOL
          DW QCOMP
          DW TWO
          DW QPAIR
          DW HERE
          DW OVER
          DW SUB
          DW SWAP
          DW STORE
          DW SEMIS
L3290     NAME $C4,'THEN'
          DW L3273
          DW DOCOL
          DW ENDIF
          DW SEMIS
L3300     NAME $C2,'DO'
          DW L3290
          DW DOCOL
          DW COMP
          DW PDO
          DW HERE
          DW THREE
          DW SEMIS
L3313     NAME $C4,'LOOP'
          DW L3300
          DW DOCOL
          DW THREE
          DW QPAIR
          DW COMP
          DW PLOOP
          DW BACK
          DW SEMIS
          DW SEMIS
L3327     NAME $C5,'+LOOP'
          DW L3313
          DW DOCOL
          DW THREE
          DW QPAIR
          DW COMP
          DW PPLOO
          DW BACK
          DW SEMIS
L3341     NAME $C5,'UNTIL'
          DW L3327
UNTIL     DW DOCOL
          DW ONE
          DW QPAIR
          DW COMP
          DW ZBRAN
          DW BACK
          DW SEMIS
L3355     NAME $C3,'END'
          DW L3341
          DW DOCOL
          DW UNTIL
          DW SEMIS
L3365     NAME $C5,'AGAIN'
          DW L3355
AGAIN     DW DOCOL
          DW ONE
          DW QPAIR
          DW COMP
          DW BRAN
          DW BACK
          DW SEMIS
L3379     NAME $C6,'REPEAT'
          DW L3365
          DW DOCOL
          DW TOR
          DW TOR
          DW AGAIN
          DW RFROM
          DW RFROM
          DW TWO
          DW SUB
          DW ENDIF
          DW SEMIS
L3396     NAME $C2,'IF'
          DW L3379
IF        DW DOCOL
          DW COMP
          DW ZBRAN
          DW HERE
          DW ZERO
          DW COMMA
          DW TWO
          DW SEMIS
L3411     NAME $C4,'ELSE'
          DW L3396
          DW DOCOL
          DW TWO
          DW QPAIR
          DW COMP
          DW BRAN
          DW HERE
          DW ZERO
          DW COMMA
          DW SWAP
          DW TWO
          DW ENDIF
          DW TWO
          DW SEMIS
L3431     NAME $C5,'WHILE'
          DW L3411
          DW DOCOL
          DW IF
          DW TWOP
          DW SEMIS
L3442     NAME $86,'SPACES'
          DW L3431
SPACS     DW DOCOL
          DW ZERO
          DW MAX
          DW DDUP
          DW ZBRAN
L3449     DW $0C
          DW ZERO
          DW PDO
L3452     DW SPACE
          DW PLOOP
L3454     DW $FFFC
L3455     DW SEMIS
L3460     NAME $82,'<#'
          DW L3442
BDIGS     DW DOCOL
          DW PAD
          DW HLD
          DW STORE
          DW SEMIS
L3471     NAME $82,'#>'
          DW L3460
EDIGS     DW DOCOL
          DW DROP
          DW DROP
          DW HLD
          DW AT
          DW PAD
          DW OVER
          DW SUB
          DW SEMIS
L3486     NAME $84,'SIGN'
          DW L3471
SIGN      DW DOCOL
          DW ROT
          DW ZLESS
          DW ZBRAN
L3492     DW $7
          DW CLIT
          DFB $2D
          DW HOLD
L3496     DW SEMIS
L3501     DFB $81,$A3
          DW L3486
DIG       DW DOCOL
          DW BASE
          DW AT
          DW MSMOD
          DW ROT
          DW CLIT
          DFB 9
          DW OVER
          DW LESS
          DW ZBRAN
L3513     DW 7
          DW CLIT
          DFB 7
          DW PLUS
L3517     DW CLIT
          DFB $30
          DW PLUS
          DW HOLD
          DW SEMIS
L3526     NAME $82,'#S'
          DW L3501
DIGS      DW DOCOL
L3529     DW DIG
          DW OVER
          DW OVER
          DW OR
          DW ZEQU
          DW ZBRAN
L3535     DW $FFF4
          DW SEMIS
L3541     NAME $83,'D.R'
          DW L3526
DDOTR     DW DOCOL
          DW TOR
          DW SWAP
          DW OVER
          DW DABS
          DW BDIGS
          DW DIGS
          DW SIGN
          DW EDIGS
          DW RFROM
          DW OVER
          DW SUB
          DW SPACS
          DW TYPE
          DW SEMIS
L3562     NAME $82,'D.'
          DW L3541
DDOT      DW DOCOL
          DW ZERO
          DW DDOTR
          DW SPACE
          DW SEMIS
L3573     NAME $82,'.R'
          DW L3562
DOTR      DW DOCOL
          DW TOR
          DW STOD
          DW RFROM
          DW DDOTR
          DW SEMIS
L3585     DFB $81,$AE
          DW L3573
DOT       DW DOCOL
          DW STOD
          DW DDOT
          DW SEMIS
L3595     NAME $81,'?'
          DW L3585
QUES      DW DOCOL
          DW AT
          DW DOT
          DW SEMIS
L3605     NAME $84,'LIST'
          DW L3595
LIST      DW DOCOL
          DW DECIM
          DW CR
          DW DUP
          DW SCR
          DW STORE
          DW PDOTQ
          DFB 6
          ASC 'Scr # '
          DW DOT
          DW CLIT
          DFB 16
          DW ZERO
          DW PDO
L3620     DW CR
          DW I
          DW THREE
          DW DOTR
          DW SPACE
          DW I
          DW SCR
          DW AT
          DW DLINE
          DW PLOOP
L3630     DW $FFEC
          DW CR
          DW SEMIS
L3637     NAME $85,'INDEX'
          DW L3605
          DW DOCOL
          DW CR
          DW ONEP
          DW SWAP
          DW PDO
L3647     DW CR
          DW I
          DW THREE
          DW DOTR
          DW SPACE
          DW ZERO
          DW I
          DW DLINE
          DW QTERM
          DW ZBRAN
L3657     DW 4
          DW LEAVE
L3659     DW PLOOP
L3660     DW $FFE6
          DW CLIT
          DFB $0D
          DW EMIT
          DW SEMIS
L3666     NAME $85,'TRIAD'
          DW L3637
          DW DOCOL
          DW THREE
          DW SLASH
          DW THREE
          DW STAR
          DW THREE
          DW OVER
          DW PLUS
          DW SWAP
          DW PDO
L3681     DW CR
          DW I
          DW LIST
          DW PLOOP
L3685     DW $FFF8
          DW CR
          DW CLIT
          DFB $F
          DW MESS
          DW CR
          DW CLIT
          DFB $0D
          DW EMIT
          DW SEMIS
L3696     NAME $85,'VLIST'
          DW L3666
VLIST     DW DOCOL
          DW CLIT
          DFB $80
          DW OUT
          DW STORE
          DW CON
          DW AT
          DW AT
L3706     DW OUT
          DW AT
          DW CSLL
          DW GREAT
          DW ZBRAN
          DW L3716-*
          DW CR
          DW ZERO
          DW OUT
          DW STORE
L3716     DW DUP
          DW IDDOT
          DW SPACE
          DW SPACE
          DW PFA
          DW LFA
          DW AT
          DW DUP
          DW ZEQU
          DW QTERM
          DW OR
          DW ZBRAN
          DW L3706-*
          DW DROP
          DW SEMIS
NMON      NAME $83,'MON'
          DW L3696
MON       DW *+2
          JMP MONITOR
NMLI      NAME $83,'MLI'
          DW NMON
DOMLI     DW *+2
          LDA 0,X
          STA MLICOM
          LDA 2,X
          STA MLICOM+1
          LDA 3,X
          STA MLICOM+2
          JSR MLI
MLICOM    DFB 0,0,0
          INX
          INX
          PHA
          TYA
          JMP PUT
NCALL     NAME $84,'CALL'
          DW NMLI
CALL      DW *+2
          STX XSAVE
          LDA 0,X
          STA CALL1+1
          LDA 1,X
          STA CALL1+2
          LDA 0
          LDX 1
          LDY 2
CALL1     JSR 0
          STY 2
          STX 1
          STA 0
          LDX XSAVE
          JMP POP
NTOP      NAME $83,'BYE'
          DW NCALL
BYE       DW *+2
          JSR MLI
          DB $CC
          DW FCLIST
          JSR MLI
          DFB $65
          DW BLIST
TOP       DFB 00
```
  
fsys.s (ProDos Filesystem interface)  
```
          LST ON,NOGen,NOAsym,NOVsym
* FORTH.SYSTEM by John Matthews, M.D.
A1        EQU $3C
A2        EQU $3E
A4        EQU $42
FSTART    EQU $800 Forth dictionary entry
FBUF1     EQU $B200
MLI       EQU $BF00 Call MLI
BITMAP    EQU $BF58 ProDOS memory bit map
FLEVEL    EQU $BF94
MACHID    EQU $BF98
CLR80COL  EQU $C000 Hardware switches
CLR80VID  EQU $C00C
SETALTCH  EQU $C00F
ROMON     EQU $C082
HOME      EQU $FC58 Monitor routines
GETKEY    EQU $FD0C
CROUT     EQU $FD8E
PRBYTE    EQU $FDDA
COUT      EQU $FDED
MOVE      EQU $FE2C
SETKBD    EQU $FE89
SETVID    EQU $FE93
          SYS
          ORG $2000
          LDX #$FF
          TXS
          LDA #0
          STA A1
          STA A2
          STA A4
          LDA #$21
          STA A1+1
          LDA #$24
          STA A2+1
          LDA #<FSYS
          STA A4+1
          LDY #0
          JSR MOVE
          LDA #>FSYS
          STA $3F2
          LDA #<FSYS
          STA $3F3
          EOR #$A5
          STA $3F4
          JMP FSYS
          ORG $A000
* Initialize normal keyboard & 40 columns
FSYS      LDA ROMON Enable the ROMs!
          JSR SETVID
          JSR SETKBD
          STA CLR80VID
          STA SETALTCH
          STA CLR80COL
          LDA MACHID
          AND #2
          BEQ NO80COL
          JSR $C300
NO80COL   JSR HOME
          JSR SCREEN
* Initialize the ProDOS bit map
          LDX #$17
          LDA #1 Global page ($BF00) in use
          STA BITMAP,X
          DEX
          LDA #0 Free all other pages
          STA FLEVEL File level = 0
CLRBITS   STA BITMAP,X
          DEX
          BPL CLRBITS
          LDA #$CF Zero page, stack and text
          STA BITMAP  page 1 in use
* Clear the future user area & buffers
          LDA #$B2
          STA A1+1
          LDY #0
          STY A1
CLRBUF1   TYA
CLRBUF2   STA (A1),Y
          INY
          BNE CLRBUF2
          INC A1+1
          LDA A1+1
          CMP #$BF
          BNE CLRBUF1
* Close any open files
          JSR MLI
          DB $CC CLOSE command
          DW CLOSLIST
          BCS ERROR
* Get the prefix
          JSR MLI
          DB $C7 GET PREFIX command
          DW PREFLIST
          BCS ERROR
          LDA PREFIX
          BEQ ERROR Null prefix is death
* Open F.DICT file
          LDA #>FNAME1
          STA ONAME
          LDA #<FNAME1
          STA ONAME+1
          JSR MLI
          DB $C8 OPEN command
          DW OPENLIST
          BCS ERROR
* Get end of file mark
          LDA REFNO Use the REFNO supplied
          STA EREF  by the call to OPEN
          JSR MLI
          DB $D1 GET EOF command
          DW EOFLIST
          BCS ERROR
* Read the file
          LDA REFNO Use the REFNO again
          STA RREF
          LDA EPOS Use the length supplied
          STA RLENGTH  by the call to GET EOF
          LDA EPOS+1
          STA RLENGTH+1
          JSR MLI
          DB $CA READ command
          DW READLIST
          BCS ERROR
* Close F.DICT
          JSR MLI
          DB $CC CLOSE command
          DW CLOSLIST
          BCS ERROR
* Open F.DISK
          LDA #>FNAME2
          STA ONAME
          LDA #<FNAME2
          STA ONAME+1
          JSR MLI
          DB $C8 OPEN command
          DW OPENLIST
          BCS ERROR
          JMP FSTART
* Handle fatal error
ERROR     PHA A Save the error code
          JSR CROUT Print RETURN
          LDY ERRMSG Print error message
          LDX #1
ERR1      LDA ERRMSG,X
          ORA #$80
          JSR COUT
          INX
          DEY
          BNE ERR1
          PLA A Restore error code
          JSR PRBYTE Print it
          JSR GETKEY Wait for it
          JSR MLI Die horribly
          DB $65 QUIT command
          DW QLIST
* Standard print routine
PRINT1    LDY #0
          PLA
          STA A1
          PLA
          STA A1+1
PRINT2    INC A1
          BNE PRINT3
          INC A1+1
PRINT3    LDA (A1),Y
          BEQ PRINT4
          ORA #$80
          JSR COUT
          JMP PRINT2
PRINT4    INC A1
          BNE PRINT5
          INC A1+1
PRINT5    JMP (A1)
* Print the credits
SCREEN    JSR PRINT1
          DB 13,13
          ASC "*** PRO-FORTH V3.2 ***"
          DB 13,13,13
          ASC "PRESENTED BY APPLE-DAYTON, INC."
          DB 13,13
          ASC "PO BOX 1666 FAIRBORN OH 45324-7666"
          DB 13,13,13
          ASC "COURTESY OF THE FORTH INTEREST GROUP"
          DB 13,13
          ASC "PO BOX 1105 SAN CARLOS CA 94070"
          DB 13,13,13
          ASC "ADAPTED FOR PRODOS BY JOHN B. MATTHEWS"
          DB 13,13,13
          DB 0
          RTS
* "Prefix" parameter list
PREFLIST  DB 1 Parameter count
          DW PREFIX Pathname pointer
* "Open" parameter list
OPENLIST  DB 3 Parameter count
ONAME     DW FNAME1 File name pointer
          DW FBUF1 File #1 buffer addr.
REFNO     DB 0 Reference number
* "End of File" parameter list
EOFLIST   DB 2 Parameter count
EREF      DB 0 Reference number
EPOS      DB 0,0,0 File position
* "Read" parameter list
READLIST  DB 4 Parameter count
RREF      DB 0 Reference number
RDATA     DW FSTART Data buffer addr.
RLENGTH   DW 0 Requested length
          DW 0 Actual length
* "Close" parameter list
CLOSLIST  DB 1 Parameter count
CREF      DB 0 0 closes all open files
* "Quit aprameter list
QLIST     DFB 4,0,0,0,0,0,0
* String storage
ERRMSG    STR "PRODOS ERROR: $"
FNAME1    STR "F.DICT"
FNAME2    STR "F.DISK"
PREFIX    DS 64,0
```
