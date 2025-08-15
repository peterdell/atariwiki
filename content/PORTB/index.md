---
title: PORTB
---
# For 400, 800 (OS A)  
||ADR||HEXADR||NAME||Description||shadow||OS  
|54017|$D301|PORTB| | [STICK2](../STICK2/index.md) [STICK3](../STICK3/index.md) [PTRIG4](../PTRIG4/index.md) [PTRIG5](../PTRIG5/index.md) [PTRIG6](../PTRIG6/index.md) [PTRIG7](../PTRIG7/index.md)| 400/800  
  
Read or write data from the control ports (joystick ports), depending on how the data direction is set (default: 0 "read/input"). To set the direction, set Bit 2 of [PBCTL](../PBCTL/index.md) to "0" and define the direction by setting the bits of PORTB (0=read, 1=write) for each input/output line. Then set Bit 2 of [PBCTL](../PBCTL/index.md) to "1" again.  
  
Example:  
```
PACTL=PACTL && %11111011 ;set Bit 2 to 0
PORTA=%11110000          ;set Port 2 to output/write, Port 1 is input/read
PACTL=PACTL %% %00000100 ;set Bit 2 to 1
```
  
||Bit||Function||Description||Joystick direction||Paddletrigger  
|7|PA7|Joystick Port 4 Pin 4|Right|Paddle 8 [PTRIG7](../PTRIG7/index.md)  
|6|PA6|Joystick Port 4 Pin 3|Left|Paddle 7 [PTRIG6](../PTRIG6/index.md)  
|5|PA5|Joystick Port 4 Pin 2|Down|not used  
|4|PA4|Joystick Port 4 Pin 1|Up |not used  
|3|PA3|Joystick Port 3 Pin 4|Right|Paddle 6 [PTRIG5](../PTRIG5/index.md)  
|2|PA2|Joystick Port 3 Pin 3|Left|Paddle 5 [PTRIG4](../PTRIG4/index.md)  
|1|PA1|Joystick Port 3 Pin 2|Down|not used  
|0|PA0|Joystick Port 3 Pin 1|Up|not used  
  
Joystick direction sets Bit=0 when pushed in that direction  
  
Paddletrigger Bit=0 when pressed  
  
# For 600XL, 800XL, 1200XL  
  
||ADR||HEXADR||NAME||Description||OS  
|54017|$D301|PORTB| Memory Management | XL/XE  
  
1200XL  
||Bit||Function||Description  
|7|$5000-$57FF|0=Self test, 1=RAM  
|6|not used|  
|5|not used|  
|4|not used|  
|3|LED2|0=off, 1=on  
|2|LED1|0=off, 1=on  
|1|not used  
|0|$C000-$FFFF|0=RAM, 1=OS-ROM  
  
600XL/800XL  
||Bit||Function||Description  
|7|$5000-$57FF|0=Self test, 1=RAM  
|6|not used|  
|5|not used|  
|4|not used|  
|3|not used|  
|2|not used|  
|1|$A000-$BFFF|0=ATARI BASIC ROM, 1=RAM  
|0|$C000-$FFFF|0=RAM, 1=OS-ROM  
  
# For 130XE  
Bits 2,3,4,5 set the behavior of extended RAM which is always mapped to $4000-$7FFF area.  
||Bit||Function||Description  
|7|$5000-$57FF|0=Self test, 1=RAM  
|6|not used|  
|5|ANTIC|0=ANTIC has access to extended RAM, 1=ANTIC has access to main RAM  
|4|CPU|0=CPU has access to extended RAM, 1=CPU has access to main RAM  
|3|$4000-$7FFF|Bank selection bit  
|2|$4000-$7FFF|Bank selection bit  
|1|$A000-$BFFF|0=ATARI BASIC ROM, 1=RAM  
|0|$C000-$FFFF|0=RAM, 1=OS-ROM  
  
Compatibility mode (only main bank enabled)  
||Bit 5   ||Bit 4   ||Bit 3   ||Bit 2   ||CPU accesses   ||ANTIC accesses  
|VBE     |CPE     |Bank selection|Bank selection| |  
|1       |1       |doesn't matter|doesn't matter|M $4000-$7FFF|   M $4000-$7FFF  
  
CPU extended RAM mode  
||Bit 5   ||Bit 4   ||Bit 3   ||Bit 2   ||CPU accesses   ||ANTIC accesses  
|VBE     |CPE     |Bank selection |Bank selection| |  
|1       |0       |0       |0       |E $0000-$3FFF   |M $4000-$7FFF  
|1       |0       |0       |1       |E $4000-$7FFF   |M $4000-$7FFF  
|1       |0       |1       |0       |E $8000-$BFFF   |M $4000-$7FFF  
|1       |0       |1       |1       |E $C000-$FFFF   |M $4000-$7FFF  
  
Video (ANTIC) extended RAM mode  
||Bit 5   ||Bit 4   ||Bit 3   ||Bit 2   ||CPU accesses  ||ANTIC accesses  
|VBE     |CPE     |Bank selection|Bank selection| |  
|0       |1       |0       |0       |M $4000-$7FFF   |E $0000-$3FFF  
|0       |1       |0       |1       |M $4000-$7FFF   |E $4000-$7FFF  
|0       |1       |1       |0       |M $4000-$7FFF   |E $8000-$BFFF  
|0       |1       |1       |1       |M $4000-$7FFF   |E $C000-$FFFF  
  
General extended RAM Mode  
||Bit 5   ||Bit 4   ||Bit 3   ||Bit 2   ||CPU accesses   ||ANTIC accesses  
|VBE     |CPE     |Bank selection|Bank selection| |  
|0       |0       |0       |0       |E $0000-$3FFF   |E $0000-$3FFF  
|0       |0       |0       |1       |E $4000-$7FFF   |E $4000-$7FFF  
|0       |0       |1       |0       |E $8000-$BFFF   |E $8000-$BFFF  
|0       |0       |1       |1       |E $C000-$FFFF   |E $C000-$FFFF  
  
---
see also: [Controller topics](../Controller_topics/index.md)  
  
previous: [PORTA](../PORTA/index.md)  
  
next: [PACTL](../PACTL/index.md)  
