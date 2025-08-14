# Disk formats / Diskettenformate  
  
||Format||Sides||Tracks/Diskside||KBit||Recording||Bytes/Sector||Sector/Track||Disksize||ATR Size 1)  
|Single SD|1|40|125|FM|128|18|90 KB|92.176 2)  
|Medium/Enhanced MD|1|40|250|MFM|128|26|130 KB|133.136 2)  
|Double DD|1|40|250|MFM|256|18|180 KB|183.952 3)  
|Quad DS/DD/40 Tracks|2|40|250|MFM|256|18|360 KB|368.272 3)  
|Octo DS/DD/80 Tracks|2|80|250|MFM|256|18|720 KB|736.912 3)  
|High|2|80|500|MFM|256|36|1.440 KB|1.474.192 3)  
|Extra High|2|80|1.000|MFM|256|72|2.880 KB|2.948.752 3)  
|Harddisk|1|1|x|MFM|128|65.535|8 MB|8.388.496 2)  
|Harddisk|1|1|x|MFM|256|65.535|16 MB|16.776.592 3)  
|Harddisk|1|1|x|MFM|512|65.535|32 MB|33.553.936 4)  
1) XFD: subtract -16 Bytes (ATR Header), therefore add +384 Bytes! (XFD saves the full boot sector size / disksize, BUT it does not / cannot save the full sector data – these additional 384 bytes are simply empty!)  
  
2) full byte size / disksize (has 128 bytes boot sectors, thus no need to subtract 384 Bytes!)  
  
3) byte size minus boot sectors (has 256 byte boot sectors, thus 3x 128 bytes = 384 bytes already subtracted, since the Atari OS only allows 128 byte boot sectors from diskette! the real disksize is therefore 384 bytes larger, but that data is not transfered from the floppy to the computer! most A8 floppy drives would require a firmware change to read/transfer full 256 bytes bootsectors)  
  
4) harddisks can use full 512 bytes for bootsectors! floppy disks are still limited to 128 bytes bootsectors!  
  
  
  
## Diskformats and DOS versions supporting them  
  
