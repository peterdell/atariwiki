---
title: SynCalc
---
# SynCalc Copyright (C) 1983, 1985 Synapse Software Corp. and Mike Silva  
  
  
SynCalc from Synapse and programmed by Mike Silva is the(!) spreadsheet for the Atari 8 bit. No program of that kind reaches the performance SynCalc does.  
  
In 2016 Mike Silva gave SynCalc into public domain including source code! Mr. Silva, the Atari community is forever in your debt! Thank you so much, we really appreciate your help. You are now in the hall of fame.  
  
![](attachments/Thank_you_Mike_Silva.jpg)  
Thank you Mike Silva!!!  
  
Further credit goes to Brian Lee, the product manager, who was very involved in guiding the look-and-feel and the overall functionality of the program. Thanky you so much Mr. Lee, we really appreciate your help, then and now. :-)  
  
Because the source code listing as well as the disk files are lost, it would be cool, if someone out there is in the possession of that, if you can share it with the community. Many thanks in advance. :-)  
  
Officially, 2 version were sold, one from 1983 and the other from 1985. Of course, there are others out there in the web, mostly patched and cracked ones.  
Versions:  
- 1983 Version, works with all models and Axlon (up to 256k) compatiable RAM expansions, ATX available  
- 1985 Version, works with all models and Axlon (up to 256k) and XE (up to 64k) compatible RAM expansions, ATX available  
- 1993 Version, works only with XL/XE models and XE (up to 256k) compatiable RAM expansions ATR available  
## 1983 Version  
The 1983 version was the first one, it had some bugs, but was and still is marvelous. The only bug we know is as follows:  
if you have a value in the 255th line and insert one line more, the Atari crashes and your work is lost. In my opinion a bug we can live with. __If you have a bug-list of the 1983 version, please let us know. Your help is very much appreciated in this case.__  
  
## 1985 Version  
The 1985 version should be free of bugs, further, it was sold with a template disk, please see below. This version uses extended RAM, if available. For example, in an Atari 130XE there is more than 80 KB RAM available. But the user has to take care, because the limit for storing data on diskette is 90 KB. __The goal should be, to create an atr-image for all Ataris (Classic, XL, XE) free of bugs and just limited to the installed RAM. Further, to get rid of the 90 KB data storage limit.__  
  
## 1993 Version  
  
Appears to be based on the 1983 version. All "STA $CFFF" bank select statements are replaced by "JSR $0101", pointing to a small subroutine that maps the Axlon bank number to and XE bank in PORTB.  
  
||Port B |FF |EF|EB|E7|E3|AF|AB|A7|A3|8F|8B|87|83|FF|FF  
||Model  | 800/XL |130 XE |130 XE | 130 XE | 130 XE  | RAMBO | RAMBO | RAMBO | RAMBO | RAMBO | RAMBO | RAMBO | RAMBO | n/a | n/a  
|| Total RAM (k) | 48/64  |128    |128    | 128    | 128     | 192   | 192   | 192   | 192   | 256   | 256   | 256   | 256   | n/a | n/a  
  
