%%tabbedSection  
%%tab-english  
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|Write| 53249 |$D001|HPOSP1|horizontal position of player 1|both  
|Read| 53249 |$D001|M1PF|missile 1 collision with playfield|both  
  
### Write: Horizontal position of player 1  
Values from 0 to 255, player is visible between 48 to 208 depending on playfield width (see [SDMCTL](../SDMCTL/index.md)) and width of player (see [SIZEP1](../SIZEP1/index.md)).  
### Read: Missile 1 collision with playfield  
  
||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|Playfield| | | |  |3| 2| 1| 0  
Playfield corresponds to [COLOR0](../COLOR0/index.md), ..., [COLOR3](../COLOR3/index.md) color register  
/%  
%%tab-deutsch  
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|Write| 53249 |$D001|HPOSP1|Horizontale Position Player 1|both  
|Read| 53249 |$D001|M1PF|Kollision Missile 1 mit Playfield|both  
  
### Write: Horizontale Position von Player 1  
Werte von 0 bis 255 möglich, Player sichtbar zwischen 48 bis 208 abhängig von der Spielfeldbreite (siehe [SDMCTL](../SDMCTL/index.md)) und Breite des Players (siehe [SIZEP1](../SIZEP1/index.md)).  
  
### Read: Kollision Missile 1 mit Playfield  
  
||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|Playfield| | | |  |3| 2| 1| 0  
Playfield entspricht dem Farbregister [COLOR0](../COLOR0/index.md), ..., [COLOR3](../COLOR3/index.md)  
/%  
/%  
---
see also:[Player Missile Topics](../Pm_topics/index.md)  
  
previous: [HPOSP0](../HPOSP0/index.md), [M0PF](../HPOSP0/index.md)  
  
next: [HPOSP2](../HPOSP2/index.md), [M2PF](../HPOSP2/index.md)  
