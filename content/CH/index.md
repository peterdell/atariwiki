||ADR||HEXADR||NAME||Description||OS  
|764|$02FC|CH|internal key code|all  
  
Enthält den internen Tastaturcode der gedrückten Taste. Manchmal hat der ATARI noch ein Zeichen im Speicher, welches vor längerer Zeit gedrückt wurde; möchte man dies verhindern, schreibt man $FF (255) in die Speicherzelle $02FC (764).  
  
The value $11 (or $51 or $91) for the HELP key does never appear in [CH](../CH/index.md)! It does appear in [KBCODE](../KBCODE/index.md) and is transferred from there to [HELPFG](../HELPFG/index.md).  
  
## Hexadecimal Values  
|| ||$00||$01||$02||$03||$04||$05||$06||$07||$08||$09||$0A||$0B||$0C||$0D||$0E||$0F  
|$00|L|J|;|F1|F2|K|+|*|O| |P|U|CR|I|-|=  
|$10|V| |C|F3|F4|B|X|Z|4| |3|6|Esc|5|2|1  
|$20|,|Spc|.|N| |M|/|Inv|R| |E|Y|Tab|T|W|Q  
|$30|9| |0|7|BS|8|<|>|F|H|D| |Caps|G|S|A  
  
together with Shift Key: add 64 ($40)  
together with Control key: add 128 ($80)  
  
## Decimal Values  
||.. ||.0||.1||.2||.3||.4||.5||.6||.7||.8||.9  
|0.|L|J|;|F1|F2|K|+|*|O|  
|1.|P|U|CR|I|-|=|V| |C|F3  
|2.|F4|B|X|Z|4| |3|6|Esc|5  
|3.|2|1|,|Spc|.|N| |M|/|Inv  
|4.|R| |E|Y|Tab|T|W|Q|9|  
|5.|0|7|BS|8|<|>|F|H|D|  
|6.|Caps|G|S|A  
  
Spc SPACE, CR RETURN, Tab TAB, Caps CAPS, Inv INVERS/ATARI-Key, Esc Escape, BS BACKSPACE, Help HELP  
  
together with Shift Key: add 64 ($40)  
together with Control key: add 128 ($80)  
  
---
see also: [Keyboard topics](../Keyboard_topics/index.md) [Console Keys](../CONSOL/index.md) [HELP](../HELPFG/index.md)  
