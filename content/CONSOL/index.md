||R/W||ADR||HEXADR||NAME||DESCRIPTION||DEFAULT||OS  
|read/write |53279 |$D01F|CONSOL|Console keys and internal speaker (400/800)|7|all  
  
## Read  
Used to look up if any of the 3 console keys (START, SELECT, OPTION) has been pressed (RESET is not a console key, neither is [HELP](../HELPFG/index.md))  
  
```
START    Bit 0    PEEK(53279)=6
SELECT   Bit 1    PEEK(53279)=5
OPTION   Bit 2    PEEK(53279)=3
```
  
  
## Write  
The built in speaker clicks (only on 400/800 computers)  
  
Defaultwert: 7 ($7)  
  
In diesem Register kann der Status der drei folgenden Zusatztasten (OPTION, SELECT, START) ausgewertet werden. Die den Tasten entsprechenden Bits werden bei Tastendruck gelöscht.  
  
Das Schreiben eines Wertes zwischen Null und Sieben in dieses Register erzeugt einen  
Klick über den Tastaturlautsprecher bzw., über den normalen Tonkanal (XL- und XE-Geräte).  
---
see also: [Keyboard topics](../Keyboard_topics/index.md), [Sound_Topics](../Sound_Topics/index.md)  
  
previous: [HITCLR](../HITCLR/index.md)  
  
next: [AUDF1](../AUDF1/index.md),[POT0](../POT0/index.md) of POKEY  
