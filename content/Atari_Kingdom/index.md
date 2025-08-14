# Atari Kingdom CX4102 ; Copyright (C) 1980 Atari, Inc. ; please use with BASIC cartridge inserted  
Atari Kingdom CX4102 is one of the first simulation game from Atari with a short source code, easy to read and understand. It is a good choice to get a first view into simulations.  
## CAS-images  
- [Kingdom_side_A_with_instructions.cas](attachments/Kingdom_side_A_with_instructions.cas) ; CAS-image of Kingdom with instructions  
- [Kingdom_side_B_without_instructions.cas](attachments/Kingdom_side_B_without_instructions.cas) ; CAS-image of Kindom without instructions  
## ATR-image  
- [Kingdom_with_DOS_2.0S_(complete_cassette_import).atr](attachments/Kingdom_with_DOS_2.0S_(complete_cassette_import).atr) ; Atari Kingdom CX4102 complete cassette import on an ATR-image with DOS 2.0S  
## Manual  
- [Atari_Kingdom_Manual.pdf](attachments/Atari_Kingdom_Manual.pdf) ; size: 561 KB ; Atari Kingdom CX4102 manual, 4 pages  
## Video with voice, music and data  
- [Atari Kingdom cassette-Dual Track with voice, music and data](attachments/Atari_Kingdom-Dual_Track.mp4) ; size: 14.4 MB ; MP4-file taken from Youtube; main start from minute 1:10  
## Box-Images  
![](attachments/Atari_Kingdom_Cover_1.jpg)  
Atari Kingdom CX4102 box cover   
  
![](attachments/Atari_Kingdom_Back_1.jpg)  
Atari Kingdom CX4102 box back   
  
## Screenshots  
![](attachments/1.jpg)  
Atari Kingdom CX4102 1st screen - beginning of loading   
  
![](attachments/2.jpg)  
Atari Kingdom CX4102 2nd loading from cassette side A with instructions   
  
![](attachments/3.jpg)  
Atari Kingdom CX4102 instruction side 1 of 2   
  
![](attachments/4.jpg)  
Atari Kingdom CX4102 instruction side 2 of 2   
  
![](attachments/5.jpg)  
Atari Kingdom CX4102 main screen - 1st start  
## Advertising  
![](attachments/Advertising1.jpg)  
Atari Kingdom CX4102 Advertising 1  
  
![](attachments/Advertising4.png)  
Atari Kingdom CX4102 Advertising 2  
  
![](attachments/Advertising3.jpg)  
Atari Kingdom CX4102 Advertising 3  
## Messages from the source code  
300 IF RND(0)<0.03 THEN GOSUB 250:? " A plague! Half the people died!!":P=INT(P/2)  
320 GOSUB 90:PRINT "ACRES TO SELL";:GOSUB 920:IF BAD THEN 320  
370 GOSUB 90:PRINT "ACRES TO BUY";:GOSUB 920:IF BAD THEN 370  
430 GOSUB 90:PRINT "BUSHELS FOR THE PEOPLE";:GOSUB 920:IF BAD THEN 430  
470 GOSUB 90:PRINT "ACRES TO PLANT";:GOSUB 920:IF BAD THEN 470  
540 GOSUB 90:PRINT "You have only ";P;" people!":GOSUB 30:GOTO 470  
660 GOSUB 250:PRINT "You starved ";S;" people this year!"  
670 ? "Due to this extreme mismanagement,"  
680 ? "you have been thrown out of office":? "and declared National Fink!":GOTO 890  
690 GOSUB 90:PRINT "You've only ";B;" bushels of grain!";:GOTO 30  
700 GOSUB 90:PRINT "You've only ";A;" acres of land!!":GOTO 30:RETURN   
720 GOSUB 200:GOSUB 250:? "In ";Y;" years of office, ";P1;"% of the":? "population starved on the average."  
730 ? D1;" people died in total starting":L4=INT(A/P)  
740 ? "with 10 acres/person and ending":? "with ";L4;" acres/person.":GOSUB 50  
810 GOSUB 250:? "A fantastic performance!":? "Charlemange, Disraeli, and "  
820 ? "Jefferson combined could not have ":? "done better!!":GOTO 870  
830 GOSUB 250:? "Your heavy-handed performance ":? "smacks of Nero and Ivan IV. The"  
840 ? "people find you an unpleasant ruler":? "frankly hate your guts!":GOTO 870  
850 GOSUB 250:? "You could have done better."  
860 ? INT(P*0.8*RND(0));" people would like to see you":? "assassinated."  
