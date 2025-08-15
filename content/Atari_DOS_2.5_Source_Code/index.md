---
title: Atari DOS 2.5 Source Code
---
# Atari DOS 2.5 Source Code from OSS ; (C) 1985 Atari, Inc. and OSS, Inc.  
---
TITLE "FMS - Dual Density for Atari 1050 drives (2.50)"  
PAGE "     --- Copyright and Author Notice ---"  
  
Copyright (c) 1978,1979,1980,1982,1984  
Optimized Systems Software, Incorporated  
San Jose, California  
  
THIS PROGRAM MAY NOT BE REPRODUCED,  
STORED IN A RETRIEVAL SYSTEM, OR  
TRANSMITTED IN WHOLE OR IN PART,  
IN ANY FORM, OR BY ANY MEANS, BE IT  
ELECTRONIC,MECHANICAL, PHOTOCOPYING,  
RECORDING, OR OTHERWISE WITHOUT THE  
PRIOR WRITTEN PERMISSION OF  
OPTIMIZED SYSTEMS SOFTWARE, INC.  
1221-B KENTWOOD AVENUE  
SAN JOSE, CALIFORNIA 95129 (U.S.A.)  
  
PHONE:  (408) 446-3099  
  
Originally designed and coded by  
Paul Laughton of Shepardson Microsystems, Inc.  
  
Modified for Atari 1050 and 130XE by  
Mark Rose & Bill Wilkinson  
of O.S.S., Inc.  
  
January, 1985  
---
This is the working source code from OSS, Inc. for the Atari DOS 2.5 system software. We deeply thank:  
  
__Paul Laughton__  
__Mark Rose__  
__Bill Wilkinson__  
  
for writing the software and the following users from AtariAge:  
  
ndary  
bob1200xl  
ivop  
Urchlay  
  
for preserving the source code for generations to come.  
## How to build Atari DOS 2.5 from OSS  
First, please read these two text files and have 48 KB RAM in your Atari:  
- [README.txt](attachments/README.txt) ; Text file, which introduces all files needed to create a running DOS 2.5 disk.  
- [Building_the_OSS_DOS_2.5_sources_on_the_Atari.txt](attachments/Building_the_OSS_DOS_2.5_sources_on_the_Atari.txt) ; This is the recipe on how to do it.  
  
Then, please go on with these disk images:  
- [builddos.atr](attachments/builddos.atr) ; DOS II 2.0s disk image with all files needed to create DOS 2.5 with the below given files.  
- [empty.atr](attachments/empty.atr) ; Blank DOS II 2.0s formatted disk-image to work with the above files.  
- [mac65102.car](attachments/mac65102.car) ; MAC/65 Version 1.02 cartridge to read in the above MAC/65-files. Many thanks to AtariGeezer from AtariAge for giving us that rare to find 034M-cartridge from OSS.  
  
The above image builddos.atr needs the following source files. Here we can go on in two ways:  
  
a) the easy one:  
  
If you have booted with the above disk image, please insert either the dossrc_a-w.atr image or the dossrc-w.atr image in drive 2 (D2:):  
- [dossrc_a-w.atr](attachments/dossrc_a-w.atr) ; Working source code for building the FMS (File Management System -> DOS.SYS-file) on an SD ATR-image with MAC/65-files.  
- [dossrc_b-w.atr](attachments/dossrc_b-w.atr) ; Working source code for building the DUP.SYS-file on an SD ATR-image with MAC/65-files.  
- [dossrc-w.atr](attachments/dossrc-w.atr) ; Same as the both images above, but on just a single DD ATR-image with DOS 2.0D.  
  
Then type:  
LOAD #D2:FMS.M65  
ASM  
You should receive the following figure:  
![](attachments/DOS.jpg)  
Successful assembled source code for the creation of DOS.SYS  
  
Then insert either the dossrc_b-w.atr image or leave the dossrc-w.atr image in drive 2 (D2:):  
  
Then type:  
LOAD #D2:DUP.M65  
ASM  
You should receive the following figure:  
![](attachments/DUP.jpg)  
Successful assembled source code for the creation of DUP.SYS  
  
Congratulations! You have created the object code for building DOS 2.5. :-)))  
On how to go on further, please read the recipe above.  
  
b) the hard one:  
  
The way is the same as in example a), except, that the below given original source files:  
- [dossrc_a.atr](attachments/dossrc_a.atr) ; Original source code for building the FMS (File Management System -> DOS.SYS-file) on an SD ATR-image with MAC/65-files.  
- [dossrc_b.atr](attachments/dossrc_b.atr) ; Original source code for building the DUP.SYS-file on an SD ATR-image with MAC/65-files.  
- [dossrc.atr](attachments/dossrc.atr) ; Same as the both images above, but on just a single DD ATR-image with DOS 2.0D.  
  
have to be patched to actually work. Please read the recipe above on how to this.  
