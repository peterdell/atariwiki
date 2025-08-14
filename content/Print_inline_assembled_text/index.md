General Information   
Author: CompyShop   
Assembler: Bibo Assembler   
Published: Bibo Assembler Toolkit Disk   
  
Textprintroutine through Stack. Routine must be  
called by JSR. Text inline after the JSR-Statement.  
The text must end with an end-maker (here the @-sign)  
The programm will be continued after the inline-text.  
  
(c) CompyShop (c) ABBUC e.V.  
  
```
00010 ------------------------------
00020 * Textprintroutine through   *
00030 * Stack. Routine must be     *
00040 * called by JSR.             *
00050 * Text inline after the      *
00060 * JSR-Statement.             *
00070 * The text must end with an  *
00080 * end-marker (here the @-sign*
00090 * The programm will be       *
00100 * continued after the inline-*
00110 * text.                      *
00120 ------------------------------
00130 *
00140 *
00150 PRINT    PLA         fetch Return Address
00160          STA $D0     from Stack
00170          PLA         and save as
00180          STA $D1     pointer 
00190 *
00200 INCP     INC $D0     increment Pointer
00210          BNE .1      
00220          INC $D1     
00230 .1       LDX #0      read char 
00240          LDA ($D0,X) from Memory
00250          CMP #'@     End?
00260          BEQ ENDPR   yes==>
00270          JSR PUTCHAR print char
00280          JMP INCP    back to loop
00290 *
00300 ENDPR    LDA $D1     Push Pointer as
00310          PHA         new Return
00320          LDA $D0     Address to
00330          PHA         Stack
00340          RTS         continue Programm 
00350 *            behind text!
00360 ------------------------------
00370 PUTCHAR  TAX         Print
00380          LDA $E407   Char 
00390          PHA         with
00400          LDA $E406   Stack
00410          PHA         Method
00420          TXA
00430          RTS         JUMP
00440 ------------------------------

```
  
