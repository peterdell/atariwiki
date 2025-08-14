# Fortran  
  
  
## Background  
Fortran is one of the earliest programming languages, and among the most influential. [Basic](../Basic/index.md) is a simplified, interpreted version of Fortran, sharing many of its constructs and commands. As of 2016, there is still no Fortran for the Atari 8 bit home computers, which is very sad, because Fortran remains important in scientific programming.  
  
Fortran was intended to be used primarily for scientific mathematical processing, and it initially lacked any capability for strings and other common tasks. These were added over the years, and as a result the language began to grow. Early versions from the 1950s and 60s are quite small and could easily run on 8-bit machines, but later versions from the 1990s are more complex. The most practical version for 8-bit machines would be Fortran77, which would be very similar to most BASICs of the era.  
  
Abacus Fortran for C64 was released in 1988. Here we have a program running native in 6502 code. The question is: who can port this to the Atari?  
  
However, there was a Fortran for the Apple II written in 6502 assembly language. Maybe there will be a time, when we get the the source code for this Apple version and can port this to the Atari? For a first step in this case, AtariWiki has collected information about Fortran for the Apple II, see below. So, if there is anyone out there, who is in the possession of the original Apple II source code of Fortran, please be so kind and give it to us. Thank you so much in advance.  
  
## Infos  
### (1):  
Released by Apple in 1980, Apple FORTRAN ran under the Pascal operating system. It cost $200 (over and above the $495 needed to get the Language System). Programs written in FORTRAN for other computers could run with little modification under Apple FORTRAN (if a user needed that ability). It compiled to a similar code as did Pascal programs, so was not any faster than Pascal. Apple’s version of FORTRAN had many bugs in it, though, and after its introduction in 1980 it was never upgraded. By September 1986 it had disappeared from their product catalogs.  
  
Another way for an Apple II user to get FORTRAN was to buy the Microsoft Z-80 Softcard for $345 and Microsoft FORTRAN for $200. This version of FORTRAN was more full-featured than Apple’s, and offered some advantages in usability. It did not require changing to the 16-sector disk controller ROMs (if you didn’t want to). Also, standard Microsoft BASIC (which was more advanced than Applesoft) was included in the Softcard package.  
  
In June of 1987 Pecan Software released FORTRAN for the IIGS. It ran under ProDOS 16 (GS/OS), but still used the UCSD Pascal disk format for its FORTRAN by creating a ProDOS file that then acted as a UCSD Volume.  
### (2):  
Cabot FORTRAN 77  
Runs on Apple I(?), IIgs, Mac, MS-DOS, CP/M and Unix boxes. Claims the 'worldwide software licence (sic) for software products developed by the University of California, San Diego  
(UCSD).  
  
Address:  
The Vicarage  
Stoke View Road  
Fishponds  
Bristol BS16 3AE  
England UK  
  
Telephone: 00 44 272 586644  
Fax: 00 44 272 586023  
BBS: 00 44 272 583023  
  
Compuserve address: 100014,241  
### (3):  
PRO FORTRAN-77  
Prospero Software  
190 Castlenau  
London SW13 9DH  
England  
$149  
  
Reviewed by Mike Fleischman  
  
Prospero Pro Fortran-77 is a full implementation of the ANSI standard version of Fortran-77. The program comes with a manual and a disk containing the two-pass Fortran compiler and the linker. It does not come with an editor, however, so you will need a text editor or word processor to use this package.  
I found I could use the software on either the ST's double-sided disk drive or two single-sided drives. The compiler supports all GEM AES and VDI calls as well as the TOS environment commands. Writing a program with full GEM support should be relatively easy.  
This is a very complete Fortran package. The language supports 1-, 2- and 4-byte integers and logicals, 4 and 8-byte floating point numbers and complex numbers. As in standard Fortran the lines are 72 columns long and character names can be only six characters. Implicit type checking is also implemented as well as the standard default Fortran work file. The most files you can have open at one time is 15. GEM support deviates from the Fortran standard, because the company followed all the C definitions for the VDI and AES interfaces.  
The first thing you will discover about the Pro Fortran compiler is that the language requires a memory resident section to be installed before anything else will run. This brings up an interesting question: Does Prospero want royalties for use of their memory resident section? I found that their copyright agreement states that you are buying this package for your sole use only and that you will not disassemble or alter the software for your own use.  
From this I would conclude that if you intend to use this software for anything other than your own use, you'd be wise to contact Prospero Software for any agreements necessary.  
The compiler and linker prompt you for the necessary information. The compiler also has optional prompts for all compile parameters. There is also a configuration program to customize the default settings. The compile time is relatively fast and the resulting code is compact. The only real hitch to writing your own program is the lack of an editor.  
I used a Sieve test to measure the speed of the compiler on my 520ST (with one megabyte of memory and two disk drives). I found that the program compiled and linked in two minutes and 46 seconds, producing a program 4,758 bytes long. My running time for this program was 11 minutes and eight seconds, compared to 13 minutes, 21 seconds for ST Basic, and 2.53 seconds for Digital Research C.  
Fortran-77 follows all the standard Fortran syntax and you should have no trouble moving your source code to a mainframe computer once it is running. I was impressed with the quality of the package and the ease of its use, but the copyright agreement would make me want a second look. Also, I am concerned that the program runs so slowly.  
But this is generally a very good implementation of Fortran-77. If you are a programming student or need to learn or use Fortran-77 in your college studies, this would be a worthwhile investment.  
  
