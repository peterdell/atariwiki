---
title: WSFN
---
# WSFN  
Harry Stewart, APX, 1981  
  
### Background  
WSFN (short for "Which Stands for Nothing") is a tiny programming language created by Li-Chen Wang (author of [Tiny BASIC](https://en.wikipedia.org/wiki/Tiny_BASIC)) as a way to send commands to a small robot. It was originally published in Dr. Dobb's Journal in September 1977, with the robot represented on-screen using what would today be known as turtle graphics.  
  
The language is similar to [PILOT](../Pilot/index.md) in concept, using single-letter commands who's primary purpose is to cause the turtle to move and create drawings. In contrast to PILOT, WSFN allows the construction of more complex macros using parenthesis, which can then be combined into larger programs. These macros can call themselves recursively, which allows it to draw complex images like fractals in a few lines of code.  
  
Extended WSFN was an implementation created for the Atari 8-bit family by Harry Stewart and published by the Atari Program Exchange (APX) in 1981. The main differences were to add another set of commands to provide access to some of the Atari platform's capabilities, notably graphics, color, sound and joystick support. The language was otherwise similar to the original, although some of the command letters changed to make room for new commands.  
  
A unique feature of the language is that the keyboard is active at all times, and users can interrupt programs as they run. For instance, if one makes a macro to draw an arc on the screen and names it "A", typing A will begin the drawing of the arc, but the user can press A in the middle of the process to draw a new arc at the current location, and so on. This makes all programs interactive without any specific code like an event loop.  
  
''Editor's note:'' One clearly missing feature is the ability to define macros that run on events other than the keyboard. If one could define macros that were triggered by the joystick, perhaps by defining the macro with a specific name like "!UP", one could write joystick-based drawing programs in a few lines of code.  
  
### Examples  
  
The following Extended WSFN code draws a square in the center of the screen:  
```
U2L12FND12F3(2R24F)2R12F
```
The code starts with the {{U}} which lifts the pen ({{U}}p) so the following commands will not draw to the screen. This is followed by a {{2}}, which means the next instruction should be run twice. In this case, the next instructions is {{L}}eft. Since each step of a turn is 45 degrees, this causes the turtle to rotate 90 degrees to the left so it points to the left side of the screen. Next, the turtle moves {{F}}orward 12 steps, is pointed {{N}}orth (up). Since the turtle was formerly pointed left, {{2R}} would have the same end effect as the {{N}}. Finally the pen is put back {{D}}own so the following commands will cause drawing on the screen.  
  
Next, the {{12F}} draws 12 steps, and since the turtle was pointing north, this causes a short line segment to be drawn up the screen. Then comes a {{3}}, meaning the following instruction should be run three times. In this case it is not a single instruction, but all of the instructions in the parens. These rotate {{2R}}ight, or 90 degrees, and then draws a segment 24 long. So the first iteration draws the horizontal line across the top, the next the vertical line down the right side, and then across the bottom. Finally, the ending {{2R12F}} finishes off the square by drawing the missing segment on the bottom of the left vertical side.  
  
As you can see, WSFN code can become almost unreadable even in simple examples!  
  
## ROM Image  
- [WSFN.rom](attachments/WSFN.rom) ; Thank you so much Atari_Ace from AtariAge for creating the rom image! Once, there was one cartridge on planet earth, which vanished in a museum and therefore was thought to be lost. After 36 years(!) you brought it back to the light. Thank you so much, we owe you very much, indeed. By the way, Atari_Ace's [website](https://ksquiggle.neocities.org/) is highly recommended by AtariWiki.org! The site is full of source codes. Give it a try! :-)))  
  
## CAR Image  
- [WSFN.car](attachments/WSFN.car) ; Thank you so much Atari_Ace from AtariAge for creating the rom image! Once, there was one cartridge on planet earth, which vanished in a museum and therefore was thought to be lost. After 36 years(!) you brought it back to the light. Thank you so much, we owe you very much, indeed. By the way, Atari_Ace's [website](https://ksquiggle.neocities.org/) is highly recommended by AtariWiki.org! The site is full of source codes. Give it a try! :-)))  
  
## CAS Image  
__... still missing ; original APX-10026 cassette ; if you own this cassette, please let us know. Thank you so much in advance. :-)__  
  
## ATR Image  
- [APX_Extended_WSFN.atr](attachments/APX_Extended_WSFN.atr) ; original APX-20026 diskette of Extended WSFN ; Thank you so much Allan Bushman for preserving this very rare software. We really owe you very much! Please go ahead. :-)  
  
