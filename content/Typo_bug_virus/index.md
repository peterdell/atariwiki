---
title: Typo bug virus
---
# Typo bug virus  
  
not really a virus, but a funny background program that creates random typos on "A" and "E" :)  
```
00010          .LI OFF
00020 ******************************
00030 *                            *
00040 * PROGRAMM:VERTIPP 0.1       *
00050 * AUTOR   :CARSTEN STROTMANN *
00060 * DATUM   :21.04.90          *
00070 * VERSION :0.1               *
00080 * FUER    :DUMME SCHERZE     *
00090 *                            *
00100 ******************************
00110 ;
00120 CH       =   $2FC
00130 VKEYBD   =   $208
00140 CASINI   =   $2
00150 BOOT     =   $9
00160 RTCLOK2  =   $14
00170 PORTB    =   $D301
00180 KBCODE   =   $D209
00190 CH1      =   $02F2
00200 KEYDEL   =   $02F1
00210 KEYDIS   =   $026D
00220 SSFLAG   =   $02FF
00230 HLPFLG   =   $02DC
00240 ATTRACT  =   $4D
00250 KRPDEL   =   $02D9
00260 SRTIMR   =   $022B
00270 SDMCTL   =   $022F
00280 DMASAV   =   $02DD
00290 KEYINT   =   $FC19
00300 RANDOM   =   $D20A
00310 ;
00320          .OR $600
00330 ;        .OF "D:AUTOS.COM"
00340 ;
00350 INIT
00360          LDA VKEYBD
00370          STA CASINI
00380          LDA VKEYBD+1
00390          STA CASINI+1
00400          LDA #KI
00410          STA VKEYBD
00420          LDA /KI
00430          STA VKEYBD+1
00440          LDA #INIT
00450          STA CASINI
00460          LDA /INIT
00470          STA CASINI+1
00480          LDA BOOT
00490          ORA #2
00500          STA BOOT
00510          RTS
00520 ;
00530 KEYBD
00540          PHA
00550          LDA RANDOM
00560          CMP #$D0
00570          BCC END
00580          LDA CH
00590          CMP #42
00600          BNE .1
00610          LDA #46
00620          STA CH
00630 .1       CMP #106
00640          BNE .2
00650          LDA #110
00660          STA CH
00670 .2       CMP #63
00680          BNE .3
00690          DEC CH
00700 .3       CMP #127
00710          BNE .4
00720          DEC CH
00730 .4       CMP #54
00740          BNE END
00750          LDA #158
00760          STA CH
00770 END      PLA
00780          RTI
00790 ------------------------------
00800 KI        TXA
00810           PHA 
00820           TYA 
00830           PHA 
00840           LDY PORTB
00850           LDA KBCODE
00860           STA CH
00870           CMP CH1
00880           BNE .1
00890           LDX KEYDEL
00900           BNE .9
00910 .1        LDX KEYDIS
00920           CMP #$83
00930           BNE .2
00940           TXA 
00950           EOR #$FF
00960           STA KEYDIS
00970           BNE .3
00980           TYA 
00990           ORA #$04
01000           BNE .4
01010 .3        TYA
01020           AND #$FB
01030 .4        TAY
01040           BCS .5
01050 .2        TXA
01060           BNE .6
01070           LDA KBCODE
01080           TAX 
01090           CMP #$9F
01100           BNE .7
01110           LDA SSFLAG
01120           EOR #$FF
01130           STA SSFLAG
01140           BCS .5
01150 .7        AND #$3F
01160           STX HLPFLG
01170           BEQ .5
01180           STX CH
01190           STX CH1
01200 .5        LDA #$03
01210           STA KEYDEL
01220           LDA #$00
01230           STA ATTRACT
01240 .9        LDA KRPDEL
01250           STA SRTIMR
01260           LDA SDMCTL
01270           BNE .6
01280           LDA DMASAV
01290           STA SDMCTL
01300 .6        STY PORTB
01310           PLA 
01320           TAY 
01330           PLA 
01340           TAX 
01350           PLA 
01360           JMP KEYBD
01370 ------------------------------
01380          .OR $02E0
01390          .DA INIT
01400 ------------------------------
```
