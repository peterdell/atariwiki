# Print to Screen without OS  
  
General Information  
  
Author: Carsten Strotmann   
Assembler: Bibo Assembler   
  
Example:  
  
```
00660 DEMO     LDX 10
00670          LDY 5
00680          JSR PRINT
00690          .AT "HELLO PSC SOFTWARE"
00700          .HX 9B
```
  
```
00010 *****************************
00020 *                           *
00030 *  Screen Output without    *
00040 *  ATARI OS Routines        *
00050 *                           *
00060 *  <X> - X POSITION         *
00070 *  <Y> - Y POSITION         *
00080 *                           *
00090 *****************************
00100 ;
00110 ;
00120 ; OS Variables
00130 ;
00140 SAVMSC   =   $58     ScreenMem
00150 CRSINH   =   $02F0   Cursor Pos
00160 ;
00170 ; ZERO PAGE REGISTER
00180 ;
00190 ZTEMP    =   $F5
00200 ;
00210 ;
00220          .OR $4000
00230 ;
00240 ;
00250 PRINT    LDA SAVMSC    copy screen-
00260          STA ZTEMP     address
00270 ;
00280 Y_LOOP   CLC
00290          LDA ZTEMP
00300          ADC #40
00310          STA ZTEMP
00320          LDA ZTEMP+1
00330          ADC #0
00340          STA ZTEMP+1
00350          DEY
00360          BNE Y_LOOP
00370 ;
00380 X_RECH   CLC
00390          TXA
00400          ADC ZTEMP
00410          STA ZTEMP
00420          LDA ZTEMP+1
00430          ADC #0
00440          STA ZTEMP+1
00450          PLA
00460          STA ZTEMP+2
00470          PLA
00480          STA ZTEMP+3
00490 ;
00500 AUSLOOP  INY
00510          LDA (ZTEMP+3),Y
00520          CMP #$9B
00530          BEQ AUSEND
00540          STA (ZTEMP),Y
00550          JMP AUSLOOP
00560 ;
00570 AUSEND   TYA
00580          CLC
00590          ADC ZTEMP+2
00600          PHA
00610          LDA ZTEMP+3
00620          ADC #0
00630          PHA
00640          RTS
00650 ------------------------------

```
