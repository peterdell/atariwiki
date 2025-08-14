# 16bit increment and decrement  
  
```
00010 ------------------------------
00020 * 16-BYTE  INCREMENT ROUTINE *
00030 ------------------------------
00040 ------------------------------
00050 INC16B   INC LSB     NIEDERWAERTIGES BYTE
00060          BNE .1      UEBERZAEHLT
00070          INC MSB     JA, DANN HOEHERWAERTIGES BYTE
00080 .1       RTS         WEITER IM PROGRAMM
00090 ------------------------------
00100 *
00110 *
00120 ------------------------------
00130 * 16-BYTE  DECREMENT ROUTINE *
00140 ------------------------------
00150 ------------------------------
00160 DEC16B   LDA LSB     NIEDERWAERTIGES BYTE
00170          BNE .1      UNGLEICH NULL
00180          DEC MSB     NEIN, HOEHERWAERTIGES BYTE
00190 .1       DEC LSB
00200          RTS         WEITER IM PROGRAMM
00210 ------------------------------

```
