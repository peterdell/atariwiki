---
title: DLISTL
---
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS||SHADOW REGISTERS  
|read/write |54274,54275|$D402,$D403|DLISTL, DLISTH|Start Address of the Display List|both|[SDLSTL](../SDLSTL/index.md), [SDLSTH](../SDLSTL/index.md)  
  
Attention: the display list can NOT cross a 1K-boundary unless you use a JMP instruction (1/$01) to cross the boundary (see [Display List Instruction table](../display_list_instruction_table/index.md))  
  
---
  
see also: [Display List Topics](../Displaylist_topics/index.md), [SDLSTL](../SDLSTL/index.md), [SDLSTH](../SDLSTL/index.md)  
  
previous: [CHACTL](../CHACTL/index.md)  
  
next: [HSCROL](../HSCROL/index.md)  
