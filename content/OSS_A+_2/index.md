---
title: OSS A+ 2
---
# OSS OS/A+ Version 2.10; Copyright (C) 1981-1983 OSS, Inc.  
  
## ATR image  
- [OSS OS/A+ Version 2.10](attachments/OSS_OS-Aplus_v2.atr)  
  
## Manuals  
- [OSS OS/A+ manual](attachments/OS_A_Plus_manual.pdf) ; size: 7.2 MB ; thanks to Atarimania! :-)  
- [OSS OS/A+ manual June 1983](attachments/OS_A_Plus_June_83_rev.pdf) ; size: 4.9 MB ; thanks to Atarimania! :-)  
- [OSS OS/A+ bug sheet](attachments/OS_A_Plus_Bug_Sheet.pdf) ; thanks to Atarimania! :-)  
  
(Information from the OSS/A+ 4.0 Handbook)  
## Version 2 File Structure  
  
OS/A+ version 2 was produced to provide the maximum  
compatibility possible with Atari's DOS 2.0s. In fact, the FMS  
used is identical to that used by Atari (for a simple reason: OSS  
wrote Atari's [DOS](../DOS/index.md)). For reasons known best to Atari, OSS were  
instructed to create Atari's FMS around a linked-sector disk  
space management scheme. In essence, this means that the last  
three bytes of each sector in a disk file contain a link to the  
next sector in that same file. The positive result of this is  
that one produces a relatively small, memory-resident, disk  
manager which is nevertheless capable of dynamically allocating  
diskette space (unlike, for example, a contiguous file disk  
manager). The biggest disadvantage of the scheme seems to be  
that one may not do direct (random) access to the bytes of such  
files, as one CAN do with either a contiguous or mapped file  
allocation technique. Also, a disk error in the middle of a  
linked file means a loss of access to the rest of the file.  
  
The purpose of the FMS is to organize the 720 data sectors  
avilable on an 810 (or its double density equivalent) diskette  
into a system of named data files. FMS has three primary data  
structures that it uses to organize the disk:  
  
1. Volume Table of Contents (VTOC): a single disk sector which keeps track of which disk sectors are available for use in data files.  
1. Directory: a group of eight contiguous sectors used to associate file names with the location of the files' sectors on the disk. Each Directory entry contains a file name, a pointer to the first data sector in the file, and some miscellaneous information.  
1. Data Sectors: sectors containing the actual data and some control information that links one data sector to the next data sector in the file.  
  
NOTE: since double density diskette sectors contain 256 bytes  
whereas single density (810 drive) sectors contain only 128,  
certain absolute byte number references may vary depending upon  
the diskette in use. Throughout this chapter, in such cases, the  
single density number is given followed by the double density  
number in square brackets ~[thus~](../thus~/index.md).  
  
## DATA SECTORS  
  
A Data Sector is used to contain the file's data bytes. Each 128 ~[256~](../256~/index.md) byte data sector is organized to hold 125 ~[253~](../253~/index.md) bytes of data and three bytes of control. The data bytes start with the first byte (byte 0) in the sector and run contiguously up to, and including, byte 124 ~[252~](../252~/index.md). The control information starts at byte 125 ~[253~](../253~/index.md)  
  
The sector byte count is contained in byte 127 ~[255~](../255~/index.md). This value is the actual number of data bytes in this particular sector. The value may range from zero (no data) to 125 ~[253~](../253~/index.md) (a full sector). Any data sector in a file may be a short sector (contain less than 125 ~[253~](../253~/index.md) data bytes).  
  
The left six bits of byte 125 ~[253~](../253~/index.md) contain the file number of the file. This number corresponds to the location of the file's entry in the Directory. Directory entry zero in Directory sector $169 has a file number of zero. Entry one in Directory sector $169 has a file number one, and so forth. The file number value may range from zero to 63 ($3F). The file number is used to insure that the sectors of one file do not get mixed up with the sectors of another file.  
  
The right two bits of byte 125 ~[253~](../253~/index.md) (and all eight bits of byte 126 ~[254~](../254~/index.md)) are used to point to the next data sector in the file. The ten bit number contains the actual disk sector number of the next sector. Its value ranges from zero to 719 ($2CF). If the value is zero then there are no more sectors in the file sector chain. The last sector in the file sector chain is the End-Of-File sector. The End-of-File sector will almost always be a short sector.  
  
## DISK DIRECTORY  
  
The Directory starts at disk sector $169 and continues for eight contiguous sectors, ending with sector $170. These sectors were chosen for the directory because they are in the center of the disk and therefore have the minimum average seek time from any place else on the disk. Each directory sector has space for eight file entries. Thus, it is possible to have up to 64 files on one disk.  
  
A Directory entry is 16 bytes in size, as illustrated by the Table below. The directory entry flag field gives specific status information about the current entry. The directory count field is used to store the number of sectors currently used by the file. The last eleven bytes of the entry are the actual file name. The primary name is left justified in the primary name field. The name extension is left justified in the extension field. Unused filename characters are blanks ($20). The Start Sector Number field points to the first sector of the data file.  
  
  
|| Starting Byte # of Field || Length of Field (bytes) ||   Purpose of Field  ||  
| 0                                 | 1                                  | Flag byte. Meanings of bits: $00 Entry never used $80 Entry was deleted $40 Entry in use $20 Entry protected $02 a version 2 file $01 Now writing file |  
| 1                                 | 2                                  | Count (LSB,MSB) of sectors in file |  
| 3                                 | 2                                  | Start sector (LSB,MSB) of link chain  |  
| 5                                 | 8                                  | File name, primary  |  
| 13                               | 3                                  | File name, extension |  
  
  
  
NOTE: only eight file directory entries are stored per sector, even on double density diskettes.  
  
![](attachments/version2dir.png)  
  
  
Table: Directory Entry Structure  
  
## VOLUME TABLE OF CONTENTS (VTOC)  
  
The VTOC sector ($168) is used to keep track of which disk sectors are available for data file usage. The Table below illustrates the organization of the VTOC sector. The most important part of the VTOC is the sector bit map.  
  
The sector bit map is a contiguous string of 90 bytes, each of which contains eight bits. There are a total of 720 (90 x 8) bits in the bit map -- one for each possible sector on an 810 diskette. The 90 bytes of bit map start at VTOC byte ten ($OA). The leftmost bit ($80 bit) of byte $OA represents sector zero. The bit just to the right of the leftmost bit ($40 bit) represents sector one. The rightmost bit (bit $01) of byte $63 represents sector 719.  
  
  
  
|| Starting Byte # of Field || Length of Field (bytes) ||   Purpose of Field  ||  
| 0                                  | 1                                 | Reserved (for type code) |  
| 1                                  | 2                                 | Total number of sectors |  
| 3                                  | 2                                 | Number of unused sectors |  
| 5                                  | 5                                 | Reserved   |  
| 10                                | 90                               | Sector usage bit map. Each bit represents a particular sector: a 1 bit indicates an available sector, a 0 bit indicates a sector in use. |  
| 100                              | 28                               | Reserved (could be used for version 2 type DOS with more than 720 sectors per disk) |  
  
  
Table: Structure of the VTOC Sector  
  
## Picture  
![](attachments/OS_A_Plus_d7.jpg)  
OSS/A+ Version 2 diskette ; thanks to Atarimania! :-)  
