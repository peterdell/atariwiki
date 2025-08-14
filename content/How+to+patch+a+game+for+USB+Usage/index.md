# How to patch a Game for USB Usage  
  
All necessary files and tools are on the attached Disk image.  
  
## The Game  
  
For this documentation I used the game "Trailbalzer" . The original Trailblazer Binary is on the attached Disk Image.  
  
## Step 1: Examine the Game Binary  
  
First we need to know where the game will load, so that we know where we can store the patch part.  
  
I used Thorsten Karwoths Power Packer, which I also use as a linker. The Power Packer desplays this information:  
  
```
$6D06-$7BC7
Init: $6D06
$1D00-$5AE1
Start: $E474
```
  
With the help on a resident memory monitor (BiboMon or QMEG) I choose the memory location starting at $9000 to be save, as it seems that the game will not use this memory location.  
  
## Step 2: How it works  
  
The Patch works by replacing the load commands for the Joystick Registers into Subroutine jumps into the USB Driver code. Normally the Joystick values for Joystick 1 will be loaded from Memory Location $0287 (Stick0) or direct from $D300 (PORTA). In most games we will find machine language commands like {{LDA $0278}}. After this command the value of the Joystick Shadow register is in the Accu-CPU-Register. We will change this commands to a call into the USB driver:  
  
- poll the USB Device  
- convert readings into Atari Joystick Values  
- return from Subroutine with Joystick Value in Accu  
  
Sometimes the values will be stored in the X or Y Index registers, but the idea is the same.  
  
## Step 3: Searching the game binary for Joystick code  
  
Now we search the game binary for commands that access the Joystick shadow registers. You will need a Memory Monitor for this. I use BiboMon or QMEG.  
  
We are looking for the byte sequence {{78 02}}, part of commands like {{LDA $0278}} or {{LDX $0278}}.  
  
We look for $0278 (Stick0), $D300 (PORTA) and $284 (Strig0 for Joystick Trigger).  
  
For trailblazer we will find  
  
- $26A9 -- LDA $0278  
- $26BF --  LDX $0278  
- $26A3 -- LDA $0284  
- $26B3 -- LDX $0284  
  
Four memory locations we need to patch.  
  
For the Stick and the Trigger (Strig) we create short routines the will  
  
- save the registers  
- poll the USB device  
- convert readings to Aari Joystick values  
- return Value  
  
```
LDASTICK
STX SAVE1
STY SAVE2
JSR POLLDEVICE
JSR USB2ATA
LDA STICK0
LDX SAVE1
LDY SAVE2
RTS
```
  
And then we patch the memory locations we have found earlier with calls to this subroutines  
  
```
PATCH
; let's patch
.OR $26A9
JSR LDASTICK
;
.OR $26BF
JSR LDXSTICK
;
.OR $26A3
JSR LDASTRIG
;
.OR $26B3
JSR LDXSTRIG
```
  
At the end of the WAITDEVICE Subrutine we remove the VBI registration (we don't need a VBI in a game patch). Instead we call the Game entry point ($E474 for Trail Balzer).  
  
```
WAITDEVICE
(...)
JMP $E474
```
  
Now we assemble our driver (see full sourcecode attached). The driver is 90% identical to the normal USB Driver.  
  
## Step 4: Linking the Game with the Patch Driver  
  
We need to link the new driver with the original binary. The new driver will be appended to the original binary. The binary will only patched in memory, we will not change the game binary on disk. For this we need a linker. I use the Power Packer for this (on the disk).  
  
First I load the original binary "TRAIL.COM". Next I load the patch driver "TRAILUSB.COM". The RUN Vector of "TRAILUSB.COM" will overwrite the RUN Vector of the original binary. Next we can save the new, combined binary (T1.COM).  
  
## Step 5: Testing the game  
  
We load the game and, hey, it works. We can now play Trailblazer with our Logitech USB Joypad. To create a patch-driver for another device (USB Wheel or USB Joystick or even USB Keyboard) we need to replace the POLLDEVICE and the USB2ATA Subroutines in the patch driver with device dependent code.  
  
Have fun!  
  
  
  
  
  
