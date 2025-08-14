# Make protected BASIC code visible  
Sometimes Atari BASIC is protected and the user isn't able to see inside the source code. This is a main disadvantage, especially, when the original code is damaged. In order to preserve the software genuine, there is a need to solve this problem.  
![](attachments/Quelltext.jpg)  
List-Protected BASIC code from the German BASIC course: '[Noch mehr BASIC TXG 55007](../Noch_mehr_BASIC_TXG_55007/index.md)'  
  
Luckily, living legend Avery Lee, the creator of the Atari [Altirra](http://www.virtualdub.org/altirra.html) emulator, has implemented 2 routines, which do the job in a marvelous way. :-)  
  
Given the fact the user has already just loaded in the BASIC code without executing, then just the F8 key has to be pressed to force an interrupt:  
![](attachments/Debug_.jpg)  
Forcing an interrupt in the Atari [Altirra](http://www.virtualdub.org/altirra.html) emulator  
  
Afterwards, in the Console window, just type in these 2 lines:  
  
.basic_rebuildvnt  
.basic_rebuildvvt  
  
and press the F8 key again. That's all. Now back in BASIC, you can list the source code in it's original form or save it to disk. :-)  
  
The 2 lines executed in Altirra, do the following things:  
  
.basic_rebuildvnt ; Rebuild BASIC variable name table  
.basic_rebuildvvt ; Rebuild BASIC variable value table  
  
Again, we deeply, deeply have to thank Avery Lee for his gigantic help to the community worldwide. Thank you so much Avery. :-)  
