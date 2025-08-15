---
title: HPOSP2
---
%%tabbedSection  
%%tab-english  
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|Write| 53250 |$D002|HPOSP2|horizontal position of player 2|both  
|Read| 53250 |$D002|M2PF|missile 2 collision with playfield|both  
  
### Write: Horizontal position of player 2  
Values from 0 to 255, player is visible between 48 to 208 depending on playfield width (see [SDMCTL](../SDMCTL/index.md)) and width of player (see [SIZEP2](../SIZEP2/index.md)).  
### Read: Missile 2 collision with playfield  
  
||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|Playfield| | | |  |3| 2| 1| 0  
Playfield corresponds to [COLOR0](../COLOR0/index.md), ..., [COLOR3](../COLOR3/index.md) color register  
/%  
%%tab-deutsch  
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|Write| 53250 |$D002|HPOSP2|Horizontale Position Player 2|both  
|Read| 53250 |$D002|M2PF|Kollision Missile 2 mit Playfield|both  
  
### Write: Horizontale Position von Player 2  
Werte von 0 bis 255 möglich, Player sichtbar zwischen 48 bis 208 abhängig von der Spielfeldbreite (siehe [SDMCTL](../SDMCTL/index.md)) und Breite des Players (siehe [SIZEP2](../SIZEP2/index.md)).  
  
### Read: Kollision Missile 2 mit Playfield  
  
||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|Playfield| | | |  |3| 2| 1| 0  
Playfield entspricht dem Farbregister [COLOR0](../COLOR0/index.md), ..., [COLOR3](../COLOR3/index.md)  
/%  
/%  
---
see also:[Player Missile Topics](../Pm_topics/index.md)  
  
previous: [HPOSP1](../HPOSP1/index.md), [M1PF](../HPOSP1/index.md)  
  
next: [HPOSP3](../HPOSP3/index.md), [M3PF](../HPOSP3/index.md)  
