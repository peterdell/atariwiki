||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS||DEFAULT VALUE  
|read/write |512,513|$0200,$0201|VDSLST|Vector to Display List Interrupt routine|both|59315/$E7B3 (a RTI instruction)  
  
Attention:  
- All 6502 registers have to be saved before and restored after the interrupt (before the RTI instruction).  
- an example to save registers and variables in the language "Action!" [Interrupts_in_ACTION](../Interrupts_in_ACTION/index.md)  
- The interrupt routine must end with an RTI (return from interrupt).  
  
## Example for saving and restoring the processor registers  
  
```
     ;we need to push to stack, first A, then X, then Y
 PHA ;push ACCU to Stack
 TXA ;transfer X to ACCU
 PHA ;push ACCU (now X) to Stack
 TYA ;transfer Y to ACCU
 PHA ;push ACCU (now Y) to Stack
     ;
     ;... routine goes in here ...
     ;
     ;now we need to pull from stack first Y, then X, then A
 PLA ;pull Y from STACK to ACCU
 TAY ;transfer ACCU to Y
 PLA ;pull X from STACK to ACCU
 TAX ;transfer ACCU to X
 PLA ;pull ACCU from STACK
 RTI ;end interrupt routine with ReTurn from Interrupt
```
  
## Example for setting your interrupt routine  
- Set bit 7 in the [display list](../display_list_instruction_table/index.md) line you want the interrupt to occur  
- clear bit 7 of [NMIEN](../NMIEN/index.md) to disable the interrupt  
- set [VDSLST](../VDSLST/index.md) to your routine  
- set bit 7 of [NMIEN](../NMIEN/index.md) to enable the interrupt  
  
  
---
  
see also: [Display List Topics](../Displaylist_topics/index.md), [NMIEN](../NMIEN/index.md), [Display List Instruction table](../display_list_instruction_table/index.md)  
