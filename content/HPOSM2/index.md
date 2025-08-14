%%tabbedSection  
%%tab-english  
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|Write| 53254 |$D006|HPOSM2|horizontal position of missile 2|both  
|Read| 53254 |$D006|P2PF|player 2 collision with playfield|both  
  
### Write: Horizontal position of missile 2  
Values from 0 to 255, missile is visible between 48 to 208 depending on playfield width (see [SDMCTL](../SDMCTL/index.md)) and width of missile (see [SIZEM](../SIZEM/index.md)/M2).  
### Read: Player 2 collision with playfield  
  
||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|Playfield| | | |  |3| 2| 1| 0  
Playfield corresponds to [COLOR0](../COLOR0/index.md), ..., [COLOR3](../COLOR3/index.md) color register  
/%  
%%tab-deutsch  
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|Write| 53254 |$D006|HPOSM2|Horizontale Position Missile 2|both  
|Read| 53254 |$D006|P2PF|Kollision Player 2 mit Playfield|both  
  
### Write: Horizontale Position von Missile 2  
Werte von 0 bis 255 möglich, Missile sichtbar zwischen 48?? bis 208?? abhängig von der Spielfeldbreite (siehe [SDMCTL](../SDMCTL/index.md)) und Breite des Missiles (siehe [SIZEM](../SIZEM/index.md)/M2).  
  
### Read: Kollision Player 2 mit Playfield  
  
||Bit ||7|| 6|| 5|| 4|| 3|| 2|| 1 ||0  
|Playfield| | | |  |3| 2| 1| 0  
Playfield entspricht dem Farbregister [COLOR0](../COLOR0/index.md), ..., [COLOR3](../COLOR3/index.md)  
/%  
/%  
---
see also:[Player Missile Topics](../Pm_topics/index.md)  
  
previous: [HPOSM1](../HPOSM1/index.md), [P1PF](../HPOSM1/index.md)  
  
next: [HPOSM3](../HPOSM3/index.md), [P3PF](../HPOSM3/index.md)  
