---
title: SpartaDosXReview
---
# Sparta Dos X Review  
  
The SpartaDOS X cartridge  
a review  
by  Doug Wokoun  
  
(copied from Usenet)  
  
The SpartaDOS X cartridge is the latest incantation of SpartaDOS for  
the 8-bit Atari and very possibly the most powerful Disk Operating System  
available for any 8-bit computer.  
  
The SpartaDOS X cartridge consists of 64K of ROM, with 48K (or 6  
cartridge banks) formatted into a ROM-disk, and the remaining 16K used as the  
main DOS core.  The ROM-disk contains files and drivers used by the system  
and SpartaDOS X versions of several utilities found in the SpartaDOS ToolKit.  
It also contains a very versatile ARC utility package.  
  
  
Some of the new features of SpartaDOS X (referred to as SDX):  
  
- built in, memory resident FORMAT utility.  Old versions of SpartaDOS could only initialize Atari format disks using 'AINIT'.  To           initialize a SpartaDOS disk required the loading of a program called 'XINIT'.  Now, any time an XIO #254 call is made, the SDX format           menu is brought up.  With this, you can select a variety of disk densities and types.  It will also allow "1-second" formatting by           simply rewriting the root directory on a formatted disk.  
- High speed disk I/O with U.S. Doubler, Atari XF551, and Indus GT disk drives.  
- New file loader supporting relocatable files (certain disk based commands can be held in memory and later removed) and symbol linking.  
- Probably the lowest MEMLO of any DOS.  The DOS can load drivers under OS-RAM, into extended memory on an XE or at MEMLO on an 800.  
- Environment variables: user definable PROMPTs, search PATHs, parameter passing on batch files, and a CARtridge or BASIC memory save           capability will retain programs even if the machine is shut off.  
- The ability to go from a cartridge to internal BASIC without rebooting.  The CAR command enters the external cartridge, "BASIC" enters internal BASIC.  You can go from Turbo BASIC XL to Atari BASIC to BASIC XE without rebooting! (with some provisions)  
- Support of up to 1 Meg internal memory as a RAMDisk.  
- "Persistent" batch files.  Continued batch file processing even after loading binary programs.  
- Fast, powerful, versatile ARC utilities.  Supports ALF files.  With these, you can Add files to an ARChive, Move (delete after          Adding), Freshen (update files by date), Update (Freshen with Add capability), Delete files from an ARChive, View files in ARC,          eXtract files, and Print ARC'd files to screen.  The ARC utilities also support password encryption and can function with the screen off to increase speed.  Also, all files are sorted in alphabetical order when added to the ARChive.  
- A new MENU program very similar to the MS-DOS XTREE.EXE program.  This program allows multi-file operations and displays the entire          directory tree, so files anywhere on a disk can be accessed easily.  
- Command compatible with MS-DOS.  Directory commands have several aliases.  CWD from disk based SpartaDOS can also be accessed          as CHDIR, or CD from SDX.  
- Drives can be referred to by letter or number.  
- Drives can be remapped.  D1: can be SWAPped with D2:, etc. and from         that point on, any referrences to D1: will be sent to D2: and vice       versa.  
  
SDX can be configured to take advantage of different hardware.  A file placed on D1: called CONFIG.SYS is used for this, or the default configuration can be used.  SDX can be configured to use OSRAM, or an extended bank of memory for its drivers.  With the right setup, MEMLO can be pushed to below memory location $1000!  
  
SDX uses a series of drivers to control most disk functions.  SPARTA.SYS is the main driver and must be installed.  'DEVICE SPARTA' is used in the CONFIG.SYS file to do this.  The number of sector buffers and file buffers can be control by passing parameters to this driver.  Another driver is <Aop>TARIDOS.SYS used to read Atari DOS 2.x disks.  Not installing this driver saves memory, but then Atari DOS disks cannot be read.  The SDX cart also contains a RAMDisk driver which can be used to install up to 3 RAMDisks of any size.  An INDUS.SYS driver is used to program the INDUS GT to operate at high speed.  There are also two clock drivers, used depending on whether  
or not you have an R-Time 8 cartridge.  
  
A major change with the X cart is the way devices are addressed.  Since ICD wanted drives to be addressed by letter or number, conflicts would have occured with existing devices.  Also, ICD wanted SDX to be more similar to MS-DOS, so those conventions were adopted.  E: has become CON:, P: has become PRN:, and D1: D2: and D3: are A: B: and C:.  Switching between an IBM machine and SpartaDOS X is much easier with these changes.  
  
Another feature of SDX is its I/O redirection.  With this, you can send the output of a program to another device.  Ex: {{DIR >>PRN:}} would do a directory, but the results would be sent to the printer.  Also, you can use a file to "feed" a program with input redirection.  Ex: {{BASIC &lt;&lt;file.ext}} would call up internal BASIC and send it file.ext as if the contents of  
that file were being typed into the machine.  This would be used in place of batch files because you can no longer send input to BASIC from a batch file.  
  
SDX recognizes two new file attributes in addition to protected, hidden and archive.  Hidden files do not appear in the directory, and archive is used to mark files for backup.  This is normally used with a hard disk backup program.  When a file is updated, the archive bit is cleared, telling a program like Flashback that the file needs to be backed up.  All of these are set with the ATR or ATTRIB commands (same thing).  You can also scan directories for files with certain attributes.  
  
Two new commands, PEEK and POKE make many operations easier.  Instead of going to BASIC to execute these commands, they can be sent to the command line.  PEEK will also display the value of the memory word stored at that location and the one following in hex and decimal.  
  
Parameters can now be passed to batch files.  In the batch file itself, these are referred to as %1 through %9.  With this, you can create general purpose batch files to automate tasks.  
  
Internally, SDX is very different from earlier versions of SpartaDOS. All of the files on the cartridge are relocatable and can be held in memory. COMMAND.COM, the command processor is one of these files.  It is non-resident in nature and is unLOADed from memory when binary files are run.  This saves about 4K of memory.  It is reLOADed when the program is exited to DOS.  Disk based programs written in relocatable format could be loaded at MEMLO, and held, eliminating the need to reload from disk each time.  Unfortunately, information on how to write these modules is almost non-existant, so for now, only the programs on the cartridge can be held.  
  
Some of the new commands and changes with SDX not mentioned above:  
- CHTD/CHVOL - now built in  
- COPY - now checks to see that there are two files specified.  Files could be lost with disk based SpartaDOS by accidentally not          specifying a second filename  
- DIR - /p directive pages output, /c directive gives file count.  
- DUMP - Hex dump of file  
- FIND - search all drives for filename  
- MEM - displays banks available, extended memory  
- PATH - Set search path  
- PROMPT - set system prompt with meta-strings  
- RS232 - now built in  
- SET - display/set environment variables  
- UNERASE - restore file(s)  
- X - load file/disable cartridge (for long binary files)  
  
This is an incomplete listing of the features of SpartaDOS X.  There are many others and new uses for the functions appear constantly.  While  
learning to use SDX will take some time, it is well worth it in the end.  
  
SDX is available direct from ICD.  The ICD BBS contains a listing of ICD products available direct at prices much lower than through a store  
or even mail-order.  Check for the latest price.  ICD BBS: 815-968-2229.  
  
Doug Wokoun  
  
  
