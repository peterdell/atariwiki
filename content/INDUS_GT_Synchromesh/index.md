# PUT SYNCHROMESH IN HIGH GEAR  
  
by Richard Q. Fox  
  
Copyright 1985 Richard Q. Fox  
  
(Reproduction in newsletters permitted, provided the above header  
is maintained.)  
  
The INDUS GT disk drive for the Atari is capable of reading disk  
data at 2 to 4 times the speed of other disk drives. However, the  
software supplied withit takes so long to load in, that any  
advantage is lost. This article describes a procedure for making  
a boot-load Synchromesh disk for the INDUS which loads in just a  
few seconds. With this disk, Synchromesh is more practical. The  
Synchromesh software is supplied as part of DOS XL 2.35I. In  
order to engage Synchromesh, you must boot load the DOS XL 2.35I  
disk at power up time.  
  
This load takes about 50 seconds, enough time to raid the  
refrigerator and still be back before the beeps and chirps have  
stopped. Once loaded, Synchromesh reads disk files very quickly.  
For example, a 204 sector file reads in 17 seconds. By contrast,  
DOS 2.0 loads in 8 seconds. However, that same 204 sector file  
requires 56 seconds. Now it might seem as if DOS 2.0 is  
incredibly slow, but if you compare the total boot plus loadtimes  
of both approaches, you'll find them about the same...they're  
both slow!  
  
The ideal situation, of course, would be to speed up the boot  
time of Synchromesh so that the boot plus load time is greatly  
reduced compared to DOS 2.0. The steps about to be described  
reduce the Synchromesh boot time from 50 to 19 seconds.  
  
Here are the tools you'll need to create your speedy Synchromesh  
disk:  
  
1. Two blank disks  
1. The DOS XL 2.35I System Master Diskette supplied with Synchromesh  
1. A utility capable of modifying single bytes on a disk sector. Examples are DISKSCAN, OMNIMON, and DISKEY.  
1. To speed up the boot process a little more, an optional step requires the use of the Archiver/Editor/Chip or Happy Enhancement and a sector copier utility.  
  
Step 1 is to boot the DOS XL 2.35I diskette described in item 2.  
This is the 50 second refrigerator break boot. So go enjoy an  
apple while you wait. Next, type I while the DOS XL disk is still  
in the drive. This is the "Initialize Disk" command. Now insert  
the first blank disk. Type the number "1" to "Format Disk Only".  
When formatting is complete, type number "4" to "Reformat Boot  
Tracks Only". This is followed by "3", "Write DOS.SYS Only". The  
last step in this sequence is "5", "Return to DOS XL".  
  
While this disk is still in the drive, type "X" for the "Xtended  
Command". Type in the following when prompted for Command:  
  
```
"TYPE E: STARTUP.EXC". 
```
  
This allows you to create the startup file. When you hit return,  
the screen goes blank. Type in the following:  
```
NOSCREEN 
GTSYNC ON 
DO CARTRIDGE;RUN "D:MENU.BAS" 
SCREEN 
END 
```
control and lower case 3  
  
This takes you back to the main menu. Swap back to the DOS XL  
2.35I diskette. You now need to copy two files from this disk.  
Press "C" for "Copy Files". The "From File" is GTSYNC.COM. The  
"To File" is also GTSYNC.COM. Answer the "Single Drive" question  
with a "Yes". Follow the screen directions to copy the file from  
DOS XL 2.35I to the disk on which you wrote the "STARTUP.EXC"  
file. Repeat this same procedure to copy "DO.COM" to your disk.  
  
The next step reduces the number of drives checked by  
Synchromesh. At this point, boot in your utility for modifying  
disk sectors. Use the utility to find the starting sector of the  
GTSYNC.COM file. The starting sector is probably 003A hex (58  
decimal). Modify byte 3A of the second sector of GTSYNC.COM to be  
one more than the number of drives you want to check. For  
instance, if you want to check for two drives, plug in 03 at byte  
3A. The location you just changed should have read 09 (one more  
thanthe 8 drives Synchromesh checks) prior to the change. If the  
procedures to this point were followed exactly, the second sector  
will probably be 003B hex (59 decimal). The value 09 is in sector  
003B at byte 3A. Now write your modification to the disk using  
the utility. At this point, Synchromesh will boot in 27 seconds.  
  
The next step is optional. Using it will cut another 8 seconds  
off the boot time. This step involves reformatting tracks 0,1,2,3  
and 4, but you will need the Archiver/Editor/Chip or the Happy  
Enhancement to do the job. The first step is to use DOS XL 2.35I  
to format the second disk (which is now blank). Use the I  
function to Initialize the disk with DOS XL 2.35I still in the  
drive (same as before). On the menu, select Option 1 (Format Disk  
Only). Swap disks and insert the blank disk. Be very careful not  
to wipe out all your work to this point by inserting the wrong  
disk! You might want to label the first disk "Super Synchromesh"  
and the second disk "Scratch" or "Temp". Finish formatting the  
"Temp" disk using Option 5. You do not have to use Options 3 and  
4 as you did in creating "Super Synchromesh". Boot in your sector  
copier utility. Set it to copy tracks 0,1,2,3 and 4 from  
the"Super Synchromesh" disk to the "Temp" disk. Boot in your  
Archiver or Happysoftware and set it up to process only tracks  
0,1,2,3 and 4. Insert the"Super Synchromesh" disk in the drive.  
Go to the formatter feature and set the formatter for the  
following sequence:  
```
11 0F 0D 0B 09 07 03 01 12 10 0E 0C 0A 08 06 04 02 
```
Format tracks 0 through 4.  
  
Reboot your sector copier utility. Copy tracks 0 through 4 from  
the "Temp" disk to the "Super Synchromesh" disk. Your "Super  
Synchromesh" disk will now boot in 19 seconds.  
  
The STARTUP.EXC file that you created transfers control to BASIC  
and runs a program called "D:MENU.BAS". You may change this file  
to meet your needs.  
  
To use your new "Super Synchromesh" disk, your best bet would be  
to writeprotect this copy and use Archiver or Happy to make  
future copies. Adding your software to these copies gives you  
fast "boot and go" disks.  