See also [http://atariage.com/forums/topic/208094-who-can-crack-this-one](http://atariage.com/forums/topic/208094-who-can-crack-this-one).  
## Manuals  
- [SynCalc-1983 Version](attachments/Synapse_SynCalc_1983.pdf) ; size: 7,6 MB  
- [SynCalc-1985 Version](attachments/Synapse_SynCalc_1985.pdf) ; size: 13,3 MB  
- [SynCalc Template Disk](attachments/SynCalc_Template_Disk_Synapse.pdf) ; size: 8 MB  
## ATR images  
- [SynCalc_1983Synapse_SoftwareUS.atx](attachments/SynCalc_1983Synapse_SoftwareUS.atx) ; atx-image of the 1983 version which runs properly, icluding the VisiCalc import program, which is missed on nearly all(!) versions  
- [SynCalc_1985Synapse_SoftwareUS.atx](attachments/SynCalc_1985Synapse_SoftwareUS.atx) ; atx-image of the 1985 version which runs properly, icluding the VisiCalc import program, which is missed on nearly all(!) versions  
- [SynCalc 128K atx-version](attachments/SynCalc_128K_1985.atx) ; atx-image which runs on Altirra, but not with the Atari800MacX emulator (2016)  
- [SynCalc 128K atr-version](attachments/SynCalc_128K_1993.atr) ; atr-image which runs on all emulators, but not verified yet regarding reliable calculations  
- [SynCalc Template Disk](attachments/Syncalc_Template_original.atr) ; atr-image from the original diskette  
- [SynCalc Data Disk.atr](attachments/SynCalc_Data_Disk.atr) ; atr-image with some examples and templates  
  
- [SynCalc Classic for 400-800 Ataris](attachments/SynCalc_Classic.atr) ; not yet tested, use on your own risk  
- [SynCalc for XL-XE-Ataris](attachments/SynCalc_XL-XE.atr) ; not yet tested, use on your own risk  
- [SynCalc with OSS DOS XL 2.30 as file version](attachments/SynCalc_with_OSS_DOS_XL_2.30.atr) ; not yet tested, use on your own risk  
## RAW files from the Kryoflux  
- [Kryoflux-raw-no-flippy.zip](attachments/Kryoflux-raw-no-flippy.zip) ; size: 22.9 MB ; A very big thank you goes to Freddy Offenga for creating the raw files from our original SynCalc 128K diskette. Freddy, great work! Thank you so much! :-)  
## RAM configuration; findings from JAC! from AtariAge  
__From p. 5 of the documenation:__  
"What You Will Need  
1. An ATARI home computer  
2. An ATARI disk drive (up to 2).  
3. The program diskette, enclosed in the inside front cover pocket of the manual.  
4. At least 48K of memory.  
5. A TV set or other video monitor. A black and white set will work.  
6. Blank diskettes for storing data.  
Optional:  
ATARI printers for obtaining hard copy versions of reports.  
You can also use the Axlon Rampower 128K or Mosaic 64K Select to increase your computer's capacity."  
  
__From p. 9 of the documenation:__  
"NOTE: The memory indicator will be nnn/NNN where nnn = amount of memory used in K bytes and NNN = total amount of memory available in K bytes (1 K byte is equal to 1024 characters). When you notice that the memory indicator shows that the worksheet is becoming full, you should save the worksheet to disk and then reload it. This may free up additional memory space. The amount of memory will vary according to the configuration of your computer."  
  
  
|| Hardware || Base RAM || Expansion || Free Memory in 1983 Version || Free Memory in 1985 Version || Free Memory in 1993 Version  
| Atari 800    | 48k | none         |  21k |  21k | n/a  
| Atari 800    | 52k | none         |  25k |  25k | n/a  
| Atari 800    | 48k | 64k Axlon    |  69k |  69k | n/a  
| Atari 800    | 48k | 128k Axlon   | 133k | 133k | n/a  
| Atari 800    | 48k | 256k Axlon   | 245k | 245k | n/a  
| Atari 800    | 48k | 512k Axlon   | 245k | 245k | n/a  
| Atari 800    | 48k | 1024k Axlon  | 245k | 245k | n/a  
| Atari 800    | 48k | 2048k Axlon  | 245k | 245k | n/a  
| Atari 800    | 48k | 4096k Axlon  | 245k | 245k | n/a  
| Atari 800 XL | 64k | none         |  21k |  21k |  21k  
| Atari 800 XL | 64k | 256k Rambo   |  21k |  84k | 213k  
| Atari 800 XL | 64k | 256k Compy   |  21k |  84k | 149k  
| Atari 800 XL | 64k | 512k Rambo   |  21k |  84k | 213k  
| Atari 800 XL | 64k | 512k Compy   |  21k |  84k | 149k  
| Atari 800 XL | 64k | 1024k Rambo  |  21k |  84k | 213k  
| Atari 130 XE | 64k | 64k Atari    |  21k |  84k |  85k  
  
