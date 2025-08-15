---
title: Connectors
---
### SIO-Connector  
```
     __________________________ 
    /                          \ 
   /   2   4   6   8   10  12   \ 
  /                              \
 /   1   3   5   7   9   11  13   \
/__________________________________\
```
||lower row||upper row  
|1 Clock Input|2 Clock Output  
|3 Data Input|4 Ground  
|5 Data Output |6 Ground  
|7 _Command|8 Motor control  
|9 _Proceed |10 +5V DC/Ready  
|11 Audio Input |12 +12V DC  
|13 _Interrupt  
  
Notes:  
- _=active low  
- Pin 10: +5V DC not on 1200XL  
- Pin 12: +12V DC on 400/800 only. 1400XL/1450XLD?  
  
### Joystick-Connector  
```
_________________________
\                       /
 \  1   2   3   4   5  /
  \                   /  
   \  6   7   8   9  /
    \_______________/ 
```
||lower row||upper row  
|1 Up|6 Trigger  
|2 Down|7 +5V DC  
|3 Left|8 Ground  
|4 Right|9 Pot A  
|5 Pot B  
1-4 see [STICK0](../STICK0/index.md)-[STICK3](../STICK3/index.md), 3 also Paddle Trigger A see [PTRIG0](../PTRIG0/index.md), 4 also Paddle Trigger B see [PTRIG1](../PTRIG1/index.md)  
5,9 see [PADDL0](../PADDL0/index.md)-[PADDL7](../PADDL7/index.md)  
6 see [STRIG0](../STRIG0/index.md)-[STRIG3](../STRIG3/index.md),  also Light Pen Input, see [LPENV](../LPENV/index.md), [LPENH](../LPENH/index.md), (400 supports a light pen or light gun in port 4 only)  
7 +5V  
  
### Monitor Connector  
  
```
   3 o           o 1

    5 o         o 4
           o
           2
```
5 PIN DIN 180° (DIN41524) FEMALE at the computer.  
  
||Pin||Description  
|1| Composite Luminance (Composite Video on PAL 600XL)  
|2| Ground  
|3| Audio Output  
|4| Composite Video  
|5| Composite Chroma (not on 800XL (except "800XLF"), 1200XL; Ground on PAL 600XL)  
  
### Power Connector  
not on 400, 800, 1200XL  
```
    7 o         o 6

  3 o             o 1

    5 o         o 4
           o
           2
```
7 PIN DIN 'C' FEMALE at the computer.  
||Pin||	 Description  
|1| +5V  
|2| Shield  
|3| Ground  
|4| +5V  
|5| Ground  
|6| +5V  
|7| Ground  
  
Power consumption  
||Model||Current @ 5VDC  
|130XE|1.5A  
|65XE| 1.0A  
|800XE| 1.0A  
|XE| 1.0A  
|600XL| 1.5A  
|800XL| 1.5A  
  
### (Left) Cartridge  
on all machines; "Left Cartridge" on 800  
```
A B C D E F H J K L M N P R S 
o o o o o o o o o o o o o o o
o o o o o o o o o o o o o o o
1                           15 
```
||upper row||lower row  
|1. _S4 Chip Select $8000 to $9FFF |A. RD4 ROM present $8000 to $9FFF  
|2. A3 CPU Address bus line |B. GND Ground  
|3. A2 CPU Address bus line |C. A4 CPU Address bus line  
|4. A1 CPU Address bus line |D. A5 CPU Address bus line  
|5. A0 CPU Address bus line |E. A6 CPU Address bus line  
|6. D4 CPU Data bus line |F. A7 CPU Address bus line  
|7. D5 CPU Data bus line |H. A8 CPU Address bus line  
|8. D2 CPU Data bus line |J. A9 CPU Address bus line  
|9. D1 CPU Data bus line |K. A12 CPU Address bus line  
|10. D0 CPU Data bus line |L. D3 CPU Data bus line  
|11. D6 CPU Data bus line |M. D7 CPU Data bus line  
|12. _S5 Chip Select  $A000 to $BFFF |N. A11 CPU Address bus line  
|13. +5V |P. A10 CPU Address bus line  
|14. RD5 ROM present $A000 to $BFFF |R. R/_W CPU read/write  
|15. _CCTL Cartridge control select |S. B02,Phi2 CPU Phase 2 clock  
_=active low  
  
