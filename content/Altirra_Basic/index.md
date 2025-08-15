---
title: Altirra Basic
---
# Altirra BASIC  
Copyright (C) 2014 Avery Lee, 2014  
  
Copying and distribution of this file, with or without modification, are permitted in any medium without royalty provided the copyright notice and this notice are preserved. This file is offered as-is, without any warranty.  
  
### Background  
Altirra BASIC is a completely new BASIC interpreter that is fully compatible with [Atari_BASIC](../Atari_BASIC/index.md) while being completely different internally. It normally ships as part of the Altirra 8-bit emulation system, but can also be loaded into any Atari from disk, or in theory, burned to ROM. The main improvements in Altirra are a bottom-up parser that replaces the top-down system found in most interpreters, fixes for the notoriously slow line-lookups in Atari BASIC, and cleanups to the code throughout.  
  
The other main source of slowness in Atari BASIC was the floating point (FP) routines. [Turbo-BASIC_XL](../Turbo-BASIC_XL/index.md) replaced these for a great improvement in performance. Altirra BASIC does not, it calls whatever FP routines are found in the machine's ROMs. However, the Altirra emulator contains a second set of FP ROMs that can be optionally turned on, addressing this issue. This FP package, unlike TURBOs, remains fully compatible with Atari's original version and is suitable for burning to ROM. Because it does not include its own FP library, Altirra has more free memory on startup.  
  
Atari Wiki is proud to have the license to publish Avery Lee's outstanding Altirra Basic. Avery has done a marvelous job in creating this Basic. Further, he has published the source code, too. :-) Avery, the Atari community say thank you so much for your contribution, we all appreciate very much. Please go ahead with your fantastic work.  
## CAR-Image:  
Altirra BASIC 1.29: [atbasic.car](attachments/atbasic.car) ; size: 12 KB  
## BIN-Image:  
Altirra BASIC 1.29: [atbasic.bin](attachments/atbasic.bin) ; size: 8 KB  
## ATR-Image:  
Altirra BASIC 1.29: [Altirra_Basic_1.29_with_DOS_II_2.5.atr](attachments/Altirra_Basic_1.29_with_DOS_II_2.5.atr) ; ATR-Image with DOS 2.5 and Altirra BASIC 1.29 as AUTORUN.SYS file  
Altirra BASIC 1.54: [Additions.atr](attachments/Additions.atr) ; plus additions from Avery's site. Thank you so much Avery! :-))) We really(!) need your work. :-)))  
## Images:  
![](attachments/Altirra1.jpg)  
Altirra BASIC 1.29 after starting from the ATR-image  
![](attachments/Altirra2.jpg)  
Sectors needed for Altirra BASIC 1.29 on the SD-ATR-image above  
## Reference:  
The original, actual version and the source code of Altirra Basic can be found can be found here:  
[Altirra at virtualdub.org](http://www.virtualdub.org/altirra.html)  
The source code itself is published within the Altirra source code package (src/ATBasic/*). For the license please see at the top of the page.  
## Manual:  
please stand by  
  
