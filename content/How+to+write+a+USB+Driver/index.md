---
title: How+to+write+a+USB+Driver
---
# How to write a new USB HID Driver  
  
## The USB Device  
  
I bought a new Logitech Rumblepad 2 USB today. Because there is currently no driver for the Atari for this device, I use this as a case study how to write an USB Driver for this device.  
  
![](attachments/LogitechRumblepad2USB.jpg)  
  
  
The Logitech Rumblepad 2 USB has one digital Joypad Controller, two analog Joystick Controller (Right Handle and Left Handle), 10 normal Buttons, a Mode Button amd a Mode LED, and a Button to change the Force Feedback Vibration Mode (long or short).  
  
## Step 1: Examine the USB Packets  
  
First I start the USBTEST.COM Utility on the USB End User Driver Disk. The USB Controller can access the Logitech Pad and prints out the Device Descriptor and the String Descriptors. Ok, we can access the device. Fine. Next I start the USB HID Trace in USBTEST. The USB HID Trace will print out all the USB Packets send from the USB Device to the Controller (the USB Cart). We will see something like this if we use the Device:  
  
```
80 80 80 FF 08 00 44 FD                        |
80 80 80 E0 08 00 44 FD                        |  Left handle from down to default
80 80 80 95 18 00 44 FD  <- Button 1 pressed   |
80 80 80 7F 08 00 44 FD                        |
```
  
Here I moved the right handle from down to the default (middle) position and I pressed Button 1 once.  
  
After playing around with the Device for a while (10 minutes), I know all(most) all packets available:  
  
- Byte 1: left handle horizontal movement ($00 = left, $80 = middle, $FF= right)  
- Byte 2: left handle vertical movement ($00 = up, $80 = middle, $FF= down)  
- Byte 3: right handle horizontal movement ($00 = left, $80 = middle, $FF= right)  
- Byte 4: right handle vertical movement ($00 = up, $80 = middle, $FF= down)  
- Byte 5: Bit 0-3 digital Joypad (see below)  
- Byte 5: Bit 4 - Button 1, Bit 5 - Button 2, Bit 6 - Button 3, Bit 7 - Button 8  
- Byte 6: Bit 0-5 - Button 5-10  
- Byte 7: Bit 2 - Vibration Switch, Bit 3 - Mode Switch and LED  
- Byte 8: unknown  
  
The digital Joypad has a unique value for each direction_  
```
.
          up
          0
        7 | 1
left  6---8---2 right
        5 | 3
          4
         down
```
  
## Step 2: The Basic Driver  
  
I start a new, fresh formatted Disk for each new driver. I install a DOS and [Bibo_Assembler](../Bibo_Assembler/index.md) on the disk, along with the Base HID Driver and the HID Device Template Sourcecode.  
  
Each HID Driver Sourcecode consists of two parts:  
  
- the basic part  
- the device dependent part  
  
The [Base HID Driver Sourcecode](../BaseHIDDriver/index.md).  
  
The Basic Part handles the generic tasks identical for all USB HID Devices:  
  
- print copyright message  
- Reset and Initialization of the USB Controller  
- Detect slow speed device  
- send USB Address 1 to device and setup EndPoint 0  
- select Configuration 1 in the device  
- initialize the VBI  
  
We change the basic driver to include our device dependent part.  
  
```
------------------------------
DEVICE   .IN "D:device.SRC"
------------------------------
```
  
## Step 3: The Device Driver  
  
The Device dependet part will be included into the basic part. The Device dependent part has two main functions:  
  
- print out device dependet messages  
- copy the USB HID Register values in Atari Shadow Register  
- simulate legacy Atari Controller (Joystick, Keyboard, Paddle)  
  
We only need to change the Device dependent part of the driver. First we must device where to store the shadow registers for the native USB Device functions. These Registers will be copied from the USB Controller Memory into the Atari Memory. The USB HID Registers start at the USB Controller Memory Location $10. I've choosen to store the USB Register Values into the Memory Locations for Paddles ($270-$277).  
  
|| USB Register || Byte of HID Packet || Function || Atari Memory Shadow || original Label || new USB label ||  
|  $10           |  1                 | left handle horiz movement  | $270 (624)  | PADDL0 | RPADLHH     |  
|  $11           |  2                 | left handle vertic movement | $271 (625)  | PADDL1 | RPADLHV     |  
|  $12           |  3                 | right handle horiz movement  | $272 (626)  | PADDL2 | RPADRHH     |  
|  $13           |  4                 | right handle vertic movement | $273 (627)  | PADDL3 | RPADRHV     |  
|  $14           |  5 Bit 0-4         | digital Joypad | $274 (628)  | PADDL4 | RPADDJY     |  
|  $14           |  5 Bit 5-7         | Button 1-4 | $275 (629)  | PADDL5 | RPADBUT1  |  
|  $15           |  6                 | Button 5-10 | $276 (630)  | PADDL6 | RPADBUT2  |  
|  $16           |  7                 | Mode Button Status | $277 (631)  | PADDL7 | RPADMODE  |  
  
