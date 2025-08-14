||R/W||Adr||Hex||Name||description||OS||Shadow of  
|R/W|755|$02F3|CHACT|Character display mode|all|[CHACTL](../CHACTL/index.md) 54273/$D401  
  
Character Mode Register. Zero means normal inverse characters, one is blank inverse characters (inverse characters will be printed as blanks, i.e., invisible), two is normal characters, three is solid inverse characters. Four to seven is the same as zero to three, but prints the display upside down. This register also controls the transparency of the cursor. It is transparent with values two and six, opaque with values three and seven. The cursor is absent with values zero, one, four and five.  
  
See [CHACTL](../CHACTL/index.md) for a table with explanations.  
  
see also: [CRSINH](../CRSINH/index.md), [ANTIC](../ANTIC/index.md)  
