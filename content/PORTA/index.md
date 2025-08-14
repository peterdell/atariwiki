||ADR||HEXADR||NAME||Description||shadow||OS  
|54016|$D300|PORTA| | [STICK0](../STICK0/index.md) [STICK1](../STICK1/index.md) | all  
  
Read or write data from the control ports (joystick ports), depending on how the data direction is set (default: 0 "read/input"). To set the direction, set Bit 2 of [PACTL](../PACTL/index.md) to "0" and define the direction by setting the bits of PORTA (0=read, 1=write) for each input/output line. Then set Bit 2 of [PACTL](../PACTL/index.md) to "1" again.  
  
Example:  
```
PACTL=PACTL && %11111011 ;set Bit 2 to 0
PORTA=%11110000          ;set Port 2 to output/write, Port 1 is input/read
PACTL=PACTL %% %00000100 ;set Bit 2 to 1
```
  
||Bit||Function||Description||Joystick direction||Paddletrigger  
|7|PA7|Joystick Port 2 Pin 4|Right|Paddle 4 [PTRIG3](../PTRIG3/index.md)  
|6|PA6|Joystick Port 2 Pin 3|Left|Paddle 3 [PTRIG2](../PTRIG2/index.md)  
|5|PA5|Joystick Port 2 Pin 2|Down|not used  
|4|PA4|Joystick Port 2 Pin 1|Up |not used  
|3|PA3|Joystick Port 1 Pin 4|Right|Paddle 2 [PTRIG1](../PTRIG1/index.md)  
|2|PA2|Joystick Port 1 Pin 3|Left|Paddle 1 [PTRIG0](../PTRIG0/index.md)  
|1|PA1|Joystick Port 1 Pin 2|Down|not used  
|0|PA0|Joystick Port 1 Pin 1|Up|not used  
  
Joystick direction Bit=0 when pushed in that direction  
  
Paddletrigger Bit=0 when pressed  
---
see also: [Controller topics](../Controller_topics/index.md)  
  
previous: [SKCTL](../SKCTL/index.md),[SKSTAT](../SKCTL/index.md) of POKEY  
  
next: [PORTB](../PORTB/index.md)  
