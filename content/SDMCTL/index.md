---
title: SDMCTL
---
%%tabbedSection  
%%tab-english  
  
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS||SHADOW||DEFAULT  
|read/write|559|$022F |SDMCTL|Direct Memory Access (DMA) Control|all|[DMACTL](../DMACTL/index.md)|34/$22  
  
This memory location is the shadow register of [DMACTL](../DMACTL/index.md) (54272; $D400). It is used to control the [ANTIC](../ANTIC/index.md)'s direct memory access ("DMA") to the memory of the Atari. The 6502 processor is halted during direct memory access. By switching the ANTIC's DMA off programs can be accelerated (approx. 30%). The following list shows how the individual bits of this register control the appearance of the screen:  
  
||Bit||Dec||Hex||Function||Default  
|7   |    128 |    $80 |    not used|0  
|6    |   64 |     $40  |   not used|0  
|5	|32|	$20|	Direct Memory Access on=1/off=0|1  
|4|	16|	$10|	One-line P/M-vertical resolution on=1/off=0|0  
|3|	8|	$8|	DMA for Players on=1/off=0|0  
|2|	4|	$4|	DMA for Missiles on=1/off=0|0  
|0,1|	3|	$3|	Wide playfield (48 bytes/chars)|  
|0,1|	2|	$2|	Normal playfield (40 bytes/chars)|10  
|0,1|	1|	$1|	Narrow playfield (32 bytes/chars)|  
|0,1|	0|	$0|	Playfield off|  
  
Bit #5 can therefore be used to control the entire direct memory access of the ANTIC. Bit #4 is used to switch between single-line P/M resolution and two-line resolution. The specification of the character width for the display playfield refers to the graphic mode 0. The numbers of characters correspond to 192, 160 or 128 color cycles. In total, the ANTIC can display 238 color cycles (including the border), but only about 174 of these are visible, depending on the TV/monitor. Therefore, not all 48 characters are completely visible when a wide display field is switched on (or the image extends beyond the edge of the monitor).  
  
To switch on the Display List Interrupt see [NMIEN](../NMIEN/index.md).  
---
/%  
%%tab-deutsch  
  
||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS||SHADOW||DEFAULT  
|read/write|559|$022F |SDMCTL|Direct Memory Access (DMA) Control|all|[DMACTL](../DMACTL/index.md)|34/$22  
  
  
Diese Speicherzelle ist das Schattenregister zu [DMACTL](../DMACTL/index.md) (54272; $D400). Sie dient der Kontrolle des direkten Speicherzugriffs ("Direct Memory Access", [DMA](../DMA/index.md)) des ANTIC auf den Speicher des Atari. Der 6502-Prozessor wird während des direkten Speicherzugriffs abgeschaltet. Durch die Abschaltung des DMA des [ANTIC](../ANTIC/index.md) können Programme beschleunigt (ca. 30%) werden. Anhand folgender Aufstellung sieht man, wie die einzelnen Bits dieses Registers das Aussehen des Bildschirms kontrollieren:  
  
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
  
Zum Einschalten des Display List Interrupts siehe [NMIEN](../NMIEN/index.md).  
---
/%  
  
  
see also: [Player Missile Topics](../Pm_topics/index.md), [Display List Topics](../Displaylist_topics/index.md)  
  
previous: [CDTMF5](../CDTMF5/index.md)  
  
next: [SDLSTL](../SDLSTL/index.md),[SDLSTH](../SDLSTL/index.md)  
