||ADR||HEXADR||NAME||Description||OS  
|58460|$E45C|SETVBV|Set system timers and interrupt vectors|both  
  
Sets an interrupt vector or system timer vector.  
  
## Usage:  
  
Assembler  
```
LDX MSB
LDY LSB
LDA (value see table below)
JSR $E45C
```
Action!  
```
PROC SETVBV=*$E45C(BYTE VECTOR,MSB,LSB)
RETURN
```
  
  
||Register||Value  
|X|MSB  
|Y|LSB  
|A|vector to be changed, see below  
  
||Value||Vector  
|0|[VIMIRQ](../VIMIRQ/index.md)  
|1|[TIMCOUNT1](../TIMCOUNT1/index.md)  
|2|[TIMCOUNT2](../TIMCOUNT2/index.md)  
|3|[TIMCOUNT3](../TIMCOUNT3/index.md)  
|4|[TIMCOUNT4](../TIMCOUNT4/index.md)  
|5|[TIMCOUNT5](../TIMCOUNT5/index.md)  
|6|[VVBLKI](../VVBLKI/index.md)  
|7|[VVBLKD](../VVBLKD/index.md)  
  
  
---
see also: [VBI_Vertical_Blank_Interrupt](../VBI_Vertical_Blank_Interrupt/index.md)  