The disk contains a boot loader in the sectors 1-8 and two versions of the program. The first version starts at sector 18 ($12) supports the Axlon compatiable memory expansions with the banking register $CFFF. The second version starts at sector 62 ($3E) and  supports the XE compatible memory expansions with the banking register $D301 (PORTB). In both cases, the extended memory is banked in at $4000. If an extended memory bank at $4000 is available for the banking value $E3 during the boot process, the second version is loaded.  
  
  
{{1B3B: LDY #$EF  
1B3D: LDA #$E3  
1B3F: STA PORTB  
1B42: TXA  
1B43: STA $4000,X  
1B46: STY PORTB  
1B49: EOR #$FF  
1B4B: STA $4000,X  
1B4E: INX  
1B4F: BPL $1B3D  
1B51: LDX #$00  
1B53: LDA #$E3  
1B55: STA PORTB  
1B58: TXA  
1B59: CMP $4000,X  
1B5C: BNE $1B6C  
1B5E: INX  
1B5F: BPL $1B58  
1B61: LDA #$3E  
1B63: STA $84  
1B65: LDA #$00  
1B67: STA $85  
1B69: JMP $1B74  
1B6C: LDA #$12  
1B6E: STA $84  
1B70: LDA #$00  
1B72: STA $85}}  
... load main part  
  
## Findings from Mike Silva:  
Zero page  
  
$95    Current Spreadsheet Row (all rows and columns are zero-based)  
$96    Current Spreadsheet Column  
  
$99    Current Screen Y  
$9A    Current Screen X  
  
$9F    Current Cell Data Pointer (points to data of current cell)  
  
$A7    Last Spreadsheet Row  
$A8    Last Spreadsheet Column  
  
$CA    Last Added Cell Data Pointer (a stack pointer to next free memory to add new cell data)  More below #1  
  
Non-zero page  
  
$1901  Array of column widths  
  
$19DB  Last direction of cursor movement (1=left, 2=right, 3=up, 4=down)  
  
$1A00  Screen memory  
  
$2BF3  Array of 3-byte cell structures.  Each structure consists of a 2-byte cell data address, followed by one additional byte (more below #2).  Array order is A1, B1, C1,...n1, A2, B2, C2,...n2,...Am, Bm, Cm,...nm where n is last sheet column, m is last sheet row.  
  
#1 Cell data is form B1, B2, B3, cell data (variable number of cell data bytes).  
B1: D7-D6 = number format code  
D5 = comma flag  
D4 = dollar flag  
D3 = percent flag  
D2 = ??? haven't figured this one out  
D1-D0 = sign code  
B2: D7-D6 = justify code  
D5-D4 = ??? haven't figured this one out  
D3 = protect value flag  
D2-D0 = margin value 0-7  
B3: D7 = protect entry flag  
D6-D0 = length of cell data that follows  
  
Cell data is either text or ATARI numeric.  In formula cells the value of the formula is first, followed by the actual formula.  
  
#2 Additional cell info byte  
D7-D6 = cell type (01 = text, 10 = numeric, 00 = empty cell?)  
D5-D2 = precision value  
D1-D0 = ???  
  
The cell data stack grows downward from $7FFF on a 48k machine.  By testing other hardware it will be possible to see where the stack begins in different memory circumstances, and also perhaps to ID some other addressing bits in the cell pointer array, bits that are just zero in the base 48k version.  
  
## Problems when importing VisiCalc files ; findings from luckybuck  
SynCalc holds an import program, called: 'VC->SC' in order to read in files from the VisiCalc program. All versions(!) out there, except the original ones are not able to import properly VisiCalc files! The SynCalc program tries to load a convert program from the original program disk. If this fails, you get the following pictures:  
![](attachments/1.jpg)  
SynCalc VC->SC option selected  
  
![](attachments/2.jpg)  
SynCalc asking for the program master disk  
  
![](attachments/3_.jpg)  
SynCalc failed to load a program from the program master disk  
  
Further, if you have really hard VisiCalc spreadsheets and the 1985 version even in original form fails to import, try the 1983 version, which works like a charm in these very rare cases.  
  
## Private Notes from JAC! in German  
Syncalc werde ich mir irgendwann nochmal im Detail anschauen, aber das braucht Zeit.  
So wie ich das ganze sehe, was SyncCalc im Original eine XEX die von Synapse auf  
einen DOS Disk mit einem entsprechenden DOS gepackt und dann verschlüsselt wurde.  
Die Boot-Disk packt das DOS dann sozusagen wieder aus.  
Nur so kann sie nach dem Booten Files von den Datendisk lesen.  
  
## Emulator Hints  
In emulators it could be useful to turn the SIO patch off for using the ".ATX" disk images.![](attachments/SIO.jpg)  
## File types  
The program disk itself has a hidden VTOC and is heavily copy protected. A really hard one, even in todays times. SynCalc saves produces three types of files (syntaxes):  
a) SC for worksheets  
b) DIF for data interchange files (or values)  
c) TXT for reporting  
Thank you Wade Ripdubski for finding out and sharing your knowledge with us. :-)))  
![](attachments/files.png)  
SynCalc file syntax  
  
