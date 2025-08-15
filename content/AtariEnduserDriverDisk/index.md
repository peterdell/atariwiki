---
title: AtariEnduserDriverDisk
---
# Atari USB Enduser Driver Disk  
  
  
A collection of USB Drivers for Users  
  
## What is on the disk:  
  
|| Filename || Comment ||  
| DOS.SYS | Atari Dos 2.5 FMS |  
| DUP.SYS | Atari Dos 2.5 DUP |  
| BIBOASS.COM | Bibo Assembler |  
| USBKEY.SRC | USB Simple Keyboard Driver Source |  
| USBKEY.COM | USB Simple Keyboard Driver  |  
| USBWHEEL.SRC | USB Wheel Driver (Thrustmaster) Source |  
| USBWHEEL.COM | USB Wheel Driver (Thrustmaster) |  
| USBTEST.COM | USB Human Interface Devices (HID) Test Program |  
| USBJOYPD.SRC | USB digital Joypad Driver Source |  
| USBJOYPD.COM | USB digital Joypad Driver |  
| USBJOYST.SRC | USB analog Joystick Driver Source |  
| USBJOYST.COM | USB analog Joystick Driver |  
| BOULDER.COM | Boulder Dash 1 for USB digital Joypad |  
  
## Standard Device Descriptor (Output of USBTEST.COM)  
  
For more detailed information on USB Device Descriptors pleas use the USB 1.1 Specification Documents at [www.usb.org](http://www.usb.org/developers/docs/).  
  
  
|| Offset || Field  || Size  || Value  || Description  ||  
|  0  | bLength |  1  | Number  | Size of this descriptor in bytes |  
|  1  | bDescriptorType |  1  | Constant | DEVICE Descriptor Type  |  
|  2  | bcdUSB |  2  | BCD USB Specification Release Number in Binary-Coded Decimal (i.e., 2.10 is 210H). | This field identifies the release of the USB Specification with which the device and its descriptors are compliant. |  
|  4  | bDeviceClass |  1  | Class  | Class code (assigned by the USB). If this field is reset to zero, each interface within a configuration specifies its own class information and the various interfaces operate independently. If this field is set to a value between 1 and FEH, the device supports different class specifications on different interfaces and the interfaces may not operate independently. This value identifies the class definition used for the aggregate interfaces. (For example, a CD-ROM device with audio and digital data interfaces that require transport control to eject CDs or start them spinning.) If this field is set to FFH, the device class is vendor-specific. |  
|  5   |  bDeviceSubClass |  1  | SubClass  | Subclass code (assigned by the USB). These codes are qualified by the value of the bDeviceClass field. If the bDeviceClass field is reset to zero, this field must also be reset to zero. If the bDeviceClass field is not set to FFH, all values are reserved for assignment by the USB. |  
|  6   | bDeviceProtocol |  1  | Protocol  | Protocol code (assigned by the USB). These codes are qualified by the value of the bDeviceClass and the bDeviceSubClass fields. If a device supports class-specific protocols on a device basis as opposed to an interface basis, this code identifies the protocols that the device uses as defined by the specification of the device class. If this field is reset to zero, the device does not use class-specific protocols on a device basis. However, it may use classspecific protocols on an interface basis. If this field is set to FFH, the device uses a vendor-specific protocol on a device basis.  |  
|  7   | bMaxPacketSize0 |  1  | Number | Maximum packet size for endpoint zero (only 8, 16, 32, or 64 are valid) |  
|  8   | idVendor |  2   | ID | Vendor ID (assigned by the USB)  |  
|  10  | idProduct |  2   | ID | Product ID (assigned by the manufacturer) |  
|  12  | bcdDevice |  2   | BCD  | Device release number in binary-coded decimal  |  
|  14  | iManufacturer |  1  | Index  | Index of string descriptor describing manufacturer |  
|  15  | iProduct |  1   | Index | Index of string descriptor describing product  |  
|  16  | iSerialNumber |  1  | Index  | Index of string descriptor describing the device s serial number |  
|  17  | bNumConfigurations |  1  | Number | Number of possible configurations |  
  
