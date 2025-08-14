# Memory Map for Player Missile Graphics  
||single line resolution|| | || double line resolution||  
||dec ||hex ||data ||dec ||hex  
|0-767 |$0000-$02FF |not used by PM graphicse.g. can be used for storing horizontal position of players or shapes |0-383 |$0000-$017F  
|768-1023 |$0300-$03FF |Missiles |384-511 |$0180-$01FF  
|1024-1279 |$0400-$04FF |Player 0 |512-639 |$0200-$027F  
|1280-1535 |$0500-$05FF |Player 1 |640-767 |$0280-$02FF  
|1536-1791 |$0600-$06FF |Player 2 |768-895|$0300-$037F  
|1792-2047 |$0700-$07FF|Player 3 |896-1023|$0380-$03FF  
  
for switching between single and double line resolution see Bit 5 of [SDMCTL](../SDMCTL/index.md)  
  
for adjusting the vertical position in double line resolution see [VDELAY](../VDELAY/index.md)  
  
for setting the base address of the PM memory map see [PMBASE](../PMBASE/index.md)  
  
see also:[Player Missile Topics](../Pm_topics/index.md)  
