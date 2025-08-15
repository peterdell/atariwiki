---
title: Copy OS ROM to RAM
---
# Copy OS ROM to RAM  
  
by Russ Gilbert, found in comp.sys.atari.8bit  
  
```
'MOVEOS.M65'
10       .TITLE      MOVE OS TO RAM
20       .OPT OBJ
30       *=  $8000
40 START LDA #0
50       STA $022F   TURN OFF ANTIC
60       STA $D40E
70       STA $D20E   DISABLE INTRPTS
80       SEI         MAKE SURE NO
90       LDA #$C0    INTERRUPTS
0100     STA $C1     SET UP BANK AREA
0110     LDY #0
0120     STY $C0
0130 L3  LDA ($C0),Y GET ROM BYTE
0140     TAX 
0150     LDA #$FE
0160     AND $D301   CLR BIT 0 TO
0170     STA $D301   BANK TO OS RAM
0180     TXA 
0190     STA ($C0),Y STORE BYTE
0200     LDA #$01
0210     ORA $D301
0220     STA $D301   BACK TO ROM
0230     INY         GET READY NEXT
0240     CPY #0
0250     BNE L3      256 TIMES
0260 NOK INC $C1
0270     CLC         DON'T UNDRSTND
0280     LDA $C1     THIS CNTRL LOOP
0290     CMP #$D0
0300     BCC T1      FROM $C0-$FF
0310     CMP #$D8    SKIP $D0-$D7
0320     BCC NOK
0330 T1  CMP #$00
0340     BNE L3
0350     CLC 
0360     LDA #$FF
0370     STA $D40E
0380     LDA #$F7
0390     STA $D20E   TURN ON NMI,IRQ
0400     LDA #$22
0410     STA $022F
0420     CLI 
0430     RTS 
0440     .END 
**************
```
  
Russ Gilbert  