### Right Cartridge (800 only)  
```
A B C D E F H J K L M N P R S
o o o o o o o o o o o o o o o
o o o o o o o o o o o o o o o
1                           15 
```
||upper row||lower row  
|1. R/_W CPU read/write late |A. B02,Phi2 CPU Phase 2 clock  
|2. A3 CPU Address bus line |B. GND Ground  
|3. A2 CPU Address bus line |C. A4 CPU Address bus line  
|4. A1 CPU Address bus line |D. A5 CPU Address bus line  
|5. A0 CPU Address bus line |E. A6 CPU Address bus line  
|6. D4 CPU Data bus line |F. A7 CPU Address bus line  
|7. D5 CPU Data bus line |H. A8 CPU Address bus line  
|8. D2 CPU Data bus line |J. A9 CPU Address bus line  
|9. D1 CPU Data bus line |K. A12 CPU Address bus line  
|10. D0 CPU Data bus line |L. D3 CPU Data bus line  
|11. D6 CPU Data bus line |M. D7 CPU Data bus line  
|12. _S4 Chip Select--$8000 to $9FFF |N. A11 CPU Address bus line  
|13. +5V |P. A10 CPU Address bus line  
|14. RD4 ROM present--$8000 to $9FFF |R. R/_W Read/write  
|15. _CCTL Cartridge control select |S. B02,Phi2 CPU Phase 2 clock  
_=active low  
  
### Enhanced Cartridge Interface (ECI)/Expansion port  
only on 130XE, 800XE and later 65XE versions  
```
  A B C D E F H 
  o o o o o o o 
  o o o o o o o 
  1 2 3 4 5 6 7 
```
||upper row ||lower row  
|A. Reserved | 1. _EXTSEL External Select  
|B. _IRQ Interrupt request | 2. _RST Reset output  
|C. _HALT Halt CPU |3. _D1XX Chip select at area $D1xx  
|D. A13 CPU Address bus line | 4. _MPD Math Pack (FP) Disable  
|E. A14 CPU Address bus line |5. Audio input  
|F. A15 CPU Address bus line | 6. _REF Refresh cycle  
|H. GND Ground |7. +5V  
_=active low  
  
### Parallel Bus Interface (PBI)  
only on 600XL and 800XL  
```
1                                               49 
o o o o o o o o o o o o o o o o o o o o o o o o o   (upper side of PCB)
o o o o o o o o o o o o o o o o o o o o o o o o o   (lower side of PCB)
2                                               50
```
||upper row||lower row  
|1. GND Ground |2. _EXTSEL External Select  
|3. A0 CPU Address bus line |4. A1 CPU Address bus line  
|5. A2 CPU Address bus line |6. A3 CPU Address bus line  
|7. A4 CPU Address bus line |8. A5 CPU Address bus line  
|9. A6 CPU Address bus line |10. GND Ground  
|11. A7 CPU Address bus line |12. A8 CPU Address bus line  
|13. A9 CPU Address bus line |14. A10 CPU Address bus line  
|15. A11 CPU Address bus line |16. A12 CPU Address bus line  
|17. A13 CPU Address bus line |18. A14 CPU Address bus line  
|19. GND Ground |20. A15 CPU Address bus line  
|21. D0 CPU Data bus line |22. D1 CPU Data bus line  
|23. D2 CPU Data bus line |24. D3 CPU Data bus line  
|25. D4 CPU Data bus line |26. D5 CPU Data bus line  
|27. D6 CPU Data bus line |28. D7 CPU Data bus line  
|29. GND Ground |30. GND Ground  
|31. B02,Phi2 CPU Phase 2 clock |32. GND Ground  
|33. NC Reserved |34. _RST Reset output  
|35. _IRQ Interrupt request |36. _RDY Ready input  
|37. NC Reserved |38. _EXTENB CPU External decoder Enable  
|39. NC Reserved |40. _REF Refresh cycle  
|41. _CAS Column Address Strobe |42. GND Ground  
|43. _MPD Math Pack (FP) Disable |44. _RAS Row Address Strobe  
|45. GND Ground |46. LR/_W Latched read/write  
|47. 800XL: NC. 600XL: +5V |48. 800XL: NC. 600XL: +5V  
|49. Audio input |50. GND Ground  
_=active low  
---
with information from:  
- [http://www.faqs.org/faqs/atari-8-bit/faq/](http://www.faqs.org/faqs/atari-8-bit/faq/)  
- [http://www.hardwarebook.info/](http://www.hardwarebook.info/)  
---
see [topic_list](../topic_list/index.md)  
