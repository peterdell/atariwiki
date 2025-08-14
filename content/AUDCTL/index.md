||Read/Write||ADR||HEXADR||NAME||Description||OS  
|Read|53768|$D208|ALLPOT|Audio control|all  
|Write|53768|$D208|AUDCTL|Pot Port State|all  
  
# AUDCTL (Write)  
AUDCTL is the option byte which affects all sound channels. This bit assignment is:  
||Bit||Description  
|7|	0=17 bit poly counter 1=9 bit polynomial noise  
|6|	0=clock channel 1 with 64kHz1=Clock channel one with 1.79 MHz (NTSC) or 1.77MHz (PAL)  
|5|	0=clock channel 3 with 64kHz1=Clock channel three with 1.79 MHz (NTSC) or 1.77MHz (PAL)  
|4|	0=clock channel 2 with 64kHz1=Join channels two and one (16 bit, with 2/4=MSB, 1/2=LSB)  
|3|	0=clock channel 4 with 64kHz1=Join channels four and three (16 bit, with 2/4=MSB, 1/2=LSB)  
|2|	1=Insert high pass filter into channel one, clocked by channel two  
|1|	1=Insert high pass filter into channel three, clocked by channel four  
|0|	0=main clock base 64 KHz1=16 KHz main clock base  
  
# ALLPOT (Read)  
Shows if the readings of the pots are (already) valid.  
||Bit||Paddle||Shadow||Register  
|0|Paddle 0| [PADDL0](../PADDL0/index.md)| [POT0](../POT0/index.md)  
|1|Paddle 1| [PADDL1](../PADDL1/index.md)| [POT1](../POT1/index.md)  
|2|Paddle 2| [PADDL2](../PADDL2/index.md)| [POT2](../POT2/index.md)  
|3|Paddle 3| [PADDL3](../PADDL3/index.md)| [POT3](../POT3/index.md)  
|4|Paddle 4| [PADDL4](../PADDL4/index.md)| [POT4](../POT4/index.md)  
|5|Paddle 5| [PADDL5](../PADDL5/index.md)| [POT5](../POT5/index.md)  
|6|Paddle 6| [PADDL6](../PADDL6/index.md)| [POT6](../POT6/index.md)  
|7|Paddle 7| [PADDL7](../PADDL7/index.md)| [POT7](../POT7/index.md)  
If a bit equals zero (0), then the register value for that pot (e.g. Bit 0 = [POT0](../POT0/index.md)) is valid; if the Bit is one (1), then the value is not (yet) valid, because the reading/scan is not finished yet or there is no paddle connected.  
  
---
see also: [Controller topics](../Controller_topics/index.md), [POTGO](../POTGO/index.md), [ALLPOT](../ALLPOT/index.md), [SKCTL](../SKCTL/index.md)  
  
previous: [AUDC4](../AUDC4/index.md),[POT7](../POT7/index.md)  
  
next: [STIMER](../KBCODE/index.md),[KBCODE](../KBCODE/index.md)  
