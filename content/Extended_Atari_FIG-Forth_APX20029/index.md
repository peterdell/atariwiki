---
title: Extended Atari FIG-Forth APX20029
---
# EXTENDED Atari fig-FORTH, Cassette: APX-10029, Diskette: APX-20029 (Atari Program Exchange)  
  
  
## Disks  
  
[APX_Extended_Fig_Forth.atr](attachments/APX_Extended_Fig_Forth.atr)  
  
## Earlier versions  
  
Earlier versions of this Forth were sold or otherwise distributed by the Author:  
- "NMV Forth" (or: "NWV Forth"); lost  
- "S*P*A*C*E Forth" ("s*p*a*c*e fig4th 1.1") ''(files to be amended)''  
  
  
## Official add-ons:  
- fun-FORTH (APX-20146) - with manual ''(files to be amended / linked)''  
- FORTH Turtle Graphics Plus (APX-20157) - with manual ''(files to be amended / linked)''  
  
## Manuals  
  
[Extended_fig-FORTH_-_APX_APX-20029.pdf](attachments/Extended_fig-FORTH_-_APX_APX-20029.pdf) size: 7.7 MB ; EXTENDED fig-FORTH, Rev. 1, 1981 by Patrick L. Mullarky  
[EXTENDED_fig-FORTH_Rev.2.pdf](attachments/EXTENDED_fig-FORTH_Rev.2.pdf) size: 7.7 MB ; EXTENDED fig-FORTH, Rev. 2, Edition B, 1982 by Patrick L. Mullarky ; donated by Allan Bushman, thank you so much Allen in the name of the Atari community! :-)  
  
## Making APX Extended fig-FORTH Turn-key  
It is possible to make APX Extended fig-FORTH (and most fig-FORTH implementations) execute a word upon boot.  
For example, to make the interpreter execute the word MYPROGRAM, enter the following:  
```  
' MYPROGRAM CFA ' ABORT 4 + !  
```  
Followed by a  
```  
SAVE  
```  
  
