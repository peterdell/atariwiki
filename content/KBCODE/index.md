||r/w||ADR||HEXADR||NAME||Description||OS  
|read|53769|$D209|KBCODE|internal key code|all  
|write|53769|$D209|STIMER|Start the POKEY Timers|all  
  
# Read  
  
Enthält den internen Tastaturcode der zuletzt gedrückten Taste.  
  
## Hexadecimal Values  
|| ||$00||$01||$02||$03||$04||$05||$06||$07||$08||$09||$0A||$0B||$0C||$0D||$0E||$0F  
|$00|L|J|;|F1|F2|K|+|*|O| |P|U|CR|I|-|=  
|$10|V|Help|C|F3|F4|B|X|Z|4| |3|6|Esc|5|2|1  
|$20|,|Spc|.|N| |M|/|Inv|R| |E|Y|Tab|T|W|Q  
|$30|9| |0|7|BS|8|<|>|F|H|D| |Caps|G|S|A  
  
together with Shift Key: add +$40  
  
together with Control key: add +$80  
  
## Decimal Values  
|| ||7||6||5||4||3||2||1||0  
|0|*|+|K|F2|F1|;|J|L  
|8|=|-|I|CR|U|P| |O  
|16|Z|X|B|F4|F3|C|Help|V  
|24|1|2|5|Esc|6|3| |4  
|32|inv|/|M| |N|.|Spc|,  
|40|Q|W|T|Tab|Y|E| |R  
|48|>|<|8|BS|7|0| |9  
|56|A|S|G|Caps| |D|H|F  
  
Spc SPACE, CR RETURN, Tab TAB, Caps CAPS, Inv INVERS/ATARI-Taste, Esc Escape, BS BACKSPACE, Help HELP  
  
together with Shift Key: add 64  
  
together with Control key: add 128  
  
  
# Write  
Start the POKEY timers (the AUDF registers above). You POKE any non-zero value here to load and start the timers; the value isn't itself used in the calculations. This resets all of the audio frequency dividers to their AUDF values. If enabled by [IRQEN](../IRQEN/index.md) below, these AUDF registers generate timer interrupts when they count down from the number you POKEd there to zero. The vectors for the [AUDF1](../AUDF1/index.md), [AUDF2](../AUDF2/index.md) and [AUDF4](../AUDF4/index.md) timer interrupts are located between 528 and 533 ($210 and $215) [VTIMR1](../VTIMR1/index.md), [VTIMR2](../VTIMR2/index.md), [VTIMR4](../VTIMR4/index.md). POKEY timer four interrupt is only enabled in the new "B" OS ROMs.  
  
---
see also: [Keyboard topics](../Keyboard_topics/index.md) [Console Keys](../CONSOL/index.md) [HELP](../HELPFG/index.md)  
  
previous: [AUDCTL](../AUDCTL/index.md),[ALLPOT](../ALLPOT/index.md)  
  
next: [SKREST](../SKREST/index.md),[RANDOM](../SKREST/index.md)  
