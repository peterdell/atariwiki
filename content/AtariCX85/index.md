---
title: AtariCX85
---
# Atari CX85 Numerical Keypad  
![](attachments/AtariCX85%2FAtari-CX85.jpg)  
  
## Source  
[Wikipedia](http://en.wikipedia.org/wiki/Atari_8-bit_computer_peripherals)  
## Documentation  
- [Atari CX85 Numerical Keypad-Users Guide](attachments/Atari_CX85_Numerical_Keypad-User_s_Guide.pdf) (PDF)  
- [Atari CX85 Numerical Keypad-Technical Reference Notes - 2 pages](attachments/Atari_CX85_Numerical_Keypad-Technical_Reference_Notes.pdf) (PDF)  
- [Atari CX85 Numerical Keypad-Technical Reference Notes - 1 page](attachments/Atari_CX85_Numerical_Keypad_Technical_Reference_Notes_1_page.pdf) (PDF) ; size: 10.5 MB  
- [Atari CX85 Numerical Keypad-Field Service Manual](attachments/atari_cx85_field_service_manual_screen.pdf) (PDF)  
![](attachments/CX+85+Field+Service+Manual.jpg)  
Atari CX85 Numerical Keypad - Field Service Manual - Thank you so much Bill Lange! :-))) We can't thank you enough to bring that ultra rare document to the light.  
  
## ATR-Images  
- [The_Atari_CX85_Master_Diskette_CX8139.atr](attachments/The_Atari_CX85_Master_Diskette_CX8139.atr) ; Original master disk  
- [cx85.atr](attachments/cx85.atr) ; Driver disk  
- [Atari CX85 Numerical Keypad - Field Service Manual program](attachments/Atari_CX85_Numerical_Keypad-Field_Service_Manual_Program.atr) ; Basic program from the Field Service Manual to test the device  
- [CX85_Reeve_Key.atr](attachments/CX85_Reeve_Key.atr) ; Copyright (C) 1986 by Alan Reeve  
  
## Source Codes  
- [original_CX85_Keyboard_Handler](../original_CX85_Keyboard_Handler/index.md) (original Atari Assembler Source)  
- [CX85_Keyboard_Handler](../CX85_Keyboard_Handler/index.md) (reverse engineered Source)  
- Atari CX85 Numerical Keypad - Field Service Manual Basic program to test the device:  
```
0 GRAPHICS 0:DIM FUNC$(10):PRINT :PRINT 
20 POKE 755,0:IF PEEK(645)=1 THEN 20
30 POKE 77,0:STICK1=PEEK(633)
40 ALLPOT=PEEK(53768):IF ALLPOT=0 THEN 40
50 IF ALLPOT=255 AND STICK1=12 THEN STICK1=16
60 FOR X=0 TO STICK1:READ A:NEXT X:IF A>9 THEN 80
70 PRINT A;" ";:GOTO 90
80 RESTORE 200:FOR X=0 TO A-10:READ FUNC$:NEXT X:PRINT FUNC$;" ";
90 FOR T=0 TO 50:NEXT T:RESTORE :GOTO 20
100 DATA 10,4,5,6,11,7,8,9,12,1,2,3,0,13,14,15,16
200 DATA DELETE,NO,YES,.,+ ENTER,-,ESCAPE
```
  
## Images  
![](attachments/AtariCX85%2FCX85_1.jpg)  
Atari CX85 Numerical Keypad - Diskette - front side  
  
![](attachments/AtariCX85%2FCX85_2.jpg)  
Atari CX85 Numerical Keypad - Diskette - back side  