## Screens  
```
SCR # 14 
  0 ( ERROR MESSAGES )
  1 Stack empty
  2 Dictionary full
  3 Wrong address mode
  4 Isn't unique
  5 Value error
  6 Disk address error
  7 Stack full
  8 Disk Error!
  9 
 10 
 11 
 12 
 13 
 14 
 15 

SCR # 15 
  0 ( ERROR MESSAGES )
  1 Use only in Definitions
  2 Execution only
  3 Conditionals not paired
  4 Definition not finished
  5 In protected dictionary
  6 Use only when loading
  7 Off current screen
  8 Declare VOCABULARY
  9 
 10 
 11 
 12 
 13 
 14 
 15 

SCR # 16 
  0 
  1 
  2 
  3 
  4 
  5 
  6 
  7 
  8 
  9 
 10 
 11 
 12 
 13 
 14 
 15 

SCR # 17 
  0 ( CASSETTE LOAD )
  1 
  2 
  3 
  4 ( LOAD DEBUG )
  5    21 LOAD
  6 
  7 ( LOAD ASSEMBLER )
  8    39 LOAD
  9 
 10 
 11 
 12 
 13 ;S
 14 
 15 

SCR # 18 
  0 ( FULL LOAD )
  1 
  2 
  3 
  4 ( LOAD DEBUG )
  5    21 LOAD
  6 
  7 ( LOAD EDITOR )
  8   27 LOAD
  9 
 10 ( LOAD ASSEMBLER )
 11    39 LOAD
 12 
 13 ;S
 14 
 15 

SCR # 19 
  0 
  1 
  2 
  3 
  4 
  5 
  6 
  7 
  8 
  9 
 10 
 11 
 12 
 13 
 14 
 15 

SCR # 20 
  0 ( ATARI FORTH DEFS )
  1     BASE @ HEX
  2 
  3 : PON    1 PFLAG ! ; ( PRT ON )
  4 : POFF   0 PFLAG ! ; ( PRT OFF )
  5 
  6 : BEEP  0C0 0 DO
  7    08 0D01F C! 6 0 DO LOOP
  8    00 0D01F C! 6 0 DO LOOP
  9    LOOP ;
 10 
 11 : ASCII BL WORD HERE 1+ C@
 12  STATE @ IF COMPILE CLIT C,
 13  THEN ;  IMMEDIATE
 14 
 15 BASE ! ;S

SCR # 21 
  0 ( DEBUGGER AIDS -- DUMP , CDUMP )
  1 
  2 BASE @ HEX
  3 
  4 
  5 
  6 
  7 
  8 : H. BASE @ HEX OVER U. BASE ! ;
  9 
 10 : B?   BASE @ DUP DECIMAL . BASE ! ;
 11 : FREE   2E5 @ HERE -  U. ." bytes" CR ;
 12 
 13 
 14 -->
 15 

SCR # 22 
  0 ( DEBUGGER AIDS -- DUMP , CDUMP )
  1     DECIMAL
  2 : ?EXIT  ?TERMINAL
  3          IF LEAVE ENDIF ;
  4 : U.R    0 SWAP D.R ;
  5 : LDMP  DUP 8 + SWAP DO I C@ 4 .R
  6          LOOP ;
  7 : DUMP   OVER + SWAP DO CR I 5 U.R I
  8          LDMP ?EXIT 8 +LOOP CR ;
  9 : CDMP   DUP 16 + SWAP DO
 10          I C@ EMIT LOOP ;
 11  HEX
 12 : CDUMP   OVER + SWAP DO CR I 5 U.R I
 13       SPACE 1 2FE C! CDMP 0 2FE C!
 14        ?EXIT 10 +LOOP CR ;
 15  DECIMAL -->

SCR # 23 
  0 ( STACK PRINTER )
  1 
  2 HEX
  3 
  4 : DEPTH SP@ 12 +ORIGIN @ SWAP - 2 / ;
  5 : S.  ( PRINTS THE STACK )
  6    DEPTH -DUP IF
  7       0 DO  CR  ." TOP+" I .
  8       SP@ I 2 * + @ U. LOOP
  9    ELSE ." Stack Empty" THEN CR ;
 10 
 11 
 12 
 13 BASE !
 14 
 15 -->

SCR # 24 
  0 ( DEFINITION TRACER )
  1      BASE @ HEX
  2 0 VARIABLE .WORD
  3 ' CLIT CFA CONSTANT .CLIT
  4 ' 0BRANCH CFA CONSTANT ZBRAN
  5 ' BRANCH CFA CONSTANT BRAN
  6 ' ;S CFA CONSTANT SEMIS
  7 ' (LOOP) CFA CONSTANT PLOOP
  8 ' (+LOOP) CFA CONSTANT PPLOOP
  9 ' (.") CFA CONSTANT PDOTQ
 10 : PWORD 2+ NFA ID.  ;
 11 : 1BYTE  PWORD .WORD @ C@ . 1 .WORD +! ;
 12 : 1WORD PWORD .WORD @ @  . 2 .WORD +! ;
 13 : NP DUP SEMIS = IF PWORD CR CR
 14     PROMPT QUIT THEN ?TERMINAL IF
 15      PROMPT QUIT THEN ;    -->

SCR # 25 
  0 ( DEFINITION TRACER )
  1 
  2 : BRNCH PWORD ." to " .WORD @ .WORD @ @ + . 2 .WORD +! ;
  3 
  4 : STG  PWORD 22 EMIT .WORD @   DUP COUNT TYPE 22 EMIT
  5    C@ .WORD @ + 1+ .WORD ! ;
  6 
  7 ' LIT CFA CONSTANT .LIT
  8 
  9 : CKIT DUP ZBRAN = OVER BRAN =
 10  OR OVER PLOOP = OR OVER PPLOOP =
 11 OR IF BRNCH ELSE DUP .LIT =
 12 IF 1WORD ELSE DUP .CLIT =
 13  IF 1BYTE ELSE DUP PDOTQ = IF STG
 14  ELSE PWORD THEN THEN THEN THEN ;
 15 -->

SCR # 26 
  0 ( DEFINITION TRACER )
  1     ' : 12 + CONSTANT DOCOL
  2 
  3 : T?PR CR CR ." Primitive" CR CR ;
  4 : ?DOCOL DUP 2 - @ DOCOL -  IF
  5   T?PR PROMPT QUIT THEN ;
  6 
  7 : .SETUP [COMPILE] ' ?DOCOL .WORD ! ;
  8 
  9 : NXT1  .WORD @ U. 2 SPACES .WORD
 10     @ @ 2 .WORD +! ;
 11 
 12 : DECOMP .SETUP CR CR BEGIN NXT1 NP
 13       CKIT CR AGAIN ;
 14 
 15 BASE !     ;S

SCR # 27 
  0 ( ** EDITOR ** )
  1 
  2  BASE @  HEX
  3 
  4 ( THIS EDITOR IS PATTERNED AFTER
  5 ( THE EXAMPLE EDITOR IN THE fig
  6 ( "INSTALLATION MANUAL" 8/80 WFR
  7 
  8 : TEXT HERE C/L 1+ BLANKS WORD
  9        HERE PAD C/L 1+ CMOVE ;
 10 
 11 : LINE DUP FFF0 AND 17 ?ERROR SCR
 12        @ (LINE) DROP ;
 13 
 14 : MARK  10 0 DO I LINE UPDATE
 15     DROP LOOP ;        -->

SCR # 28 
  0 ( EDITOR )
  1 VOCABULARY EDITOR IMMEDIATE
  2 : WHERE DUP B/SCR / DUP SCR ! ." SCR # " DECIMAL .
  3 SWAP C/L /MOD C/L * ROT BLOCK + CR C/L -TRAILING TYPE CR HERE
  4 C@ - SPACES 1 2FE C! 1C EMIT 0 2FE C! [COMPILE] EDITOR QUIT ;
  5 
  6 EDITOR DEFINITIONS
  7 
  8 : #LOCATE R# @ C/L /MOD ;
  9 : #LEAD #LOCATE LINE SWAP ;
 10 : #LAG  #LEAD DUP >R + C/L R> - ;
 11 
 12 
 13 : -MOVE LINE C/L CMOVE UPDATE ;
 14 
 15 -->

SCR # 29 
  0 ( EDITOR )
  1 : H LINE PAD 1+ C/L DUP PAD C!
  2      CMOVE ;
  3 : E LINE C/L BLANKS UPDATE ;
  4 : S DUP 1 - 0E DO I LINE I 1+
  5     -MOVE -1 +LOOP E ;
  6 : D DUP H 0F DUP ROT
  7     DO I 1+ LINE I -MOVE LOOP E ;
  8 
  9 
 10    -->
 11 
 12 
 13 
 14 
 15 

SCR # 30 
  0 ( EDITOR )
  1 
  2 : M   R# +! CR SPACE #LEAD TYPE
  3       17 EMIT #LAG TYPE #LOCATE
  4       . DROP ;
  5 : T   DUP C/L * R# ! DUP H 0 M ;
  6 : L   SCR @ LIST 0 M ;
  7 : R   PAD 1+ SWAP -MOVE ;
  8 : P   1 TEXT R ;
  9 : I   DUP S R ;
 10 : TOP   0 R# ! ;
 11 
 12 
 13   -->
 14 
 15 

SCR # 31 
  0 ( EDITOR )
  1 
  2 
  3 : CLEAR  SCR ! 10 0 DO FORTH I
  4          EDITOR E LOOP ;
  5 
  6 
  7 
  8 
  9 
 10 : COPY   B/SCR * OFFSET @ + SWAP
 11          B/SCR * B/SCR OVER +
 12          SWAP DO DUP FORTH I
 13          BLOCK 2 - ! 1+ UPDATE
 14          LOOP DROP FLUSH ;
 15   -->

SCR # 32 
  0 ( EDITOR )
  1 
  2 : 1LINE   #LAG PAD COUNT MATCH R#
  3           +! ;
  4 
  5 
  6 : FIND   BEGIN 3FF R# @ < IF TOP
  7          PAD HERE C/L 1+ CMOVE 0
  8          ERROR ENDIF 1LINE UNTIL
  9          ;
 10 
 11 : DELETE   >R #LAG + FORTH R -
 12        #LAG R MINUS R# +! #LEAD
 13        + SWAP CMOVE R> BLANKS
 14        UPDATE ;
 15 -->

SCR # 33 
  0 ( EDITOR )
  1 
  2 : N   FIND 0 M ;
  3 
  4 : F   1 TEXT N ;
  5 
  6 : B   PAD C@ MINUS M ;
  7 
  8 : X   1 TEXT FIND PAD C@ DELETE
  9       0 M ;
 10 
 11 : TILL   #LEAD + 1 TEXT 1LINE 0=
 12          0 ?ERROR #LEAD + SWAP -
 13          DELETE 0 M ;
 14 
 15 -->

SCR # 34 
  0 ( END OF EDITOR )
  1 
  2 : C   1 TEXT PAD COUNT #LAG ROT
  3       OVER MIN >R FORTH R R# +!
  4       R - >R DUP HERE R CMOVE
  5       HERE #LEAD + R> CMOVE R>
  6       CMOVE UPDATE 0 M ;
  7 
  8 
  9 FORTH DEFINITIONS DECIMAL
 10 
 11 LATEST 12 +ORIGIN !
 12 HERE 28 +ORIGIN !
 13 HERE 30 +ORIGIN !
 14 ' EDITOR 6 + 32 +ORIGIN !
 15 HERE FENCE !    BASE !    ;S

SCR # 35 
  0 
  1 
  2 
  3 
  4 
  5 
  6 
  7 
  8 
  9 
 10 
 11 
 12 
 13 
 14 
 15 

SCR # 36 
  0 ( DISK COPY ROUTINE  32K RAM )
  1 
  2    BASE @ DECIMAL
  3 16384 CONSTANT BUFHEAD
  4 0 VARIABLE BLK#  0 VARIABLE ADRS
  5 : GET   ADRS @ BLK# @ ;
  6 : RD    GET DUP 718 = IF LEAVE THEN 1 R/W ;
  7 : WRT   GET DUP 718  = IF LEAVE THEN  0 R/W ;
  8 : +BLK  1 BLK# +!  128 ADRS +! ;
  9 : DSETUP   BLK# ! BUFHEAD ADRS ! ;
 10 : GKEY ." HIT ANY KEY "  KEY CR DROP ;
 11 : RDIN  CR ." Insert SOURCE disk  "  GKEY DSETUP
 12 90 0 DO RD +BLK  LOOP ;
 13 : WRTO  CR ." Insert DESTINATION disk  "  GKEY DSETUP
 14 90 0 DO WRT +BLK  LOOP ;
 15 -->

SCR # 37 
  0 ( DISK COPY ROUTINE )
  1 
  2 ( INSERT SOURCE DISK IN DRIVE #1
  3 
  4 ( SIMPLY TYPE  "DISKCOPY" !
  5 
  6 : MS1 CR CR
  7 ." SINGLE-DRIVE DISK COPY" CR CR ;
  8 
  9 
 10 : %COPY      0 DO I 90 *
 11              DUP DUP RDIN WRTO
 12              90 +  . LOOP ;
 13 : DISKCOPY   CR MS1 CR 8 %COPY ;
 14 
 15 BASE !   ;S

SCR # 38 
  0 
  1 
  2 
  3 
  4 
  5 
  6 
  7 
  8 
  9 
 10 
 11 
 12 
 13 
 14 
 15 

SCR # 39 
  0 ( ** ASSEMBLER **   IN FORTH )
  1 
  2 (  ASSEMBLER COMFORMS TO THE
  3 ( fig "INSTALLATION GUIDE" WITH
  4 ( THE FOLLOWING EXCEPTIONS:
  5 
  6 (  SHIFTS ARE: "XXX.A" FOR A-REG.
  7 ( SHIFTS.
  8 (  CONDITIONAL BRANCHES ARE
  9 (  PATTERNED AFTER THE BRANCH OP-
 10 (  CODES:   "IFEQ," IS USED IN-
 11 ( STEAD OF "0= IF," FOR BETTER
 12 ( CLARITY.  SEE SCREEN 43.
 13 
 14 
 15 -->

SCR # 40 
  0 ( ASSEMBLER )
  1 
  2 VOCABULARY ASSEMBLER IMMEDIATE
  3 
  4 BASE @  HEX
  5 
  6 : CODE  [COMPILE] ASSEMBLER
  7         CREATE SMUDGE ;
  8 
  9 ASSEMBLER DEFINITIONS
 10 
 11 : SB  <BUILDS C, DOES> @ C, ;
 12       ( SINGLE BYTE OPERATORS)
 13 
 14 
 15 -->

SCR # 41 
  0 ( ASSEMBLER )
  1 
  2 00 SB BRK, 18 SB CLC, D8 SB CLD,
  3 58 SB CLI, B8 SB CLV, CA SB DEX,
  4 88 SB DEY, E8 SB INX, C8 SB INY,
  5 EA SB NOP, 48 SB PHA, 08 SB PHP,
  6 68 SB PLA, 28 SB PLP, 40 SB RTI,
  7 60 SB RTS, 38 SB SEC, F8 SB SED,
  8 78 SB SEI, A8 SB TAX, BA SB TSX,
  9 8A SB TXA, 9A SB TXS, 98 SB TYA,
 10 
 11 0A SB ASL.A,   2A SB ROL.A,
 12 4A SB LSR.A,   6A SB ROR.A,
 13 
 14 : NOT  0= ;  ( REVERSE LOGICAL )
 15 : 0=  1 ; ( PUSH A TRUE )  -->

SCR # 42 
  0 ( ASSEMBLER )
  1 
  2 : 3BY  <BUILDS C, DOES> @ C, , ;
  3 
  4 4C 3BY JMP,   6C 3BY JMP(),
  5 20 3BY JSR,
  6 
  7 : ?ER5    5 ?ERROR ;
  8 
  9 : IF.  <BUILDS C, DOES> C@ C, 0
 10         C, HERE ;
 11 : THEN,   DUP HERE SWAP - DUP
 12         7F > ?ER5 DUP -80 < ?ER5
 13   SWAP -1 + C! ;  IMMEDIATE
 14 : ENDIF, [COMPILE] THEN, ; IMMEDIATE
 15 -->

SCR # 43 
  0 ( ASSEMBLER )
  1 
  2 30 IF. IFPL,  ( BPL )
  3 10 IF. IFMI,  ( BMI )
  4 70 IF. IFVC,  ( BVC )
  5 50 IF. IFVS,  ( BVS )
  6 B0 IF. IFCC,  ( BCC )
  7 90 IF. IFCS,  ( BCS )
  8 F0 IF. IFNE,  ( BNE )
  9 D0 IF. IFEQ,  ( BEQ )
 10 
 11 : BEGIN,   HERE ; IMMEDIATE
 12 : END,   IF D0 ELSE F0 THEN  C,
 13          HERE 1+ - DUP
 14         -80 < ?ER5 C, ; IMMEDIATE
 15 : UNTIL,  [COMPILE]  END,  ; IMMEDIATE        -->

SCR # 44 
  0 ( ASSEMBLER )
  1 
  2 0D VARIABLE MODE ( ABS. MODE )
  3 
  4 : MODE=   MODE @ = ; ( CK MODE )
  5 : 256<   DUP 100 ( HEX) U< ;
  6 : MODEFIX  256< IF -08 MODE +!
  7            THEN ;
  8      ( MODE=MODE-8 IF ADR<256 )
  9 : CKMODE   MODE= IF MODEFIX
 10                  THEN ;
 11 : M0 <BUILDS C, DOES> SWAP
 12      0D CKMODE  1D CKMODE SWAP
 13      C@ MODE @ OR C,    256< IF
 14      C, ELSE , THEN 0D MODE ! ;
 15  DECIMAL  46 LOAD    ;S

SCR # 45 
  0 BjDISKNAMEDAT
  1 
  2 APX-20029fig-FORTH 1.1 Rev. 2.0Patrick L. Mullarky01/15/821
  3 J
  4 
  5 
  6 
  7 
  8 
  9 
 10 
 11 
 12 
 13 
 14 
 15 

SCR # 46 
  0 ( ASSEMBLER )
  1     HEX
  2 : X)  01 MODE ! ;   ( [ADDR,X]  )
  3 : #   09 MODE ! ;   ( IMMEDIATE )
  4 : )Y  11 MODE ! ;   ( [ADDR],Y  )
  5 : ,X  1D MODE ! ;   ( ADDR,X    )
  6 : ,Y  19 MODE ! ;   ( ADDR,Y    )
  7 
  8 
  9 00 M0 ORA, 20 M0 AND, 40 M0 EOR,
 10 60 M0 ADC, 80 M0 STA, A0 M0 LDA,
 11 C0 M0 CMP, E0 M0 SBC,
 12 
 13 : BIT,   256< IF 24 C, C, ELSE
 14          2C C, , THEN ;
 15 -->

SCR # 47 
  0 ( ASSEMBLER )
  1 
  2 : STOREADD  C, 256<  IF C, ELSE ,
  3             THEN 0D MODE ! ;
  4 
  5 : ZPAGE      OVER 100 < IF F7 AND
  6              THEN  ;
  7 : XYMODE  MODE @ 19 = MODE @ 1D
  8           = OR ;
  9 : M1  <BUILDS C, DOES> C@ MODE @
 10 : OPCODE  C@ ZPAGE XYMODE IF 10
 11           OR THEN ;
 12 : M2  <BUILDS C, DOES> OPCODE
 13       MODE @ 9 = IF 4 - THEN
 14       STOREADD ;
 15 

SCR # 48 
  0 AC M2 LDY,   AE M2 LDX,
  1 CC M2 CPY,   EC M2 CPX,
  2 
  3 : M3    <BUILDS C, DOES> OPCODE
  4         STOREADD ;
  5 
  6 8C M3 STY,    8E M3 STX,
  7 -->
  8 ( END OF ASSEMBLER )
  9 
 10 FORTH DEFINITIONS
 11 
 12 
 13 LATEST 0C +ORIGIN !  ( NTOP )
 14 
 15 HERE   1C +ORIGIN !  ( FENCE )

SCR # 49 
  0 
  1 HERE   1E +ORIGIN !  ( DP )
  2 
  3 
  4 
  5 
  6 
  7 BASE !      ;S
  8 ( COLOR COMMANDS )
  9 BASE @ HEX
 10 : SETCOLOR  2 * SWAP 10 * OR SWAP
 11           02C4 ( COLPF0 ) + C! ;
 12 : SE.  SETCOLOR ;  ( ALIAS )
 13 
 14 (  REGISTER#-3, COLOR-2, LUM-1
 15 

SCR # 50 
  0 (    0-3          0-F     0-7
  1 
  2 -->
  3 
  4 
  5 
  6 
  7 
  8 ( GRAPHICS COMMANDS )
  9 E456 CONSTANT CIO
 10   1C VARIABLE MASK
 11  340 CONSTANT IOCX
 12   53 VARIABLE SNAME
 13 
 14 CODE GR.  1 # LDA,  GFLAG STA,
 15          XSAVE STX,    0 ,X LDA,

SCR # 51 
  0  # 30 LDX,     IOCX 0B + ,X STA,
  1 # 3 LDA,  IOCX 2 + ,X STA,
  2 SNAME FF AND # LDA,  IOCX 4 + ,X
  3  STA,   SNAME 100 / # LDA,
  4 IOCX 5 + ,X STA,   MASK LDA,
  5 IOCX 0A + ,X STA,    CIO JSR,
  6 XSAVE LDX,   0 # LDY,  POP JMP,
  7 -->
  8 ( GRAPHICS COMMANDS )
  9 
 10 CODE &GR     XSAVE STX, # 30 LDX,
 11              # C LDA,  IOCX 2 +
 12              ,X STA,   CIO JSR,
 13              XSAVE LDX, 0 # LDA,
 14              GFLAG STA, NEXT JMP,
 15 

SCR # 52 
  0 : XGR  &GR  0 GR.  &GR ;
  1   ( EXIT GRAPHICS MODE )
  2 
  3 -->
  4 
  5 
  6 
  7 
  8 ( GRAPHICS I/O )
  9 
 10 CODE CPUT   0 ,X LDA,  PHA,
 11   XSAVE STX,  # 30 LDX,
 12   # B LDA,  IOCX 2 + ,X STA, TYA,
 13   IOCX 8 + ,X STA, IOCX 9 + ,X
 14   STA, PLA,  CIO JSR,  XSAVE LDX,
 15   POP JMP,

SCR # 53 
  0 
  1 54 CONSTANT ROWCRS
  2 55 CONSTANT COLCRS
  3 
  4 : POS  ROWCRS C! COLCRS ! ;
  5 : PLOT   POS CPUT ;
  6 
  7 -->
  8 ( GRAPHICS I/O )
  9 
 10 : GTYPE  -DUP IF OVER + SWAP
 11         DO I C@ CPUT LOOP ELSE
 12         DROP ENDIF ;
 13 
 14 : (G")  R COUNT DUP 1+ R> + >R
 15         GTYPE ;

SCR # 54 
  0 
  1 : G"  22 STATE @ IF COMPILE (G")
  2       WORD HERE C@ 1+ ALLOT
  3      ELSE WORD HERE COUNT GTYPE
  4      ENDIF  ; IMMEDIATE
  5 
  6 
  7 -->
  8 ( DRAW, FIL )
  9 
 10 2FB CONSTANT ATACHR
 11 2FD CONSTANT FILDAT
 12 
 13 CODE GCOM    XSAVE STX, 0 ,X LDA,
 14    # 30 LDX,  IOCX 2 + ,X STA,
 15    CIO JSR,  XSAVE LDX, POP JMP,

SCR # 55 
  0 
  1 : DRAW   POS ATACHR C! 11 GCOM ;
  2 
  3 : FIL  FILDAT C!  12 GCOM ;
  4 
  5 
  6 BASE ! ;S
  7 
  8 ( SOUND COMMANDS )
  9     BASE @ HEX
 10 
 11 D208 CONSTANT AUDCTL
 12 D200 CONSTANT AUDBASE
 13 
 14 : SOUND  ( CH# FREQ DIST VOL --- )
 15   3 DUP 0D20F C! 232 C!

SCR # 56 
  0   SWAP 16 * + ROT DUP + AUDBASE +
  1     ROT OVER C! 1+ C! ;
  2 
  3 : FILTER!  AUDCTL C! ;
  4    ( N --- )
  5 
  6 
  7 BASE ! ;S
  8 ( GRAPHICS TESTS )
  9 
 10 : BOX  0 10 10 PLOT  1 50 10 DRAW
 11        1 50 25 DRAW  1 10 25 DRAW
 12        1 10 10 DRAW ;
 13 
 14 : FBOX  XGR   5 GR.   BOX
 15       10 25 POS  2 FIL ;

SCR # 57 
  0 
  1 
  2 
  3 
  4 
  5 
  6 
  7 
  8 ( DOS OBJECT READER )
  9 
 10 BASE @ HEX
 11 
 12 0 VARIABLE BLOCK#  0 VARIABLE BYTES  0 VARIABLE BYTPTR
 13 0 VARIABLE ADDRSS  0 VARIABLE #BYTES
 14 : GETCOUNT  7F + C@ 7F AND  BYTES ! 0 BYTPTR ! ;
 15 : FNEXTBLK  7D + DUP C@ 100 * SWAP 1+ C@ + 3FF AND 1 - ;

SCR # 58 
  0 : LINKBLOCK  FNEXTBLK
  1   DUP BLOCK# ! DUP 0 > IF BLOCK THEN ;
  2 : BLK-CK  BYTES @ 0= IF BLOCK# @ BLOCK LINKBLOCK
  3   GETCOUNT THEN ;
  4 : NEXTBYTE  BLK-CK -1 BYTES +! BYTPTR @ 1 BYTPTR +!
  5 BLOCK# @ BLOCK + C@ ;
  6 : NEXTWORD  NEXTBYTE NEXTBYTE 100 * + ;
  7 -->
  8 ( DOS OBJECT READER )
  9 
 10 : ADRCALC  NEXTWORD DUP ADDRSS ! NEXTWORD SWAP - 1+  #BYTES ! ;
 11 
 12 : BLOCKSET  DUP BLOCK# ! BLOCK GETCOUNT ;
 13 
 14 : LOADOBJ  BLOCKSET  NEXTWORD 1+ IF CR ." Not an Object file"
 15  CR QUIT THEN

SCR # 59 
  0     BEGIN
  1          ADRCALC
  2         #BYTES @ 0 DO NEXTBYTE ADDRSS @ C! 1 ADDRSS +! LOOP
  3         BLOCK# @ BLOCK FNEXTBLK
  4    1+ 0= BYTES @ 0= AND   END ;
  5 
  6 
  7 BASE ! ;S
  8 ( FLOATING POINT WORDS )
  9  BASE @  HEX
 10 : FDROP   DROP DROP DROP ;
 11 : FDUP    >R >R DUP R> DUP ROT
 12           SWAP R ROT ROT R> ;
 13 CODE FSWAP
 14   XSAVE STX, # 6 LDY,
 15 BEGIN,  0 ,X LDA, PHA, INX, DEY,

SCR # 60 
  0 0= END, XSAVE LDX,  # 6 LDY,
  1 BEGIN, 6 ,X LDA,  0 ,X STA, INX,
  2 DEY, 0= END, XSAVE LDX,  # 6 LDY,
  3  BEGIN, PLA, 0B ,X STA, DEX, DEY,
  4 0= END,   XSAVE LDX,  NEXT JMP,
  5 
  6 XSAVE 100 * 86 + CONSTANT XSAV
  7 : XS,   XSAV ,  ;       -->
  8 ( FLOATING POINT WORDS )
  9 CODE FOVER     DEX, DEX, DEX,
 10  DEX, DEX, DEX, XSAVE STX,
 11  # 6 LDY,  BEGIN,  0C ,X LDA,
 12  0 ,X STA, INX, DEY, 0= END,
 13  XSAVE LDX,  NEXT JMP,
 14 
 15 XSAVE 100 * A6 + CONSTANT XLD

SCR # 61 
  0 : XL,   XLD  ,  ;
  1 
  2 CODE AFP   XS, D800 JSR, XL, NEXT JMP,
  3 CODE FASC  XS, D8E6 JSR, XL, NEXT JMP,
  4 CODE IFP   XS, D9AA JSR, XL, NEXT JMP,    -->
  5 
  6 
  7 
  8 ( FLOATING POINT WORDS )
  9 
 10 CODE FPI   XS, D9D2 JSR, XL, NEXT JMP,
 11 CODE FADD  XS, DA66 JSR, XL, NEXT JMP,
 12 CODE FSUB  XS, DA60 JSR, XL, NEXT JMP,
 13 CODE FMUL  XS, DADB JSR, XL, NEXT JMP,
 14 CODE FDIV  XS, DB28 JSR, XL, NEXT JMP,
 15 CODE FLG  XS, DECD JSR, XL, NEXT JMP,

SCR # 62 
  0 CODE FLG10 XS, DED1 JSR, XL, NEXT JMP,
  1 CODE FEX  XS, DDC0 JSR, XL, NEXT JMP,
  2 CODE FEX10 XS, DDCC JSR, XL, NEXT JMP,
  3 CODE FPOLY XS, DD40 JSR, XL, NEXT JMP,
  4   -->
  5 
  6 
  7 
  8 ( FLOATING POINT WORDS )
  9 
 10 D4 CONSTANT FR0
 11 E0 CONSTANT FR1
 12 FC CONSTANT FLPTR
 13 F3 CONSTANT INBUF
 14 F2 CONSTANT CIX
 15 

SCR # 63 
  0 -->
  1 
  2 
  3 
  4 
  5 
  6 
  7 
  8 ( FLOATING POINT )
  9 
 10 : F@ >R R @ R 2+ @ R> 4 + @ ;
 11 : F! >R R 4 + ! R 2+ ! R> ! ;
 12 
 13 : F.TY  BEGIN INBUF @ C@ DUP
 14        7F AND EMIT 1 INBUF +!
 15        80 > UNTIL ;

SCR # 64 
  0 
  1 
  2 : F. FR0 F@ FSWAP FR0 F! FASC
  3     F.TY SPACE FR0 F! ;
  4 : F?   F@ F. ;
  5 
  6 -->
  7 
  8 ( FLOATING POINT )
  9 
 10 : <F    FR1 F! FR0 F! ;
 11 : F>  FR0 F@ ;
 12 : FS  FR0 F! ;
 13 
 14 : F+   <F FADD F> ;
 15 : F-   <F FSUB F> ;

SCR # 65 
  0 : F*   <F FMUL F> ;
  1 : F/   <F FDIV F> ;
  2 : FLOAT   FR0 ! IFP F> ;
  3 : FIX   FS FPI FR0 @ ;
  4 : FLOG   FS FLG F> ;
  5 : FLOG10 FS FLG10 F> ;
  6 : FEXP  FS FEX F> ;
  7 : FEXP10 FS FEX10 F> ;  -->
  8 ( FLOATING POINT )
  9 
 10 : ASCF 0 CIX ! INBUF ! AFP F> ;
 11 
 12 : FLIT R> DUP 6 + >R F@ ;
 13 : FLITERAL STATE @ IF
 14   COMPILE FLIT HERE F! 6 ALLOT
 15   ENDIF ;

SCR # 66 
  0 : FLOATING  ( FLOAT FOLLOWING CONSTANT )
  1    BL WORD HERE 1+ ASCF
  2    FLITERAL ;  IMMEDIATE
  3 ( EX:  FLOATING 1.2345 )
  4 ( OR   FLOATING  -1.67E-13 )
  5 
  6 : FP [COMPILE] FLOATING ;
  7 IMMEDIATE     -->
  8 ( FLOATING POINT )
  9 
 10 : FVARIABLE
 11  <BUILDS HERE F! 6 ALLOT DOES> ;
 12 
 13 : FCONSTANT
 14   <BUILDS HERE F! 6 ALLOT DOES>
 15   F@ ;

SCR # 67 
  0 
  1 : F0=   OR OR 0= ;
  2 : F=    F- F0= ;
  3 : F<    F- DROP DROP 80 AND 0 > ;
  4 
  5 
  6 
  7 BASE !  ;S
  8 
  9 
 10 
 11 
 12 
 13 
 14 
 15 

SCR # 68 
  0 
  1 
  2 
  3 
  4 
  5 
  6 
  7 
  8 ( FORTH INC.'S EDITOR )
  9 
 10 ( This editor was written by S.H. Daniel, in FORTH DIMENSIONS,
 11 ( Volume III, number 3.
 12 
 13 ( The only change was to make the cursor a "block" for higher
 14 ( visibility.  P. Mullarky 9/29/81
 15 

SCR # 69 
  0 -->
  1 
  2 
  3 
  4 
  5 
  6 
  7 
  8 ( FORTH INC.'S EDITOR )
  9 
 10 BASE @ FORTH DEFINITIONS HEX
 11 
 12 : TEXT HERE C/L 1+ BLANKS WORD HERE PAD C/L 1+ CMOVE ;
 13 : LINE DUP FFF0 AND 17 ?ERROR SCR @ (LINE) DROP ;
 14 VOCABULARY EDITOR IMMEDIATE
 15 : WHERE DUP B/SCR / DUP SCR ! ." SCR # " DECIMAL . SWAP

SCR # 70 
  0 C/L /MOD C/L * ROT BLOCK + CR C/L TYPE [COMPILE] EDITOR QUIT ;
  1 EDITOR DEFINITIONS
  2 : #LOCATE R# @ C/L /MOD ;
  3 : #LEAD #LOCATE LINE SWAP ;
  4 : #LAG #LEAD DUP >R + C/L R> - ;
  5 : -MOVE LINE C/L CMOVE UPDATE ;
  6 : BUF-MOVE PAD 1+ C@ IF PAD SWAP C/L 1+ CMOVE ELSE DROP THEN ;
  7 : >LINE# #LOCATE SWAP DROP ;  -->
  8 ( FORTH INC.'S EDITOR )
  9 
 10 : FIND-BUF PAD 50 + ;
 11 : INSERT-BUF FIND-BUF 50 + ;
 12 : (HOLD) LINE INSERT-BUF 1+ C/L DUP INSERT-BUF C! CMOVE ;
 13 : (KILL) LINE C/L BLANKS UPDATE ;
 14 : (SPREAD) >LINE# DUP 1 - E DO I LINE I 1+ -MOVE -1
 15 +LOOP (KILL) ;

SCR # 71 
  0 : X >LINE# DUP (HOLD) F DUP ROT DO I 1+ LINE I -MOVE
  1 LOOP (KILL) ;
  2 : DISPLAY-CURSOR CR SPACE #LEAD TYPE A0 EMIT #LAG TYPE
  3 #LOCATE . DROP ;
  4 : T C/L * R# ! 0 DISPLAY-CURSOR ;
  5 : L SCR @ LIST ;
  6 : N 1 SCR +! ;
  7 : B -1 SCR +! ;      -->
  8 ( FORTH INC.'S EDITOR )
  9 
 10 : (TOP) 0 R# ! ;
 11 : SEEK-ERROR (TOP) FIND-BUF HERE C/L 1+ CMOVE HERE COUNT TYPE
 12 ."  None" QUIT ;
 13 : (R) >LINE# INSERT-BUF 1+ SWAP -MOVE ;
 14 : P 5E TEXT INSERT-BUF BUF-MOVE (R) ;
 15 : WIPE 10 0 DO I (KILL) LOOP ;

SCR # 72 
  0 : COPY B/SCR * OFFSET @ + SWAP B/SCR * B/SCR OVER + SWAP DO DUP
  1 FORTH I BLOCK 2 - ! 1+ UPDATE LOOP DROP FLUSH ;
  2 : 1LINE #LAG FIND-BUF COUNT MATCH R# +! ;
  3 : (SEEK) BEGIN 3FF R# @ < IF SEEK-ERROR THEN 1LINE UNTIL ;
  4 : (DELETE) >R #LAG + R - #LAG R MINUS R# +! #LEAD + SWAP
  5 CMOVE R> BLANKS UPDATE ;
  6 : (F) 5E TEXT FIND-BUF BUF-MOVE (SEEK) ;
  7 : F (F) DISPLAY-CURSOR ;   -->
  8 ( FORTH INC.'S EDITOR )
  9 : (E) FIND-BUF C@ (DELETE) ;
 10 : E (E) DISPLAY-CURSOR ;
 11 : D (F) E ;
 12 : TILL #LEAD + 5E TEXT FIND-BUF BUF-MOVE 1LINE 0= IF
 13 SEEK-ERROR THEN #LEAD + SWAP - (DELETE) DISPLAY-CURSOR ;
 14 0 VARIABLE COUNTER
 15 : BUMP 1 COUNTER 1+ COUNTER @ 38 > IF 0 COUNTER ! CR CR

SCR # 73 
  0 F MESSAGE C EMIT THEN ;
  1 : S C EMIT 5E TEXT 0 COUNTER ! FIND-BUF BUF-MOVE SCR @ DUP
  2 >R DO I SCR ! (TOP) BEGIN 1LINE IF DISPLAY-CURSOR SCR ? BUMP
  3 THEN 3FF R# @ < UNTIL LOOP R> SCR ! ;
  4 : I 5E TEXT INSERT-BUF BUF-MOVE INSERT-BUF COUNT #LAG ROT
  5 OVER MIN >R R R# +! R - >R DUP HERE R CMOVE HERE #LEAD + R>
  6 CMOVE R> CMOVE UPDATE
  7 DISPLAY-CURSOR ;     -->
  8 ( FORTH INC.'S EDITOR )
  9 
 10 : U C/L R# +! (SPREAD) P ;
 11 : R (E) I ;
 12 : M SCR @ >R R# @ >R >LINE# (HOLD) SWAP SCR ! 1+ C/L * R#
 13 (SPREAD) (R) R> C/L + R# R> SCR ! ;
 14 
 15 

SCR # 74 
  0 DECIMAL
  1 LATEST 12 +ORIGIN !
  2 HERE 28 +ORIGIN !
  3 HERE 30 +ORIGIN !
  4 ' EDITOR 6 + 32 +ORIGIN !
  5 HERE FENCE !
  6 FORTH DEFINITIONS  BASE !  FORTH ;S
  7 
  8 ( RAGSDALE ASSEMBLER )
  9 
 10 ( This assembler was published in Dr. Dobbs Journal V.6 N.9
 11       ( Sept. '81 )
 12 ( ... and is the assembler used in the fig "Installation Guide."
 13 
 14 
 15 

SCR # 75 
  0 
  1 
  2 -->
  3 
  4 
  5 
  6 
  7 
  8 ( RAGSDALE ASSEMBLER )
  9 VOCABULARY ASSEMBLER IMMEDIATE ASSEMBLER DEFINITIONS BASE @ HEX
 10 
 11 0 VARIABLE INDEX -2 ALLOT 0909 , 1505 , 0115 , 8011 , 8009 ,
 12 1D0D , 8019 , 8080 , 0080 , 1404 , 8014 , 8080 , 8080 ,
 13 1C0C , 801C , 2C80 ,
 14 2 VARIABLE MODE : .A 0 MODE ! ; : # 1 MODE ! ; : MEM 2 MODE ! ;
 15 : ,X 3 MODE ! ; : ,Y 4 MODE ! ; : X) 5 MODE ! ; : )Y 6 MODE ! ;

SCR # 76 
  0 : ) F MODE ! ; : BOT ,X 0 ; : SEC ,X 2 ; : RP) ,X 101 ;
  1 : UPMODE IF MODE @ 8 AND 0= IF 8 MODE +! THEN THEN
  2 1 MODE @ F AND -DUP IF 0 DO DUP + LOOP THEN OVER 1+ @ AND 0= ;
  3 : CPU <BUILDS C, DOES> C@ C, MEM ;
  4 00 CPU BRK, 18 CPU CLC, D8 CPU CLD, 58 CPU CLI, B8 CPU CLV,
  5 CA CPU DEX, 88 CPU DEY, E8 CPU INX, C8 CPU INY, EA CPU NOP,
  6 48 CPU PHA, 08 CPU PHP, 68 CPU PLA, 28 CPU PLP, 40 CPU RTI,
  7 60 CPU RTS, 38 CPU SEC, F8 CPU SED, 78 CPU SEI, AA CPU TAX, -->
  8 ( RAGSDALE ASSEMBLER )
  9 A8 CPU TAY, BA CPU TSX, 8A CPU TXA, 9A CPU TXS, 98 CPU TYA,
 10 : MCP <BUILDS C, , DOES> DUP 1+ @ 80 AND IF 10 MODE +! THEN
 11 OVER FF00 AND UPMODE UPMODE IF MEM CR LATEST ID. 3 ERROR THEN
 12 C@ MODE C@ INDEX + C@ + C, MODE C@ 7 AND IF MODE C@ F AND 7 <
 13 IF C, ELSE , THEN THEN MEM ;
 14 1C6E 60 MCP ADC, 1C6E 20 MCP AND, 1C6E C0 MCP CMP,
 15 1C6E 40 MCP EOR, 1C6E A0 MCP LDA, 1C6E 00 MCP ORA,

SCR # 77 
  0 1C6E E0 MCP SBC, 1C6C 80 MCP STA, 0D0D 01 MCP ASL,
  1 0C0C C1 MCP DEC, 0C0C E1 MCP INC, 0D0D 41 MCP LSR,
  2 0D0D 21 MCP ROL, 0D0D 61 MCP ROR, 0414 81 MCP STX,
  3 0486 E0 MCP CPX, 0486 C0 MCP CPY, 1496 A2 MCP LDX,
  4 0C8E A0 MCP LDY, 048C 80 MCP STY, 0480 14 MCP JSR,
  5 8480 40 MCP JMP, 0484 20 MCP BIT,
  6 : BEGIN, HERE 1 ; IMMEDIATE
  7 : UNTIL, ?EXEC >R 1 ?PAIRS R> C, HERE 1+ - C, ; IMMEDIATE -->
  8 ( RAGSDALE ASSEMBLER )
  9 : IF, C, HERE 0 C, 2 ; IMMEDIATE
 10 : THEN, ?EXEC 2 ?PAIRS HERE OVER C@ IF SWAP ! ELSE OVER 1+
 11 - SWAP C! THEN ;  IMMEDIATE
 12 : ELSE, 2 ?PAIRS HERE 1+ 1 JMP, SWAP HERE OVER 1+ - SWAP C!
 13 2 ;  IMMEDIATE
 14 : NOT 20 + ;
 15 90 CONSTANT CS D0 CONSTANT 0= 10 CONSTANT 0< 90 CONSTANT >=

SCR # 78 
  0 
  1 : END-CODE CURRENT @ CONTEXT ! ?EXEC ?CSP SMUDGE ;  IMMEDIATE
  2 FORTH DEFINITIONS DECIMAL
  3 : CODE ?EXEC CREATE [COMPILE] ASSEMBLER ASSEMBLER MEM !CSP ;
  4 IMMEDIATE
  5 ' ASSEMBLER CFA ' ;CODE 8 + ! LATEST 12 +ORIGIN !
  6 HERE 28 +ORIGIN ! HERE 30 +ORIGIN ! HERE FENCE !
  7 ' ASSEMBLER 6 + 32 +ORIGIN !     BASE ! FORTH ;S
  8 
  9 
 10 
 11 
 12 
 13 
 14 
 15 

SCR # 79 
  0 
  1 
  2 
  3 
  4 
  5 
  6 
  7 
  8 ( TEST SCREEN )
  9 
 10 123 456 XXX 789 123
 11 
 12 
 13 
 14 
 15 

SCR # 80 
  0 
  1 
  2 
  3 
  4 
  5 
  6 
  7 
  8 ( DOS I/O )
  9 BASE @ HEX
 10 340 VARIABLE IOCB   0 VARIABLE IO.X   0 VARIABLE IO.CH
 11 : IOCC   10 * 70 MIN DUP IO.X C! 340 + IOCB !  ;
 12 : <IO>  <BUILDS , DOES> @ IOCB @ + ;
 13 2 <IO> ICCOM  3 <IO> ICSTA  4 <IO> ICBAL  8 <IO> ICBLL
 14 A <IO> ICAX1  B <IO> ICAX2  C <IO> ICAX3  D <IO> ICAX4
 15 E <IO> ICAX5  F <IO> ICAX6

SCR # 81 
  0 
  1 CODE XCIO  XSAVE STX, IO.X LDX, IO.CH LDA, E456 JSR,
  2 XSAVE LDX, IO.CH STA, TYA, PUSH0A JMP,
  3 
  4 : OPEN  IOCC ICAX2 C! ICAX1 C! ICBAL ! 03 ICCOM C! XCIO ;
  5 : CLOSE  IOCC 0C ICCOM C! XCIO ;
  6 : PUTC  IOCC IO.CH C! 0B ICCOM C! XCIO ;
  7 : GETC  IOCC 7 ICCOM C! XCIO IO.CH C@ SWAP ;   -->
  8 ( DOS I/O )
  9 : GETREC  IOCC 5 ICCOM C! ICBLL ! ICBAL ! XCIO ;
 10 : PUTREC  IOCC 9 ICCOM C! ICBLL ! ICBAL ! XCIO ;
 11 : STATUS  IOCC ICSTA C@ ;
 12 : DEVSTAT  IOCC 0D ICCOM C! XCIO >R 2EA @ 2EC @ R> ;
 13 : SPECIAL IOCC ICCOM C! ICAX6 C! ICAX5 C! ICAX4 C! ICAX3 C!
 14 ICAX2 C! ICAX1 C! XCIO ;
 15 : FORMAT  CR CR ." Input Drive # " KEY DUP EMIT 30 -

SCR # 82 
  0 1 MAX 4 MIN
  1 CR CR ." When you hit RETURN I'm going to" CR ." FORMAT Drive "
  2 DUP . CR CR ." Hit any other key to abort  " BEEP KEY
  3 9B = IF (FMT) 1 = CR CR ." Format " IF ." OK" ELSE ." ERROR"
  4 THEN ELSE DROP THEN CR CR ;
  5 BASE ! ;S
  6 
  7 
  8 ( ATARI-850  DOWNLOAD )
  9 BASE @ HEX
 10 CODE DO-SIO
 11   XSAVE STX, 0 # LDA,   E459 JSR,
 12   XSAVE LDX,   NEXT JMP,
 13 : SET-DCB   50 300 C!  1 301 C!  3F 302 C! 40 303 C! 500 304 !
 14   5 306 C!  0 307 C!  C 308 C!  0 309 ! 0 30B C! ;
 15 

SCR # 83 
  0 CODE RELOCATE  XSAVE STX, 506 JSR, HERE 8 + JSR,  XSAVE LDX,
  1   NEXT JMP,  0C JMP(),
  2 
  3  : BOOT850    HERE 2E7 !  SET-DCB  DO-SIO
  4 500 300 0C CMOVE DO-SIO RELOCATE
  5 2E7 @ HERE - ALLOT HERE FENCE ! ;
  6 BASE ! ;S
  7 
  8 
  9 
 10 
 11 
 12 
 13 
 14 
 15 

SCR # 84 
  0 
  1 
  2 
  3 
  4 
  5 
  6 
  7 
  8 ( "STARTING FORTH" CHANGES )
  9     BASE @   DECIMAL
 10 : VARIABLE  0 VARIABLE ;
 11 : 'S SP@ ;  : S0 18 +ORIGIN @ ;
 12 : 1- 1 - ;  : 2- 2 - ;  : 2* DUP + ;  : 2/ 2 / ; : NOT 0= ;
 13 : I' R> R> R ROT ROT >R >R ;
 14 : J R> R> R> R R# ! >R >R >R R# @ ;
 15 : PAGE 125 EMIT ;

SCR # 85 
  0 : 2VARIABLE VARIABLE 0 , ;  : EXIT R> ;  : H DP ;
  1 : 2CONSTANT <BUILDS HERE D! 4 ALLOT DOES> D@ ;
  2 : CREATE VARIABLE -2 ALLOT ; : 2@ D@ ; : 2! D! ;
  3 : >IN IN ;  : /LOOP [COMPILE] LOOP ; IMMEDIATE
  4 : ['] [COMPILE] ' ; : WITHIN >R 1- OVER < SWAP R> < AND ;
  5 : NUMPATCH DROP 58 OVER = SWAP 44 48 WITHIN OR NOT ;
  6 : NUMFIX ' NUMPATCH CFA ' NUMBER 52 + ! ; NUMFIX
  7 -->
  8 ( "STARTING FORTH" CHANGES )
  9 
 10 : ABORT"   STATE @ IF COMPILE 0BRANCH HERE 0 ,
 11 COMPILE (.") ASCII " WORD HERE C@ 1+
 12 
 13 ALLOT COMPILE QUIT HERE OVER - SWAP !
 14 ELSE IF ASCII " WORD HERE COUNT TYPE
 15 QUIT THEN THEN ; IMMEDIATE

SCR # 86 
  0 
  1  BASE !    ;S
  2 
  3 
  4 
  5 
  6 
  7 
  8 ( DDISK )
  9 BASE @ HEX
 10 0 VARIABLE CBLOCK   0 VARIABLE BUFF
 11 : .HEAD 7D EMIT ." Enter BLOCK number in hex: " QUERY
 12 BL WORD HERE NUMBER DROP CR ;
 13 : GBLK .HEAD CR CR CBLOCK ! ;
 14 : RBLOCK CBLOCK @ BLOCK DUP BUFF ! ;
 15 

SCR # 87 
  0 : .H  0 <# # # #> TYPE SPACE ;
  1 : DLINE  8 0 DO DUP I + C@  .H LOOP ;
  2 : C.ON 1 2FE C! ;  : C.OFF 0 2FE C! ;
  3 : DCHAR C.ON 8 0 DO DUP I + C@ DUP 9B = IF DROP BL THEN
  4 EMIT LOOP C.OFF ;
  5 
  6 : FQUIT  DROP 7D EMIT ." ALL DONE" CR DECIMAL  PROMPT QUIT ;
  7 -->
  8 ( DDISK )
  9  HEX  : D.LINE DLINE SPACE DCHAR  ;
 10 : D.BLOCK  3 54 C! 2 55 ! ." BLOCK " CBLOCK @ . CR  RBLOCK
 11  80 0 DO I .H DUP I + D.LINE DROP CR 8 +LOOP DROP  ;
 12 : PBLK CBLOCK +! D.BLOCK ;
 13 : +BLOCK 1 PBLK ;
 14 : -BLOCK -1 PBLK ;
 15 

```
  
  