||DOS||90KB||130KB||180KB||360KB||720KB||1.440KB||Remark  
|[DOS 1.0](../Atari_DOS_1/index.md)|Y|N|N|N|N|N|  
|[DOS 2.0](../Atari_DOS_2/index.md)  SmartDOS|Y|N|Y|N|N|N|DOS 2.0s can read 180k after a Reset; DOS 2.0d can read 90k after a Reset!  DOS.SYS of SmartDOS is based on DOS 2.0! (Rainbow DOS and Black DOSare merely DUP.SYS replacements for DOS 2.0s or DOS 2.0d, there are many others...)  
|[DOS 2.5](../Atari_DOS_2/index.md)|Y|Y|N|N|N|N|  
|[DOS 3.0](../Atari_DOS_3/index.md)|Y|Y|N|N|N|N|  
|[DOS 4.0](../Atari_DOS_4/index.md)|Y|N|Y|Y|N|N|  
|[DOS XE](../Atari_DOS_XE/index.md)|Y|Y|Y|Y|N|N|  
|[Bibo DOS 6.x](../Bibo-DOS/index.md)|Y|Y|Y|Y|N|N|  
|[Turbo DOS 2.x](../Turbo-DOS/index.md)|Y|Y|Y|Y|N|N|  
|[Top DOS 1.5 Prof](../TOP-DOS/index.md)|Y|Y|Y|Y|?|N|  
|Mach DOS 3.7|Y|N|Y|Y|N|N|  
|[MyDOS 4.5x](../MyDOS/index.md)|Y|Y|Y|Y|Y|N|MyDOS requires a special / external formatter to format 1440 KB- one is available e.g. with the CSS Black Box or the CSS Floppyboard,maybe there are also some other external formatters...?!?  
|[Sparta DOS 3.2x/3.3x](../SpartaDOS/index.md)|Y|Y|Y|Y|Y|Y|  
|Real DOS 2.x|Y|Y|Y|Y|Y|Y|  
|BeweDOS 1.x|Y|Y|Y|Y|N|N|a 720k or 1440k disk must be formatted with SpartaDOS orSDX or Real DOS, then Bewe DOS can be copied onto it!  
|[SDX 4.x](../SpartaDOS/index.md)|Y|Y|Y|Y|Y|Y|  
|[Lite DOS 2.x/3.X](http://www.mr-atari.com/Mr.Atari/LiteDOS/)|Y|Y|Y|Y|Y|?|  
|[Super DOS 5.x](../SuperDOS/index.md)|Y|Y|Y|Y|N|N|  
|DOS II+D 4.5|Y|Y|N|N|N|N|  
|DOS II+D 6.x|Y|Y|Y|N|N|N|  
|[XDOS 2.43](../XDOS_2.43/index.md)|Y|Y|Y|Y|N|N|in 360k mode the two disksides are used as twofloppy drives (D1: and D2:) in XDOS!  
|KDOS 1.0|Y|N|N|N|N|N|  
|[OSS A+2.0](../OSS_A__2/index.md)|Y|N|Y|N|N|N|  
|[DOS XL 2.3x](../OSS_DOS_XL/index.md)|Y|N|Y|N|N|N|  
|[OS A+4.1](../OSS_A__4/index.md)|N?|Y|Y|Y|Y|Y|OS A+4.1 was advertized being capable of 128 BpS,256 BpS and 512 BpS, any format from 128 KB to approx. 15,6 MB!  
  
  
  
## Harddisk partition formats and DOS versions supporting them  
  
### 128 Byte sectors (single density)  
||Partition SizeSectors||512 K4.095||1 M8.191||2 M16.383||4 M32.767||8 M65.535||Remark  
|Top DOS 1.5 Prof|Y|Y|Y|Y|Y|Top DOS Prof. should support subdirs and harddisks,but I have no clue how! (manuals and information missing!)  
|MyDOS 4.5x|Y|Y|Y|Y|Y|  
|SpartaDOS 3.2x/3.3x|Y|Y|Y|Y|Y|  
|RealDOS 2.x|Y|Y|Y|Y|Y|  
|MyDOS 4.5x|Y|Y|Y|Y|Y|  
|BeweDOS 1.x|Y|Y|Y|Y|Y|harddisk must be formatted with Sparta DOS or SDX or Real DOS,then Bewe DOS can be copied onto it!  
|LiteDOS 2.x/3.x|Y|Y|Y|Y|Y|  
|DOS XE|Y|Y|Y|Y|Y|DOS XE does support subdirs, but harddisks up to 16MB can only be used with sup8pdct's homebrew DOS XE formatter!  
|OS A+ 4.1|Y|Y|Y|Y|Y|OS A+ 4.1 was advertized being capable of 128 BpS,256 BpS and 512 BpS, any format from 128 KB to approx. 15,6 MB!  
  
  
  
### 256 Byte sectors (double density)  
||Partition SizeSectors||1 M4.095||2 M8.191||4 M16.383||8 M32.767||16 M65.535||Remark  
|Top DOS 1.5 Prof|Y|Y|Y|Y|Y|Top DOS Prof. should support subdirs and harddisks,but I have no clue how! (manuals and information missing!)  
|MyDOS 4.5x|Y|Y|Y|Y|Y|  
|SpartaDOS 3.2x/3.3x|Y|Y|Y|Y|Y|  
|RealDOS 2.x|Y|Y|Y|Y|Y|  
|BeweDOS 1.x|Y|Y|Y|Y|Y|harddisk must be formatted with Sparta DOS or SDX or Real DOS,then Bewe DOS can be copied onto it!  
|SDX 4.x|Y|Y|Y|Y|Y|  
|LiteDOS 2.x/3.x|Y|Y|Y|Y|Y|  
|DOS XE|Y|Y|Y|Y|Y|DOS XE does support subdirs, but harddisks up to 16MB can only be used with sup8pdct's homebrew DOS XE formatter!  
|OS A+ 4.1|Y|Y|Y|Y|Y|OS A+ 4.1 was advertized being capable of 128 BpS,256 BpS and 512 BpS, any format from 128 KB to approx. 15,6 MB!  
  
  
### 512 Byte sectors (quad density)  
||Partition SizeSectors||1 M2.047||2 M4.095||4 M8.191||8 M16.383||16 M32.767||32 M65.535||Remark  
|Top DOS 1.5 Prof|N|N|N|N|N|N|  
|MyDOS 4.5x|N|N|N|N|N|N|  
|SpartaDOS 3.2x/3.3x|N|N|N|N|N|N|  
|RealDOS 2.x|N|N|N|N|N|N|  
|BeweDOS 1.x|N|N|N|N|N|N|  
|SDX 4.x|Y|Y|Y|Y|Y|Y|  
|LiteDOS 2.x/3.x|N|N|N|N|N|N|  
|DOS XE|N|N|N|N|N|N|  
|OS A+ 4.1|Y|Y|Y|Y|Y|?|OS A+ 4.1 was advertized being capable of 128 BpS,256 BpS and 512 BpS, any format from 128 KB to approx. 15,6 MB!  
  
  
## Andere Quellen  
- [Diskettenformate.pdf](attachments/Diskettenformate.pdf) ; Thank you so much [Bernhard Pahl](http://www.b-pahl.de/atari8bit/8-Bit-Daten/8-Bit-Daten.html#disk) for providing this information! :-)  
