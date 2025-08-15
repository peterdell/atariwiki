---
title: CTH-FastBasic
---
# CTH FastBasic  
Closer To Home FastBasic Copyright (C) C.T.H. Closer To Home & Tom Hunt  
  
### Background  
CTH FastBasic is a version of [Atari_BASIC](../Atari_BASIC/index.md) written by Tom Hunt of the Closer to Home BBS (CTH). It fixes the two biggest performance problems in Atari BASIC, and runs much faster as a result, on the order of 30 to 80% on most programs, and as much as 300% on some. You will find the largest speed increase when running large basic programs as opposed to small ones. It is otherwise compatible with Atari BASIC, and should run any Atari BASIC program without modifications.  
  
To get started, just load CTHFAST.COM. Instead of ATARI basic's familiar READY prompt you will see (CTH FastBasic). You can test out the speed increase with the supplied basic program named BENCHTST.BAS. Then try CTH FastBasic out on some of your own programs. Have a watch or stopwatch handy, and compare CTH FastBasic against ATARI basic. As I mentioned before, the biggest increase in execution speed will be seen on your larger basic programs. It is easy to switch between the two with a simple POKE. You POKE 54017,253 to install ATARI basic, and POKE 54017,255 to switch to CTH Fastbasic. This is necessary only if you want to switch back and forth between the two.  
  
If you go to DOS from CTH FastBasic you will have to do something you aren't accustomed to in order to return to CTH FastBasic. With Sparta you must type RUN A04D, and with Atari dos 2.5 and 2.0 you must use the M option of the DUP menu. After typing M you specify A04D as the run address. The reason you must do this instead of typing CAR or B with Sparta Dos/ATARI Dos is because there is no cartridge present, and the dos knows it. So by using this procedure you will return to the CTH FastBasic program that is in ram. If using Sparta Dos, your basic program will be preserved. Going to ATARI dos will wipe out your basic program. Alternately, you can use the supplied program named B to return to basic. This is probably the safest way, preventing a mistyped address from doing who knows what to your system. Another small utility program included in this ARC file is named SC. I use it when I want to use CTH FastBasic with MOE. Just put it in your batch file immediately before MOE is loaded in. Otherwise MOE won't allow CTH FastBasic to set the screen up. You can use the SC utility in the same manor for most programs that refuses to allow CTH FastBasic to create a display list for the screen.  
  
Also, using the RESET key will wipe out CTH FastBasic.  
  
I suggest that you run CTH FastBasic only on completed programs, not programs under the process of development. This is because there is a difference between the way ATARI basic and CTH FastBasic uses the CONT and GOTO statements. If you do use CTH_FastBasic and edit a program be sure to use RUN instead of CONT and GOTO.  
  
## C.T.H. FastBasic suite  
- [CTH_Fast_Basic.zip](attachments/CTH_Fast_Basic.zip) ; all you need for running C.T.H. FastBasic, enjoy! :-) ; Thank you so much Tom Hunt! :-)  
  
## Picture  
![](attachments/Startscreen.jpg)  
Closer To Home FastBasic - startscreen  