## Manual  
- [APX_Extended_WSFN-Original.pdf](https://data.atariwiki.org/DOC/APX_Extended_WSFN-Original.pdf) ; size: 171.8 MB ; original manual scanned in super quality by Allan Bushman. Thank you so much Allan for all the work you have done for us. We are really deep in your debt. Please go ahaed. :-)))  
- [APX_Extended_WSFN-OCR-Print.pdf](https://data.atariwiki.org/DOC/APX_Extended_WSFN-OCR-Print.pdf) ; size: 76.2 MB ; OCR version of the above manual version  
- [APX_Extended_WSFN-OCR-Screen.pdf](https://data.atariwiki.org/DOC/APX_Extended_WSFN-OCR-Screen.pdf) ; size: 5.3 MB ; OCR screen optimized version of the above manual  
- [Atari_WSFN-An_Introduction.pdf](attachments/Atari_WSFN-An_Introduction.pdf) ; size: 2.3 MB ; WSFN introduction from Harry B. Stewart realeased in 2016. Thank you so much Harry, we really appreciate your help so much. :-)))  
- [Atari_WSFN-Manual_draft.pdf](attachments/Atari_WSFN-Manual_draft.pdf) ; size: 2.5 MB ; WSFN manual draft from Harry B. Stewart realeased in 2016. Thank you so much Harry, we really appreciate your help so much. :-)))  
  
## Source Code  
- [wsfn.txt](attachments/wsfn.txt) ; original source code from Harry B. Stewart, typed in and digitized by Atari_Ace from AtariAge. We both thank you so much, can't tell you. :-))) By the way, Atari_Ace's [website](https://ksquiggle.neocities.org/) is highly recommended by AtariWiki.org! The site is full of source codes. Give it a try! :-)))  
  
## References  
- [Wikipedia description of WSFN](https://en.wikipedia.org/wiki/WSFN_(programming_language))  
- [Atari WSFN Source Code from Harry B. Stewart on archive.org](https://archive.org/details/AtariWSFNSourceCode); Thank you so much Harry B. Stewart for giving this source code into PD, Atari_Ace from AtariAge for typing in the source code and checking it and Kay Savetz for uploading to archive.org. :-)))  
- [Atari WSFN - An Introduction - draft from Harry B. Stewart on archive.org](https://archive.org/details/AtariWSFNAnIntroduction); Thank you so much Harry B. Stewart for giving this introduction into PD and Kay Savetz for digitzing and uploading to archive.org. :-)))  
- [Atari WSFN Manual Draft from Harry B. Stewart on archive.org](https://archive.org/details/AtariWSFNManualDraft) ; Thank you so much Harry B. Stewart for giving this draft into PD and Kay Savetz for digitzing and uploading to archive.org. :-)))  
- [Atarimania entry of WSFN](http://www.atarimania.com/utility-atari-400-800-xl-xe-extended-wsfn_28120.html) ; Thank you so much Allan Bushman for preserving this very rare software. We really owe you very much! Please go ahead. :-)))  
- [AtariAge site of WSFN](http://atariage.com/forums/topic/258767-atari-wsfn-source-code/)  
- [Atari 8-bit forever entry of WSFN](http://gury.atari8.info/software/1007.php)  
- [atariarchives.org entry of WSFN](http://www.atariarchives.org/APX/showinfo.php?cat=20026)  
- [Canada's Videogame Museum's entry of WSFN](http://www.pcmuseum.ca/details.asp?id=39356&type=software)  
- [Alchetron entry of WSFN](https://alchetron.com/WSFN-(programming-language)-5071974-W)  
  
## Pictures  
![](attachments/ATAExtendedWSFN-1-750.jpg)  
Extended WSFN APX-20026 box - front  
  
![](attachments/ATAExtendedWSFN-2-750.jpg)  
Extended WSFN APX-20026 box - back  
  
![](attachments/APX_Extended_WSFN_diskette.jpg)  
Extended WSFN Diskette APX-20026  
  
![](attachments/APX_Extended_WSFN_3.gif)  
Extended WSFN - example #1  
  
![](attachments/APX_Extended_WSFN_2.gif)  
Extended WSFN - example #1  
  
![](attachments/Extended_WSFN_ad.jpg)  
Extended WSFN APX-20026 box - ad  
