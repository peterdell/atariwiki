---
title: USB Cartridge
---
### Project USB Cartridge  
  
- Project Name  : USB Cartridge with two USB Slots  
- Project Start : Summer 2002  
- Project Member: Marc Brings, Thomas Grasel, Harry Reminder, Florian Dingler, Guus Assmann, Carsten Strotmann  
- Project Specs : see Information below  
  
- Project Pictures:  
- [USB Programming Session 27th May 2006](../ProjUSBConvSixPic/index.md)  
- [USB Programming Session 9th-12th December 2005](../ProjUSBConvFivePic/index.md)  
- [USB Programming Session 19th-21st August 2005](../ProjUSBConvFourPic/index.md)  
- [Vintage Computer Festival Europe, Munich, April/May 2005](../ProjUSBVCFePic/index.md)  
- [USB Programming Session 14th-16th January 2005](../ProjUSBConvThreePic/index.md)  
- [USB Programming Session 16th-18th July 2004](../ProjUSBConvTwoPic/index.md)  
- [Pictures Cartridge](../ProjUSBCartPic/index.md)  
- [USB Programming Session 9th August 2003](../ProjUSBConvOnePic/index.md)  
- [USB Host-Slave Cart](../ProjUSBCartTwoPic/index.md)  
  
## Software  
  
- [Base HID Driver](../BaseHIDDriver/index.md)  
- [USB Device Driver Development Kit Disk](https://sourceforge.net/project/showfiles.php?group_id=111428&package_id=120826)  
- [Atari USB Enduser Driver Disk](../AtariEnduserDriverDisk/index.md)  
- [Keyboard Driver](../Atari_USB_Keyboard_Driver/index.md)  
- [Digital Joypad Driver](../Digital_Joypad_Driver/index.md)  
- [Logitech Rumblepad 2 USB Driver](../JoypadRumblePadTwoUsb/index.md)  
- [Analog Joystick Driver](../AtariAnalogJoystickDriver/index.md)  
- [Thrustmaster Steering Wheel Driver](../USB_Steering_Wheel_Driver/index.md) ( [Pictures of Pole-Position USB Version](../ProjUSBCartAtariWheelPolePosPics/index.md) )  
- [Logitech GP Steering Wheel Driver](../Logitech_Formula_GP_USB_Wheel_Driver/index.md)  
- [Logitech VP Steering Wheel Driver](../Logitech_Formula_VF_USB_Wheel_Driver/index.md)  
- [Speedlink_Competition_Pro_USB](../Speedlink_Competition_Pro_USB/index.md)  
- [Device compatibility matrix](../DeviceMatrix/index.md)  
  
## Documentation  
  
- [How to write a new USB HID Driver](../How_to_write_a_USB_Driver/index.md)  
- [How to write patch a Game for USB usage](../How_to_patch_a_game_for_USB_Usage/index.md)  
  
## Status  
  
CarstenStrotmann - 2 Dec 2004  
  
The Carts are ready for shipping from US to Europe...  
  
![](attachments/USB_Cart_ready.jpg)  
  
CarstenStrotmann - 29 Nov 2004  
  
Steve Tucker --> [AtariMax Website](http://www.atarimax.com) is currently assembling USB Carts for the European and US market.  
  
![](attachments/USBCart_raw.jpg)  
  
  
CarstenStrotmann - 18 Jul 2004  
  
Another coding session with Harry Reminder, Thomas Grasel, it seems that we always meet at the hottest days in summer.  
We have now acces to HID (Human Interface Devices) for the Host Mode of the Cypress SL811 ready, so we can access USB Keyboard, USB Joystick and USB Mouse, as well as other USB HID Devices.  
  
We will have generic 6502 Sourcecode and FORTH Sourcecode ready in the next days and have real Atari XL/XL driver for Keyboard, Mouse and Joystick on the Unconventional Party in September in Lengenfeld.  
  
See the [Pictures](../ProjUSBConvTwoPic/index.md) of the day.  
  
  
CarstenStrotmann - 6 Jan 2004  
  
Harry Reminder and Thomas Grasel made a new USB Cartridge Hardware, now with a Cypres SL811HS chip. This USB chip is Host AND Slave, so with this we can attach the Atari to a PC/Mac (Slave-Mode) and we can attach USB-Devices (Mouse, Graphic-Tablet, Memory-Stick ...) to the Atari (Host-Mode). See new project [pictures](../ProjUSBCartTwoPic/index.md).  
  
  
CarstenStrotmann - 10 Aug 2003  
  
Harry Reminder, Thomas Grasel and I used the hottest Day of the year (so far, 40 C in Frankfurt) for a USB Coding Session. The Joystick Firmware is almost complete, there are some problems with the Uni-Code Strings (this might be the 1st ATARI 8-Bit PGM with Uni-Code :) ) and with the USB Reports.  
  
See the [Pictures](../ProjUSBConvOnePic/index.md) of the day.  
  
CarstenStrotmann - 9 Jul 2003  
  
The ATARI and the PC (running Debian GNU/Linux) are talking to each other via USB. This days we're completing the basic USB Stack. There will be a new improved version of the device driver development kit released in the next weeks. We're also taking new pictures on how the cartridge is looking like today, and some screenshots of the Linux-Side. We'Re still operating the USB-Cart in slave mode.  
  
  
CarstenStrotmann - 14 Apr 2003  
  
Today we made "first contact" with the USB Controller, we are now able to talk with the USB Controller from the ATARI. Now we're starting the driver development.  
  
The blueprint version 1.1 need two changes:  
  
- the USB Controller Reset-Pin must be connected to a reset-circuit  
- the mode-pins of the USB-Controller must be connected to ground  
  
Then the first USB contoller is available in $D548 (Data-Register) and $D549 (Address-Register). The second Controller is available on $D540 (Data) and $D541 (Address).  
  
To initialize the clock frequency for the second controller, write $01 into USB-Register $01. This generates an output-clock of 24Mhz for the second controller (48mhz / 1+1, see USB-Controller Datasheet).  
  
  
Credits:  
  
- Marc Brinks has completed the cartridge  
- Thomas Grasel and Harry Reminder found the last bugs and made the modifications to the cart  
  
![](http://sourceforge.net/sflogo.php?group_id=111428&amp;type=5)  
  
  
  
  
  
  
  
  
  
