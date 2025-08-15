---
title: DiffOldOs2XL
---
# OS Diffs Atari 800 <-> Atari XL/XE Series  
  
__Answers-Tips-and-Relevant Information__  
  
[by Paul Alhart](..//index.md)  
  
I really like my 1200XL, but at the same time I really hate having to use  
the TRANSLATOR to boot up certain software. What to do? I Translated the  
offending software to run on my system and filed my Translator Disk away in  
the back of a drawer somewhere.  
  
You can do the same. In the beginning, Atari  
said, "If programmers use the PUBLISHED VECTORS into the Operating System  
(O/S), their programs will run on ANY 8-bit Atari Computer." (IF is such a  
big word.) To make a long story short, some programmers did not follow this  
rule, but to save a few bytes, jumped right into the O/S. This was fine  
before the XL/XE machines came along with a different O/S.  
  
The published  
vectors are still the same as Atari promised, but they point to different  
locations in the O/S. The following list gives the published vector location  
and the vectors name followed by the ILLEGAL O/S entry points. If you find  
that a program Jumps to F3F6 to open the screen, (20 F6 F3)  and you have an  
800XL, change the code to (20 8E EF). Remember: Low byte/High byte.  
  
I have  
found this to be the most common ILLEGAL jump. The next most common are the  
"K: Get/Put" calls.  I spent many hours Peeking into my operating system  
with a lot of help from Compute's Mapping The Atari to come up with this  
list. It now saves me lots of time and hopefully will help you also.  
Note: Translated software will only run on the O/S that it has been  
translated for, so keep an original copy as back-up.  
  
  
||   Vector||Label||800||XL/XE||1200XL||  
| 200 |  VDSLST  |   E790  |   C0CE  |   C0E7  |  
| 202 |  VPRCED  |   E78F  |   C0CD  |   C0E6  |  
| 204 |  VINTER  |   E78F  |   C0CD  |   C0E6  |  
| 206 |  VBREAK  |   E78F  |   C0CD  |   C0E6  |  
| 208 |  VKEYBD  |   FFBE  |   FC19  |   FC0C  |  
| 20A |  VSERIN  |   EB0F  |   1A23  |   E929  |  
| 20C |  VSEROR  |   EA90  |   19E6  |   E88A  |  
| 20E |  VSEROC  |   EACF  |   EAEC  |   E8C9  |  
| 210 |  VTIMR1  |   E78F  |   C0CD  |   C0E6  |  
| 212 |  VTIMR2  |   E78F  |   C0CD  |   C0E6  |  
| 214 |  VTIMR4  |   E78F  |   C0CD  |   C0E6  |  
| 216 |  VIMIRQ  |   E706  |   C030  |   C054  |  
| 222 |  VVBLKI  |   E7AE  |   C0E2  |   C019  |  
| 224 |  VVBLKD  |   E905  |   C28A  |   C2A3  |  
| 226 |  CDTMA1  |   EBEC  |   EC11  |   EA2E  |  
| | | | |  |  
| E400 | E:OPEN  |   F3FC  |   EF94  |   EEF8  |  
| E402 | E:CLOSE |   F634  |   F2D3  |   F17E  |  
| E404 | E:GET   |   F63E  |   F24A  |   F18F  |  
| E406 | E:PUT   |   F6A4  |   F2B0  |   F1F5  |  
| E408 | E:STATUS |   F634 |    F21E |    F174  |  
| E40A | E:SPECIAL | F63D  |   F2C3  |   F17C  |  
| E40C | E:JUMP   |  F3E4  |         |   EECD  |  
| |  | |  |  |  
| E410 | S:OPEN   |  F3F6  |   EF8E  |   EEED  |  
| E412 | S:CLOSE  |  F634  |   F2D3  |   F17E  |  
| E414 | S:GET    |  F593  |   F180  |   F0D6  |  
| E416 | S:PUT    |  F5B7  |   F1A4  |   F0FA  |  
| E418 | S:STATUS |  F634  |   F21E  |   F174  |  
| E41A | S:SPECIAL |  FCFC |    F9AF |    F903  |  
| E41C | S:JUMP   |  F3E4  |   EF6F  |   EECD  |  
| | | |  |  |  
| E420 | K:OPEN   |  F634  |   F21E  |   F174  |  
| E422 | K:CLOSE  |  F634  |   F21E  |   F174  |  
| E424 | K:GET    |  F6E2  |   F2FD  |   F242/F247  |  
| E426 | K:PUT    |  F63D  |   F22D  |   F17D  |  
| E428 | K:STATUS |  F634  |   F21E  |   F174  |  
| E42A | K:SPECIAL |  F63D |    F22D |    F17D |  
| E42C | K:JUMP    | F3E4  |   EF6F  |   EECD  |  
| |  | | |  |  
| E430 | P:OPEN   |  EE9F  |   FEC2  |   EC63  |  
| E432 | P:CLOSE  |  EEDC  |   FF07  |   ECA3  |  
| E434 | P:GET    |  EE9E  |   FEC1  |   EC62  |  
| E436 | P:PUT    |  EEA7  |   FECB  |   EC6C  |  
| E438 | P:STATUS |  EE81  |   FEA3  |   EC44  |  
| E43A | P:SPECIAL |  EE9E |    FEC1 |    EC62  |  
| E43C | P:JUMP   |  EE78  |   FE9A  |   EC3A  |  
| | |  | |  |  
| E440 | C:OPEN   |  EF4C  |   FCE6  |   ED1A  |  
| E442 | C:CLOSE  |  F02B  |   FDCF  |   EE03  |  
| E444 | C:GET    |  EFD6  |   FD7A  |   EDAE  |  
| E446 | C:PUT    |  F010  |   FDB4  |   EDE8  |  
| E448 | C:STATUS |  F028  |   FDCC  |   EE00  |  
| E44A | C:SPECIAL |  EF4B |    FCE5 |    ED19  |  
| E44C | C:JUMP   |  EF41  |   FCDC  |   ED0F  |  
| | |  | |  |  
| E450 | DISKIV   |  EDEA  |   C6A3  |   C2A9  |  
| E453 | DISKINV  |  EDF0  |   C6B3  |   C2B9  |  
| E456 | CIOV     |  E4C4  |   E4DF  |   E4DF  |  
| E459 | SIOV     |  E959  |   C933  |   F74E  |  
| E45C | SETVBV   |  E8ED  |   C272  |   C28B  |  
| E45F | SYSVBV   |  E7AE  |   COE2  |   C019  |  
| E462 | XITVBX   |  E905  |   C28A  |   C2A3  |  
| E465 | SIOINV   |  E944  |   E95C  |   E739  |  
| E468 | SENDEV   |  EBF2  |   EC17  |   EA34  |  
| E46B | INTINV   |  ECD5  |   C00C  |   C00C  |  
| E46E | CIOINV   |  E4A6  |   E4C1  |   E4C1  |  
| E471 | BLKBDV   |  F223  |  _F223_ |   FCE1  _SLFTST_  |  
| E474 | WARMSV   |  F11B  |   C290  |   C34B  |  
| E477 | COLDSV   |  F125  |   C2C8  |   C37B  |  
| E47A | RBLOKV   |  EFE9  |   FD8D  |   EDC1  |  
| E47D | CSOPIV   |  EF5D  |   FCF7  |   ED2B  |  
| E480 | PUPDIV   |        |   F223  |   FCE1  |  
| E483 | SLFTST   |        |   xx    |  5000  |  
| E486 | PENTV    |        |   EEBC  |  CAAE  |  
| E489 | PHUNLV   |        |   E915  |   CAEB  |  
| E48C | PHINIV   |        |   E898  |   CA34  |  
  
  
