---
title: Create an atx image from KryoFlux raw files
---
# Create an atx image from KryoFlux raw files ; Copyright (C) 2014-2015 Avery Lee, All Rights Reserved  
The [KryoFlux](https://kryoflux.com/) is an incredible device for backup, not only for Atari, but for Commodore, Atari ST, Amiga an so on.  
Besides the KryoFlux stuff, please see the link above, you need this incredible software from Avery Lee, author of [Altirra](http://www.virtualdub.org/altirra.html):  
- [a8rawconv-0.9-pc.zip](attachments/a8rawconv-0.9-pc.zip) ; thank you Avery Lee for giving the community this software! :-))) We really appreciate your help, input and all you have done for us! Please go ahead and live long and prosper.  
- [a8rawconv-0.9-mac.zip](attachments/a8rawconv-0.9-mac.zip) ; thank you Farb from AtariAge for compiling the software for the Mac. Now, the Mac users are in game, too. :-)  
To convert existing raw files to an atx image, you have to do the following on a:  
## - PC:  
Similar to the receipt for the Mac, but instead please use the following in the command shell:  
  
__D:Atari...a8rawconv.exe -l -tpi 48 -if kryoflux -of atx -v D:Atari...input.raw D:Atari...output.atx >D:Atari...report.log__  
  
Where 'D:Atari...' is the path to the folder of the raw files and the program a8rawconv.exe  
  
Thank you so much FloppyDoc for your help in this! We really appreciate your contribution very much.  
## - Mac:  
Go to the Terminal app, copy all raw files in one folder of your choice. Copy a8rawconv in that folder. Type "cd" a blank in Terminal and drag & drop the folder into the Terminal app. Press return. Afterwards type in:  
  
__./a8rawconv -b -l -if kryoflux -of atx -v input.raw output.atx >report.log__  
  
in case of trouble please use:  
  
__./a8rawconv -l -tpi 48 -if kryoflux -of atx -v input.raw output.atx >report.log__  
  
and press return again. If everything was done well, you should receive a proper atx image. Don't forget to deactivate the SIO Patch in Atari800MacX in order to use the atx image without any problems. The input.raw file should be just the very first file of all the raw files belonging to the disk image. Avery Lee's is really smart and does the rest for you. :-)  
  
Would be cool, if someone can write the PC instructions here. Thank you in advance. :-)  
  
## Manual:  
- [manual.rtf](attachments/manual.rtf) ; Copyright (C) 2014-2015 Avery Lee, All Rights Reserved  
