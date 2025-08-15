---
title: Read, write or convert from an Atari 815 Double Disk Drive
---
# Read, write or convert from an Atari 815 Double Disk Drive  
  
One of the major spin-offs from the [The Atari Accountant](https://atariwiki.org/wiki/Wiki.jsp?page=The%20Atari%20Accountant%20Series), thanks to Curt Vendel, is, that we now have the knowledge and technology to read, write and convert data from an Atari 815 Double Disk Drive.  
  
Ryan Goolevitch and Joachim Baßmann had the same idea at the same time independently from each other. Here it is:  
  
The Atari 815 Double Disk Drive is capable of dealing with single sided diskettes in true DD format, only. The head is at the same positon, it is in the Atari 810 Disk Drive. Therefore, going back to 1981 and earlier, the user was not able to change disks with the Atari 810 Single Disk Drive. But nowadays we have drives capable of reading DD diskettes and even double sided! So, we can get at least the data from the 815 with a sector copy program. An Atari 1050 disk drive with Happy, US Doubler, Speedy etc. can do this job without any problem.  
  
However, the 815 encoded the data bits on the disks binary inverted, compared to every other double density Atari compatible disk drive, so even though you can hopefully sector copy each 180 KB side. Header, gaps and so on are not inverted. The next step is to XOR every data bit in the resulting ATR image to get a usable disk. Bingo, that is all! :-)  
  
Please take into account the conversion table for dealing with bits:  
![](attachments/XOR.jpg)  
Conversion table for bits  
  
So, with this in mind and the outstanding program: [xorfiles.exe copyright (c) 2002 by Nir Sofer](http://www.nirsoft.net/utils/xorfiles.html), a PC user is able to convert the 815 atr to a readable 'normal' disk we used all years long. In order to do this, the user needs a DD formatted atr disk image, full of $FFs. Luckily, Joachim Baßmann has made this very special diskette for us, please see below in the Downloads chapter. Thank you so much Joachim, for all you have done for the community, we owe you so much. :-) Please go ahead!  
  
Hex-Dump of the FF.atr:  
![](attachments/HEX-Dump1.jpg)  
Hex-Dump of the FF.atr - first sector ; please take into account the marked row 1 (first 16 hex bytes) has to be unchanged  
  
![](attachments/HEX-Dump2.jpg)  
Hex-Dump of the FF.atr - last sector  
  
## Downloads  
- [readme.txt](attachments/readme.txt) ; from [Nir Sofer](http://www.nirsoft.net/utils/xorfiles.html) ; thank you so much Nir! Highly appreciated! :-)  
- [xorfiles.exe.zip](attachments/xorfiles.exe.zip) ; from [Nir Sofer](http://www.nirsoft.net/utils/xorfiles.html) ; thank you so much Nir! Highly appreciated! :-)  
- [FF.atr](attachments/FF.atr) ; thank you Joachim Baßmann for creating the needed atr image :-)  
  
## References  
- [The Atari Accountant Series on atari8bit.net](https://atari8bit.net/the-atari-accountant/)  
  
- [What's so specialabout the 815 on AtariAge](http://atariage.com/forums/topic/278709-whats-so-special-about-the-815/)  
  
- [Atari 815 - what's inside on AtariAge](http://atariage.com/forums/topic/186285-atari-815-whats-inside/)  
  
- [Atari 815 - controller source code on AtariAge](http://atariage.com/forums/topic/78379-atari-815-controller-source/) ; thank you so much Curt Vendel for saving this source code for the community. We can't say enough thank you to you! Great work!  
  
- [Why inverted data? - Percom at88 s1pd](http://atariage.com/forums/topic/224072-percom-at88-s1pd/)  
  
## Recommendations  
AtariWiki highly recommends for bit manipulation actions:  
  
Hardware:  
- [HP-16C calculator](http://www.hpmuseum.org/hp16.htm) ; thanks to the hpmuseum.org  
- [TI Programmer](http://www.datamath.org/Sci/MAJESTIC/Programmer.htm) ; thanks to Joerg Woerner  
- [TI LCD Programmer](http://www.datamath.org/Sci/Slanted/LCD-Programmer.htm) ; thanks to Joerg Woerner  
- [TI Programmer II](http://www.datamath.org/Sci/Slanted/Programmer-II.htm) ; thanks to Joerg Woerner  
  
Software/Emulation:  
- PC's or Mac's own calculators in the programmer mode  
- [PCalc](https://itunes.apple.com/us/app/pcalc/id284666222?mt=8) in the programmer mode for iPhone/iPad  
- [Computer programmer‘s flavor (former Touch 16i app, emulation of the HP-16C calculator)](https://epxx.co/ctb/touchios/) ; for iPhone/iPad  
