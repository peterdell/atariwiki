# Atari PILOT with Turtle Graphics CX405  
  
### Background  
PILOT is an extremely simple programming language written in 1968 explicitly for teaching programming to children. The language consists of one-letter commands followed by a colon, one command per line, and with a very limited set of commands and operations. Variables are prefixed with $, and labels with a *.  
  
Atari PILOT is unique in that it added a set of commands for graphics and sound using two-letter commands, GR and SO. The graphics system used turtle graphics, with the string following the GR command containing multiple sub-commands like DRAW and TURN. The syntax for these commands is similar to [WSFN](../WSFN/index.md), allowing a series of commands to be repeated by placing them inside parenthesis and putting the number of times to perform it in front.  
  
For editing purposes, Atari PILOT uses line numbers, which were not part of the original language.  However, these can be skipped by using the AUTO feature, which adds these numbers automatically without displaying them on the screen. The screen turns a yellow color when AUTO is active. The editor includes features for renumbering, which suggests it might be the one from [Atari_Assembler_Editor](../Atari_Assembler_Editor/index.md).  
  
### Example  
  
The following is a simple Hello World in PILOT:  
```
R:Hello World in PILOT
T:What is your name?
A:$NAME
R:Hello $NAME!
```
R is a "remark", similar to the REM statement in BASIC, T is "type", the equivalent of PRINT, and A is "accept", the equivalent to INPUT. The following example shows the Atari extensions for graphics:  
```
R:Draw a square in the center of the screen
GR:4(DRAW 20; TURN 90)
```
The 4 after the GR: is a looping construct which repeats the section in the (...) four times. This is similar to the [WSFN](../WSFN/index.md) language, which had similar turtle graphics and looping structures.  
  
## Images  
![](attachments/pilot_atari.gif)  
Atari Pilot Cartridge CXL4018 - 1st screen after booting  
  
![](attachments/pilot_educators_cart_2.jpg)  
Atari Pilot box - front - thanks to Allan Bushman for scanning  
  
![](attachments/pilot_educators_cart.jpg)  
Atari Pilot box - back - thanks to Allan Bushman for scanning  
  
## Source Code  
- [Atari Pilot source code](attachments/Atari_PILOT_source_code.txt) ; Thank you so much Atari_Ace from AtariAge for your help in creating the code. We really appreciate your help, please go ahead! :-)))  
  
## Commercial  
- [Atari PILOT commercial](attachments/atari_8bit_commercial_pac_man_pilot.flv) ; flash file, size: 4.7 MB.  
  
## Manuals  
- [Atari_Pilot_Primer.pdf](attachments/Atari_Pilot_Primer.pdf) The PILOT Programming Language Instruction Manual  
- [Atari_Pilot_Demonstration_Programs-Users_Guide.pdf](attachments/Atari_Pilot_Demonstration_Programs-Users_Guide.pdf)  
- [Atari_Student_Pilot-Reference_Guide.pdf](attachments/Atari_Student_Pilot-Reference_Guide.pdf)  
- [PILOT-Pocket_Reference_Card.pdf](attachments/PILOT-Pocket_Reference_Card.pdf)  
- [Atari Pilot External Specification-Revision E 1980](attachments/Atari_Pilot_External_Specification_revision_E.pdf) 6.2 MB PDF file, b/w only, searchable, Atari Pilot External Specification, Revision E, 1980, thank you so much for your work Kay Savetz! We really appreciate that!  
  
## References  
- [Pilot Source Code on archive.org](https://archive.org/details/AtariPILOTSourceCode); Thank you so much Harry & Kevin for your help in getting the code. We really appreciate your help, please go ahead! :-)))  
- [Pilot Source Code on AtariAge](http://atariage.com/forums/topic/257991-atari-pilot-source-code/)  
  
## CAR-Images  
- [ATARI_PILOT.car](attachments/ATARI_PILOT.car)  
  
## ROM-Images  
![](attachments/pilot.jpg)  
Atari Pilot Cartridge CXL4018  
- [Atari_PILOT.rom](attachments/Atari_PILOT.rom)  
  
## BIN-Images  
- [Pilot_(1981).bin](attachments/Pilot_(1981).bin)  
  
## ATR-Images  
- [Atari_PILOT_Demonstration_Program_Cassettes_CX4113-A_and_B-Side_1_and_2.atr](attachments/Atari_PILOT_Demonstration_Program_Cassettes_CX4113-A_and_B-Side_1_and_2.atr)  
- [Language_1.atr](attachments/Language_1.atr)  
- [Language_2.atr](attachments/Language_2.atr)  
- [Pilot_1.atr](attachments/Pilot_1.atr)  
- [Pilot_2.atr](attachments/Pilot_2.atr)  
- [Pilot_3.atr](attachments/Pilot_3.atr)  
  
## CAS-Images  
- [Pilot_Education_Package-Cassette_A_side_1.cas](attachments/Pilot_Education_Package-Cassette_A_side_1.cas)  
- [Pilot_Education_Package-Cassette_A_side_2.cas](attachments/Pilot_Education_Package-Cassette_A_side_2.cas)  
- [Pilot_Education_Package-Cassette_B_side_1.cas](attachments/Pilot_Education_Package-Cassette_B_side_1.cas)  
- [Pilot_Education_Package-Cassette_B_side_2.cas](attachments/Pilot_Education_Package-Cassette_B_side_2.cas)  
  
## Atari Pilot Cassettes CX4113  
With Giga-Thanks to Allan Bushman (he will never be forgotten!), we are now at 100 % of the Atari Pilot CX405 Educators' Package, the complete(!) box.  
The package includes two Demonstration Program Cassettes:  
  
- __Atari Pilot Cassette CX4113 A:__  
  
![](attachments/pilot_educators_k7_2.jpg)  
PILOT Programs for Children - cassette A side 1 - thanks to Allan Bushman for scanning  
- [Pilot_Education_Package-Cassette_A_side_1.cas](attachments/Pilot_Education_Package-Cassette_A_side_1.cas)  
  
![](attachments/pilot_educators_k7.jpg)  
A PILOT Teaching Program - cassette A side 2 - thanks to Allan Bushman for scanning  
- [Pilot_Education_Package-Cassette_A_side_2.cas](attachments/Pilot_Education_Package-Cassette_A_side_2.cas)  
  
- __Atari Pilot Cassette CX4113 B:__  
  
![](attachments/pilot_educators_k7_3.jpg)  
PILOT "Turtle Graphics" Demonstration - cassette B side 1 - thanks to Allan Bushman for scanning  
- [Pilot_Education_Package-Cassette_B_side_1.cas](attachments/Pilot_Education_Package-Cassette_B_side_1.cas)  
  
![](attachments/pilot_educators_k7_4.jpg)  
PILOT Do-It-Yourself Slide Show - cassette B side 2 - thanks to Allan Bushman for scanning  
- [Pilot_Education_Package-Cassette_B_side_2.cas](attachments/Pilot_Education_Package-Cassette_B_side_2.cas)  
  
Both cassettes just include program data only! No audio! Therefore, we prefer to have it on diskette, please see above under: ATR-Images  
  
## Atari Pilot Cassettes CX4113 Program Pictures  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-01.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-01  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-02.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-02  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-03.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-03  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-04.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-04  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-05.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-05  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-06.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-06  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-07.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-07  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-08.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-08  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-09.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-09  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-10.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-10  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-11.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-11  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-12.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-12  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-13.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-13  
![](attachments/Atari+PILOT+Demonstration+Program+Cassettes+CX4113-14.jpg)  
Atari PILOT Demonstration Program Cassettes CX4113-14  