Accessing the USB Controller Memory is wasy. Load the X-Index Register with the USB Memory Location to access (0-255) and jump to subroutine REGFETCH. REGFETCH will return with the value of that memory location in the Accu (A) Register. This value is then stored into the Atari Shadow register. Because we are running in an VBI, we will overwrite all values the Atari OS has written into this registers.  
  
```
POLLDEVICE
LDA #03
JSR PROCESS         ; Poll for next USB HID Packet

LDX #$10            ; load USB Register $10
JSR REGFETCH
STA RPADLHH         ; store in shadow register

LDX #$11
JSR REGFETCH
STA RPADLHH

LDX #$12
JSR REGFETCH
STA RPADRHH

LDX #$13
JSR REGFETCH
STA RPADRHV

LDX #$14
JSR REGFETCH
PHA                ; save value on stack
AND #$0F           ; clear top nibble Bit 4-7
STA RPADDJY        ; store in shadow register
PLA                ; restore original value from stack
LSR                ; shift top nibble into lower nibble
LSR                ; Bit 4-7 -> 0-3
LSR
LSR
STA RPADBUT1       ; store in shadow register

LDX #$15
JSR REGFETCH
STA RPADBUT2

LDX #$16
JSR REGFETCH
STA RPADMODE

RTS
```
  
Code to print the Device dependet messages. These Subroutines will be called by the Base driver upon initialization:  
  
```
PRINTDEVICE
JSR PRINT
JSR PRINT
.AS "Logitech RumblePad 2 USB Driver"
.HX 40
RTS

PRINTVERSION
JSR PRINT
.AS "Version 1.0"
.HX 40
RTS

PRINTCOPY
JSR PRINT
.AS "(c) 20041213 C. Strotmann"
.HX 40
RTS
```
  
The Subroutine USB2ATA is emulating legacy Atari devices (Atari Joystick) from the USB Joypad values. In this driver, all USB Device Buttons fire the Trigger of the first Atari Joystick. The left USB Handle goes to digital Atari Joystick 1 (STICK(1) in Basic) and the right USB Handle goes to digital Joystick 2 (STICK(2) in Basic).  
  
```
; THRESHOLD ANALOG->DIGITAL
THLEFT   .HX 60
THRIGHT  .HX A0
THUP     .HX 60
THDOWN   .HX A0

USB2ATA
LDA #$0F         ; setup default
STA STICK0       ; Atari Stick and Trigger
STS STICK1       ; values $0F = 15 = no move
LDA #1
STA STRIG0
STA STRIG1
;
LDA RPADBUT1     ; any Button pressed?
ORA RPADBUT2
BEQ GETSTICK     ; no!
LDA #0           ; yes, store Trigger pressed value
STA STRIG0
;
GETSTICK1         ; process Stick 1 (Left Handle)
LDA STICK0
LDX RPADLHH
CPX THLEFT
BCC .1           ; LEFT
CPX THRIGHT
BCS .2           ; RIGHT
BCC .10
EOR #$04         ; LEFT
BPL .3
.2
EOR #$08         ; RIGHT
.3
STA STICK0
.10
LDX RPADLHV
CPX THUP
BCC .11          ; UP
CPX THDOWN
BCS .12          ; DOWN
BCC .20
.11
EOR #$01         ; UP
BNE .13
.12
EOR #$02         ; DOWN
.13
STA STICK0
.20

GETSTICK2         ; process Stick 2 (Right Handle)
LDA STICK1
LDX RPADRHH
CPX THLEFT
BCC .1           ; LEFT
CPX THRIGHT
BCS .2           ; RIGHT
BCC .10
EOR #$04         ; LEFT
BPL .3
.2
EOR #$08         ; RIGHT
.3
STA STICK1
.10
LDX RPADRHV
CPX THUP
BCC .11          ; UP
CPX THDOWN
BCS .12          ; DOWN
BCC .20
.11
EOR #$01         ; UP
BNE .13
.12
EOR #$02         ; DOWN
.13
STA STICK1
.20

RTS
```
  
The [Complete Device dependent part](../JoypadRumblePadTwoUsb/index.md) of the Source Code.  
  
## Step 4: Compile and Test  
  
Now we compile the new Driver and Test the driver with a small basic Program.  
  
- we load the Base Driver Part into [BiboAssembler](../BiboAssembler/index.md) and compile with ASM to a binary driver (COM File).  
- we load the driver from DOS  
- we enter Basic and test the driver with this small Basic Program  
  
```
100 REM Small USB Testprogram for Logitech Rumble Pad 2 USB Driver
110 REM -----------------------------------------------------------
120 IF STICK(0) < 15 THEN PRINT "Moved Left Handle, Joystick 1:", STICK(0)
130 IF STICK(1) < 15 THEN PRINT "Moved Right Handle, Joystick 2:", STICK(1)
140 IF STRIG(0) < 1 THEN PRINT "Pressed Button:", STRIG(0)
150 GOTO 120

```
