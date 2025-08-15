---
title: HDI Interface
---
# High-Density Disk Interface  
  
The HDI is the interface for connecting up to 4 standard  
drives to the XL/XE. You can mix 3,5" and 5,25" floppies at will.  
Required is that the drive supports the Disk Change signal at pin 34 of  
the Shugart bus. It doesn't support Medium Density (128 bytes/sector in  
MFM mode and 1.2 MB drives). Maximum transfer rate: 500 Kbit/s (1.44  
MByte disks).  
  
The HDI has been developed in 1991 by Erhard Pütz (FloppyDoc).  
  
![](attachments/hdi.jpg)  
  
[HDI-CAS.jpg](attachments/HDI-CAS.jpg)  
  
## Manual:  
  
HDI Manual: [HDI_Manual.pdf](attachments/HDI_Manual.pdf)  
  
  
HDI Schematics [sch_hdi.png](attachments/sch_hdi.png) (PDF: [sch_hdi.pdf](attachments/sch_hdi.pdf))  
  
  
  
# HDI High Speed SIO  
```
01000 * High-Speed SIO-Driver, will
01010 * be relocated by HDI and
01020 * send to computer.
01030 ;
01040 USIOA    LDA $0301     ;DUNIT
01050          BNE SIO2
01060          LDX #$08
01070 DLWTBLL  STA LWTBL-1,X ;$F614
01080          DEX
01090          BNE DLWTBLL
01100          RTS
01110 SIO2     TAX
01120 REL01    LDA LWTBL-1,X ;$F614
01130          BNE SIO3
01140          LDA #$28
01150 REL02    STA LWTBL-1,X ;$F614
01160          LDY #$07
01170 SIOCL    LDA $0302,Y   ;DCOMND
01180          PHA
01190 REL03    LDA C3F,Y     ;$F60D
01200          STA $0302,Y   ;DCOMND
01210          DEY
01220          BPL SIOCL
01230 REL04    JSR SIO3      ;$F450
01240          LDX $0301     ;DUNIT
01250          LDY $0303     ;DSTATS
01260          BMI SIO21
01270          LDA $01
01280 REL05    STA LWTBL-1,X ;$F614
01290 SIO21    LDY #$00
01300 SIO21CL  PLA
01310          STA $0302,Y   ;DCOMND
01320          INY
01330          CPY #$08
01340          BCC SIO21CL
01350 SIO3     SEI
01360          TXA
01370          ORA #$30
01380          STA $023A     ;CDEVIC
01390          LDA $0302     ;DCOMND
01400          STA $023B     ;CCOMND
01410          LDA $030A     ;DAUX1
01420          STA $023C     ;CAUX1
01430          LDA $030B     ;DAUX2
01440          STA $023D     ;CAUX2
01450 REL06    LDA LWTBL-1,X ;$F614
01460          STA $D204     ;AUDF3
01470          TSX
01480          STX $3F       ;FEOF
01490          LDA #$02
01500          STA $37       ;DRETRY
01510 IO11     LDA #$07
01520          STA $36       ;CRETRY
01530 IO12     LDA #$34
01540          STA $D303
01550          LDA #$00
01560          STA $30       ;STATUS
01570          STA $3E       ;FTYPE
01580          STA $35       ;BUFEND+1
01590          STA $D206     ;AUDF4
01600          LDA #$3A
01610          STA $32       ;BUFADR
01620          LDA #$02
01630          STA $33       ;BUFADR+1
01640          ASL
01650          STA $34       ;BUFEND
01660 REL07    JSR SEND1     ;$F4DC
01670          LDA $0304     ;DBUFLO
01680          STA $32       ;BUFADR
01690          LDA $0305     ;DBUFHI
01700          STA $33       ;BUFADR+1
01710          LDA $0308     ;DBYTLO
01720          STA $34       ;BUFEND
01730          LDA $0309     ;DBYTHI
01740          STA $35       ;BUFEND+1
01750          LDA $0303     ;DSTATS
01760          BPL IO2
01770 REL08    JSR SEND1     ;$F4DC
01780 IO2      DEC $3E       ;FTYPE
01790 REL09    JSR SETTI1    ;$F544
01800          BIT $0303     ;DSTATS
01810          BVC IO3
01820 REL10    JSR GETA1     ;$F521
01830 IO3      LDA #$A0
01840          STA $D207     ;AUDC4
01850          LDA $10
01860          STA $D20E     ;IRQEN
01870 REL11    JSR CLRTI1    ;$F576
01880          LDA $30       ;STATUS
01890          BEQ IO4
01900          DEC $37       ;DRETRY
01910          BNE IO11
01920 IO4      TAY
01930          BNE IO5
01940          INY
01950 IO5      STY $0303     ;DSTATS
01960          CLI
01970          RTS
01980 SEND1    LDY #$00
01990 SE1      INY
02000          BNE SE1
02010          LDA #$23
02020 REL12    JSR POKEY     ;$F5F7
02030          LDA ($32),Y   ;BUFADR
02040          STA $31       ;CHKSUM
02050          STA $D20D     ;SEROUT
02060          INY
02070          BNE SE3
02080 SE2      LDA ($32),Y   ;BUFADR
02090 REL13    JSR PUTBYTE   ;$F5D4
02100          INY
02110          BNE SE3
02120          INC $33       ;BUFADR+1
02130          DEC $35       ;BUFEND+1
02140          LDX #$E0
02150 SEWL     INX
02160          BNE SEWL
02170 SE3      CPY $34       ;BUFEND
02180          BNE SE2
02190          LDA $35       ;BUFEND+1
02200          BNE SE2
02210          LDA $31       ;CHKSUM
02220 REL14    JSR PUTBYTE   ;$F5D4
02230 SEO1     LDA $D20E     ;IRQST
02240          AND #$08
02250          BNE SEO1
02260          LDY #$03
02270 REL15    JSR STOUTX0   ;$F578
02280          LDA #$C0
02290          STA $D20E     ;IRQEN
02300          BNE RDQUIT
02310 GETA1    LDY #$00
02320          STY $31       ;CHKSUM
02330 GE1      JSR GETBYTE   ;$F5B1
02340          STA ($32),Y   ;BUFADR
02350 REL16    JSR ADDSUM    ;$F5EF
02360          INY
02370          BNE GE2
02380          INC $33       ;BUFADR+1
02390          DEC $35       ;BUFEND+1
02400 GE2      CPY $34       ;BUFEND
02410          BNE GE1
02420          LDA $35       ;BUFEND+1
02430          BNE GE1
02440 REL17    JSR GETBYTE   ;$F5B1
02450          CMP $31       ;CHKSUM
02460          BNE ERR8F
02470          RTS
02480 SETTI1   LDA $0306     ;DTIMLO
02490          ROR
02500          ROR
02510          TAY
02520          AND #$3F
02530          TAX
02540          TYA
02550          ROR
02560          AND #$C0
02570          TAY
02580 REL18    JSR STOUT     ;$F57A
02590 RDQUIT   LDA #$3C
02600          STA $D303
02610          LDA #$13
02620 REL19    JSR POKEY     ;$F5F7
02630 REL20    JSR GETBYTE   ;$F5B1
02640          CMP #$41
02650          BEQ CLRTI1
02660          CMP #$43
02670          BEQ CLRTI1
02680          CMP #$45
02690          BEQ ERR90
02700          LDA #$8B
02710          BNE ERR
02720 ERR90    LDA #$90
02730          STA $30       ;STATUS
02740 CLRTI1   LDY #$00
02750 STOUTX0  LDX #$00
02760 STOUT    LDA ERRABS    ;$F
02770          STA $0226     ;CDTMA1
02780 STOU2    LDA ERRABS+1  ;$F
02790          STA $0227     ;CDTMA1+1
02800          LDA #$01
02810          JMP $E45C     ;Setze CDTMV1
02820 ERRABS   .DA ERR8A     ;$F
02830 IOER80   LDX $3F       ;FEOF
02840          TXS
02850          LDA #$80
02860          STA $30       ;STATUS
02870          BNE EABS3
02880 ERR8F    LDA #$8F
02890          .HX 2C
02900 ERR8A    LDA #$8A      ;Timeout
02910 ERR      STA $30       ;STATUS
02920          LDX $3F       ;FEOF
02930          TXS
02940          LDA $3E       ;FTYPE
02950          BMI ERRA
02960          DEC $36       ;CRETRY
02970          BEQ ERRA
02980 REL21    JMP IO12      ;$F47A
02990 ERRA     LDA #$28
03000          STA $D204     ;AUDF3
03010 EABS3    JMP IO3       ;$F4C1
03020 GETBYTE  LDA $D20E     ;IRQST
03030          BPL IOER80
03040          AND #$20
03050          BNE GETBYTE
03060          LDA #$DF
03070          STA $D20E     ;IRQEN
03080          LDA #$E0
03090          STA $D20E     ;IRQEN
03100          LDA $D20F     ;SKSTAT
03110          STA $D20A     ;SKRES
03120          BPL ERR8A
03130          AND #$20
03140          BEQ ERR8A
03150          LDA $D20D     ;SERIN
03160          RTS
03170 PUTBYTE  TAX
03180 PUTA1    LDA $D20E     ;IRQST
03190          AND #$10
03200          BNE PUTA1
03210          LDA #$EF
03220          STA $D20E     ;IRQEN
03230          LDA #$D0
03240          STA $D20E     ;IRQEN
03250          TXA
03260          STA $D20D     ;SEROUT
03270          LDX $D20E     ;IRQST
03280          BPL IOER80
03290 ADDSUM   CLC
03300          ADC $31       ;CHKSUM
03310          ADC #$00
03320          STA $31       ;CHKSUM
03330          RTS
03340 POKEY    STA $D20F     ;SKCTL
03350          STA $D20A     ;SKRES
03360          LDA #$28
03370          STA $D208     ;AUDCTL
03380          LDA #$A8
03390          STA $D207     ;AUDC4
03400          LDA #$F8
03410          STA $D20E     ;IRQEN
03420          RTS
03430 C3F      .HX 3F40
03440          .DA $0001
03450          .DA $0001
03460          .DA $0001
03470 LWTBL    .BL 8,0
03480 USIOE
03490 ABSTBL   .DA DLWTBLL+1,REL01+1,REL02+1,REL03+1,REL04+1,REL05+1,REL06+1
03500          .DA REL07+1,REL08+1,REL09+1,REL10+1,REL11+1,REL12+1,REL13+1
03510          .DA REL14+1,REL15+1,GE1+1,REL16+1,REL17+1,REL18+1,REL19+1
03520          .DA REL20+1,STOUT+1,STOU2+1,ERRABS,REL21+1,EABS3+1
```
  
