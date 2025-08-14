||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS||SHADOW||DEFAULT  
|read/write|54272|$D400 |DMACTL|Direct Memory Access (DMA) Control|all|[SDMCTL](../SDMCTL/index.md)|34/$22  
  
  
Diese Speicherzelle der Kontrolle des direkten Speicherzugriffs ("Direct Memory Access", [DMA](../DMA/index.md)) des ANTIC auf den Speicher des Atari. Der 6502-Prozessor wird während des direkten Speicherzugriffs abgeschaltet. Durch die Abschaltung des DMA des [ANTIC](../ANTIC/index.md) können Programme beschleunigt (ca. 30%) werden. Anhand folgender Aufstellung sieht man, wie die einzelnen Bits dieses Registers das Aussehen des Bildschirms kontrollieren:  
  
||Bit||Dec||Hex||Function||Default  
|7   |    128 |    $80 |    not used|0  
|6    |   64 |     $40  |   not used|0  
|5	|32|	$20|	Direct Memory Access on=1/off=0/aus|1  
|4|	16|	$10|	Einzeilige P/M-Auflösung on=1/off=0|0  
|3|	8|	$8|	DMA für Player on=1/off=0|0  
|2|	4|	$4|	DMA für Missiles on=1/off=0|0  
|0,1|	3|	$3|	Breites Anzeigefeld (48 Zeichen)|  
|0,1|	2|	$2|	Normales Anzeigefeld (40 Zeichen)|10  
|0,1|	1|	$1|	Schmales Anzeigefeld (32 Zeichen)|  
|0,1|	0|	$0|	Kein Anzeigefeld|  
  
Mit Bit fünf kann man also den gesamten direkten Speicherzugriff des ANTIC kontrollieren. Das Bit vier dient dem Umschalten zwischen einzeiliger P/M-Auflösung und zweizeiliger Auflösung. Die Angabe der Zeichenbreite für das Anzeigefeld bezieht sich auf die Grafikstufe Null. Die Anzahlen der Zeichen entsprechen 192, 160 oder 128 Farbpunkten. Insgesamt kann der ANTIC 238 Farbpunkte (einschließlich des Randes) darstellen, davon sind jedoch je nach Fernseher/Monitor nur ca. 174 sichtbar. Es sind deshalb beim Einschalten eines breiten Anzeigefeldes nicht alle 48 Zeichen vollständig sichtbar (bzw. das Bild geht über den Rand des Monitors hinaus).  
  
---
see also: [Player Missile Topics](../Pm_topics/index.md)  
  
previous: [PBCTL](../PBCTL/index.md) of PIA  
  
next: [CHACTL](../CHACTL/index.md)  
