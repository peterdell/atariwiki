---
title: Atari Datasette XC12 Turbo 6000 Baud Interface
---
The purpose of this interface is to use high transfer rates for compact cassettes which are used with the XC12 Datasette. The roots are about 10 years ago, in Eastern Germany it was unimaginable expensive to buy a floppy station. That's why the people searched for other ways because they were not satisfied with the slow original Datasette. The whole system was called "CHAOS SYSTEM" and it uses 6000 Baud for data transfers. Just build the small interface into the XC12 and you're ready to go.  
  
The structure of the files is much the same like for diskette files. To run the software the files on cassette must be loaded with the "CHAOS LOADER". For copy purposes the "CHAOS COPY" has to be used. Both can be loaded either by a cartridge or as a normal cassette file: put the compact cassette into the XC12, boot Atari up with OPTION+START pressed, press PLAY on Datasette and then SPACEBAR on the Atari keyboard.  
  
After the "CHAOS LOADER" started put in your Turbo Software cassette and press PLAY. If a suitable file is found the "CHAOS LOADER" displays its name on the screen. Press SPACEBAR to load it or RESET for searching the next. After loading the file it will be started. With "CHAOS COPY" you can copy Turbo Software, not much to say.  
  
There are several utilities to transfer files between normal cassette and turbo system or floppy station and turbo system:  
*Turbo-Cas-Trans: (TURBTRAN.COM TURBOCC.CAS) transfers turbo files to normal (600 baud) cassette files  
*Cas-Turbo-Trans: (CCTURBO.COM) transfers normal cassette files to turbo files  
*Turbo-Disk-Trans: (TDTRANS.COM TD2.COM TD3.COM) copies files from Turbo to Disk  
*Disk-Turbo-Trans: (DT2.COM DTTRANS.COM DTTRANS2.COM) copies files from Disk to Turbo  
All the software is provided on a disk. The .COM files must usually be loaded from a DOS. The .CAS files must be copied to a cassette and then used in the appropriate manner. Use the 'C'-command in DOS for copy them (source, target e.g. D:CHAOSLAD.CAS, C:).  
  
## BIN image  
[TURBOMOD.BIN](attachments/TURBOMOD.BIN) ; ROM image for use with the interface. Thanks to Torsten Berthold!  
  
## ATR image  
[TURBUTIL.ATR](attachments/TURBUTIL.ATR) ; Turbo Tape Utilities. A disk with several utilities. An Atari XL/XE & XC 12 with Turbo 6000 Baud interface is required.  
  
## Source code  
[https://github.com/baktragh/turgen_tape_loaders](https://github.com/baktragh/turgen_tape_loaders)  
  
## Table of Software used with the Turbo interface and maximum baud rates  
still missing...  
|| # || Program name || max. Baud rate   
| 1| Atari Datasette | 600   
| 2| ... | 6000   
  
## Parts  
*1 × A302 (or TDA345 - not tested)  
*1 × B621 (or TCA321A or LM311 - not tested)  
*2 × 1 k&Omega; resistor  
*2 × 4.7 k&Omega; resistor  
*2 × 51 k&Omega; resistor  
*2 × 12 k&Omega; resistor  
*1 × 2.2 µF capacitor  
*1 × 47 nF capacitor  
*1 × 22 nF capacitor  
  
## Diagrams  
![](attachments/turb_sch.gif)  
Circuit diagram of the Turbo interface  
  
![](attachments/turb_brd.gif)  
Closer view with more details in part of the circuit diagram above  