## FORTRAN via FujiNet adapter  
In January of 2021 Thomas Cherryhomes realzied [FORTRAN on the Atari via the FujiNet adapter](https://www.youtube.com/watch?v=5XV_LuCw-JE). Thom, the community is sooo deep in you debt, we deeply thank you so much from the heart! :-)))  
  
## Source Code  
__Who can help us with the source code of the Abacus Fortran for C64 and Apple II Fortran? AtariWiki really appreciate any help in this case. Thank you so much in advance. :-)__  
  
## Images (for the Commodore 64)  
- [Abacus Fortran for C64](https://www.lyonlabs.org/commodore/onrequest/collections.html) ; Thank you Lyonlabs for hosting! :-) We really appreciate your help  
  
## Images (for the Apple II)  
- [Apple II Fortran Images](attachments/Apple_II-Fortran-Images.zip) ; size: 730 KB  
The SST was used to convert the disk FORT2 to the nib format. It is verified, that it works with ApplePC v2.52. It is also a modified version corrected to work with APPLESTUFF (as you may recall, Apple Fortran uses the Apple Pascal architecture, APPLESTUFF is a library for turtle graphics and sound). If you want to format a new disk you would also need to get a copy of Pascal, APPLE 3.  
- [Fortran Recipes 2.0 - source codes](attachments/Fortran_Recipes_2.0.zip) ; size: 294 KB  
  
## Manuals  
- [ANSI Fortran 66](attachments/ansi_Fortran66.pdf) ; size: 10.9 MB  
- [Abacus Fortran for C64](https://www.lyonlabs.org/commodore/onrequest/collections.html) ; size: 29.7 MB ; Thank you Lyonlabs for hosting! :-) We really appreciate your help  
- [Apple II FORTRAN Language Reference Manual.pdf](attachments/Apple_II_FORTRAN_Language_Reference_Manual.pdf) ; size: 5.9 MB  
- [Apple II FORTRAN Language Reference Manual_OCR.pdf](attachments/Apple_II_FORTRAN_Language_Reference_Manual_OCR.pdf) ; size: 3.8 MB  
- [Fortran 90 Reference Card.pdf](attachments/Fortran_90_Reference_Card.pdf) ; size: 193 KB  
- [IBM FORTRAN IV-Language 1973.pdf](attachments/IBM_FORTRAN_IV-Language_1973.pdf) ; size: 23.1 MB  
- [IBM Fortran coding form.pdf](attachments/IBM_Fortran_coding_form.pdf) ; size: 42 KB  
- [Microsoft FORTRAN 80 version 3.4 user's manual Nov. 80.pdf](attachments/Microsoft_FORTRAN-80_Ver3.4_Users_Manual_Nov80.pdf) ; size: 12.6 MB  
- [Professional Programmer's guide to Fortran 77.pdf](attachments/Professional_Programmer_s_Guide_to_Fortran77.pdf) ; size: 726 KB  
- [Programming in Fortran-Vladimir Zwass.pdf](http://data.atariwiki.org/DATA/Programming_in_Fortran-Vladimir_Zwass.pdf) ; size: 98.4 MB  
- [SUN FORTRAN 77 Language Reference.pdf](attachments/SUN_FORTRAN_77_Language_Reference.pdf) ; size: 3.1 MB  
- [SUN FORTRAN 77 4.0 Reference Manual.pdf](attachments/SUN_FORTRAN_77_4.0_Reference_Manual.pdf) ; size: 872 KB  
- [The New Features of Fortran 2003.pdf](attachments/The_New_Features_of_Fortran_2003.pdf) ; size: 103 KB  
- [Fortran 2004-Working draft.pdf](attachments/Fortran_2004-Working_draft.pdf) ; size: 4.7 MB  
- [Unisoft Fortran Language Reference Manual Sep. 83.pdf](attachments/Unisoft_Fortran_Language_Reference_Manual_Sep83.pdf) ; size: 6.8 MB  
  
## References  
- [Fortran 77 Tutorial](https://en.wikibooks.org/w/index.php?title=Fortran_77_Tutorial&stable=1)  
- [Fortran Resources and Fortran 77/90/95 Compilers for Windows and Linux](http://www.personal.psu.edu/hdk/fortran.html)  
- [Fortran 77 on Atari 8 bit discussed at AtariAge](http://atariage.com/forums/topic/240546-fortran-77-on-atari-8-bit/?hl=+fortran)  
- [Disk images of Apple Fortran](https://mirrors.apple2.org.za/ftp.apple.asimov.net/images/programming/fortran/)  
  
## Images  
![](attachments/Fortran_acs_cover.jpg)  
Original Fortran from IBM  
  
![](attachments/Funktionen-F77.jpg)  
FORTRAN 77 functions  
  
![](attachments/Fortran-Abacus.jpg)  
Abacus FORTRAN for the Commodore C64 - Manual cover from 1988  
  
![](attachments/Fortran-C64.jpg)  
Abacus FORTRAN for the Commodore C64 - from Bob Stover & Tim Adams from 1988  
  
![](attachments/abacus-fortran64-1.jpg)  
Abacus FORTRAN for the Commodore C64 - 1st startscreen from 1986  
  
![](attachments/abacus-fortran64-2.jpg)  
Abacus FORTRAN for the Commodore C64 - Main Menu from 1986  
  
![](attachments/Apple-FORTRAN-Manual-cover.jpg)  
Apple FORTRAN Manual cover from 1980  
