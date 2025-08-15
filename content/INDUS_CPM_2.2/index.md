---
title: INDUS CPM 2.2
---
# INDUS CPM 2.2  
  
This  document explains the specifics of your Indus GT based  CPM 2.2  system.   The  CPM system runs in the Indus GT  disk  drive,  which  contains a Z80 microprocessor,  and 64K of ram (thanks  to  the  ram charger).   The Indus drive in turn,  communicates  with  your Atari computer.   Most of the time,  the Atari computer acts  as a terminal,  but is also used to send data to the printer, and  also  to operate a second disk drive.   The basic nature of  this  environment  is that the Indus is the boss,  and the Atari is the  slave processor in a network based system.  
  
## Requirements:  
  
Indus  GT  disk drive with 64K ramcharger  board,  configured  as drive 1;  an Atari home computer with at least 48K.  Optionally a second  double  density capable drive,  and an  Atari  compatable printer (or 850 interface connected to a printer).  
  
## Boot up:  
  
Insert the terminal disk into the Indus drive and boot the  Atari (with Basic disabled if an XL or XE type computer).  You will see  a menu "A: TRM40", and "B: TRM80".  TRM40 is a 40 column terminal  program  suitable  for  TV's,  TRM80  is  an  80  column  usually  requiring some type of monitor.   Press the "A" key for TRM40  or  "B" for TRM80.  
  
After  the terminal program has been booted,  insert the CPM disk into  the Indus and while holding down the "drive  type"  button, press the "error" button;  this will boot up CPM,  which will ask you  to hit the return key to continue.   At this point your  are booted up and running CPM.  
  
## Terminal emulation  
  
TRM40 emulates an ADM-31, and TRM80 emulates an ADM3A.  
  
TRM40 control keys:  
  
  
|| Key    || Function ||  
| ^bk sp | screen toggle |  
| ^3     | cursor display lock/unlock |  
| ^;     | left shift screen |  
| ^.     | right shift screen |  
  
  
## Second disk option  
  
A  second drive may be used with CPM,  this will be slow as  data  
must  pass thru the Atari computer.   To use drive "2" as  double  
density,  specify  CPM  disk "B:".   To use drive "2"  as  single  
density, specify CPM disk "C:".  When transferring CPM files from  
a  double  density  disk to another double density  disk,  it  is  
faster if the destination disk is put in drive "1" (CPM "A:") and  
the  source disk in drive "2"  (CPM "B:").   Note drive "1"  must  
always be used as a double density disk.   Only drive "2" can  be  
access as a single density drive (as CPM disk "C:").  
  
## Printer option  
  
Any standard Atari printer (or printer hooked up via an Atari 850  
interface) can be accessed using the standard CPM conventions.  
  
## Commands  
  
### CPM.SUB  
  
This  was  the CPM procedure used to install all of  the  Digital  
Research patches for CPM 2.2,  and to create EXSUB.COM.  EXSUB is  
used to get out of XSUB state (refer to the CPM manual).  
  
### INIT.COM  
  
INIT is used to initialize a floppy disk for Indus CPM.  Init can  
format a disk,  generate a bootable disk,  and optionally erase a  
directory.   Run  the "INIT" program and remove your  main  disk,  
insert a fresh disk,  and reply to the prompts as asked.  You can  
optionally  format a disk,  and optionally erase  the  directory.  
INIT  always will copy the boot information,  creating a bootable  
disk.  
  
### ICDS.COM  
  
ICDS  is  used  to copy files to/from  an  Atari  DOS  compatable  
diskette.   The  Atari DOS diskette must be a double density (256  
byte sectors) disk,  such as XLDOS or MYDOS.   ICDS is similar to  
Atari DOS,  with the addition that CPM disks are supported.   Run  
ICDS from drive "1" (CPM disk "A:") and place the Atari DOS  disk  
in drive "2".   To specify a CPM file,  prefix the file name with  
"A:",  to  specify  a DOS file prefix the name  with  "2:".   The  
following commands can be used:  
  
  
|| Key  || Function ||  
| A    | display a directory (specify "A:", or "2:") |  
| C    | copy a file (or files, wild cards supported) |  
| D    | delete a file |  
| H    | display help menu |  
  
  
When transferring a file from Atari format to CPM format, or vice  
versa, you will be asked for text file translation, answer yes if  
the  file  is  a  text  file.    The  conversion  mainly  involes  
converting  the  Atari end-of-line character into a CPM  carriage  
return-line feed sequence (or vice versa).  
  
As an example, the following would be entered after a "C" command  
to copy an Atari file named "TEST.TXT" to a CPM file of the  same  
name:  
```
        2:TEST.TXT,A:
```
In this example, text translation would be desired (enter "Y").  
Note:  MYDOS style subdirectories are supported with ICDS.  
  
The  following  tables  describe the  structures  of  the  double  
density and single density disks used by Indus CPM.  These tables  
are the disk parameter blocks used by CPM to organize the data on  
a  disk.   This  information should be used to configure  "alien"  
disk  programs available on other non-Indus based CPM systems  to  
transfer data to an Indus compatable CPM disk.  
  
Double density:  40 tracks, 18 256-byte sectors per track  
```
                DW        36                ;# CPM RECS/TRK
                DB        3,7,0             ;1K AU PARAMS
                DW        170               ;171*1K=171K DISK SIZE
                DW        63                ;64 DIR ENTRIES
                DB        0C0H,000H         ;DIR PARAMS
                DW        16                ;CSV SIZE
                DW        2                 ;TRACK OFFSET
                                            ; interleave = 1
```
Single density:  40 tracks, 18 128-bytes sectors per track  
```
                DW        18                ;# CPM RECS/TRK
                DB        3,7,0             ;1K AU PARAMS
                DW        84                ;85K DISK SIZE
                DW        31                ;63 DIR ENTRIES
                DB        080H,000H         ;DIR PARMS
                DW        8                 ;CSV SIZE
                DW        2                 ;TRACK OFFSET
        ;                                   ;interleave = 5
                DB        01,06,11,16
                DB        03,08,13,18
                DB        05,10,15
                DB        02,07,12,17
                DB        04,09,14
```