![](attachments/rating.png)  
SynCalc rating from Wade Ripdubski (InverseATASCII). AtariWiki fully admits that rating. Mike Silva has done a men's jpb. Shaft's score would be a 10 out of 10.  
Please also take a look at Wade's site: [SynCalc at InverseATASCII](http://inverseatascii.info/2016/02/23/s2e08-synapse-software-syncalc/) ; highly recommended!  
## References  
[Synapse Wiki](https://en.wikipedia.org/wiki/Synapse_Software)  
[Br0derbund Wiki](https://en.wikipedia.org/wiki/Brøderbund)  
[SynCalc at InverseATASCII](http://inverseatascii.info/2016/02/23/s2e08-synapse-software-syncalc/)  
## Video  
- [Commercial video with Alan Alda about SynCalc from Atarimania](attachments/atari_8bit_synapse_software_alan_alda_commercial.flv) ; a big thank you to Atarimania ; funny to watch! :-)  
## Images  
![](attachments/1Startscreen.gif)  
SynCalc startscreen ; thanks to Atarimania  
  
![](attachments/2Start.gif)  
SynCalc start of program ; thanks to Atarimania  
  
![](attachments/3popup.gif)  
SynCalc pop up window ; thanks to Atarimania  
  
![](attachments/SynCalc_requires_48k_of_RAM.jpg)  
SynCalc requires 48k of RAM and all cartridges removed  
  
![](attachments/max.jpg)  
Maximum RAM in KB available for SynCalc regardless how many is installed  
  
![](attachments/Synapse_Syncalc_with_128K.jpg)  
Synapse Syncalc with 128 KB RAM startscreen with 85 KB RAM free  
  
![](attachments/RAM-Vertelung_markiert.jpg)  
Synapse Syncalc with different machines and different free RAM  
  
![](attachments/1983-1.jpg)  
SynCalc 1983 version-front of box ; thanks to Atarimania  
  
![](attachments/1983-2.jpg)  
SynCalc 1983 version-back of box ; thanks to Atarimania  
  
![](attachments/1983-3.jpg)  
SynCalc 1983 version-diskette ; thanks to Atarimania  
  
![](attachments/SynCalc_128K-1.jpg)  
SynCalc 1985 version-front of box  
  
![](attachments/SynCalc_128K-2.jpg)  
SynCalc 1985 version-back of box  
  
![](attachments/SynCalc_128K-3.jpg)  
SynCalc 1985 version-side of box  
  
![](attachments/templates1.jpg)  
SynCalc Template Diskette - image 1 ; thanks to Atarimania  
  
![](attachments/templates2.jpg)  
SynCalc Template Diskette - image 2 ; thanks to Atarimania  
  
![](attachments/SynCalc_Templates_Disk_5.jpg)  
SynCalc Template Diskette - image 3 ; thanks to RHOD  
  
![](attachments/SynCalc_Templates_Disk_4.jpg)  
SynCalc Template Diskette - ad 1  
  
![](attachments/SynCalc_Templates_Disk_3.jpg)  
SynCalc Template Diskette - ad 2  
  
![](attachments/syncalc_1985_ad.jpg)  
SynCalc ad ; thanks to Atarimania  
  
![](attachments/ad.jpg)  
SynCalc ad from eBay  
