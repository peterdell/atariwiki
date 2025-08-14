||R/W||Adr||Hex||Name||Description||OS||default  
|R/W|752|$2F0|CRSINH|Cursordarstellung|all|0  
  
||Wert||Auswirkung  
|0|Cursor sichtbar  
|1-255|Cursor unsichtbar  
  
Erst nach einer Cursorbewegung wird die Änderung in diesem Registers wirksam.  
Das Drücken der Tasten BREAK oder RESET, die Änderung der Grafikstufe oder das Öffnen eines I/O-Kanals zum Bildschirm (S:) oder Editor (E:) stellt den Default-Wert wieder her - der Cursor wird wieder sichtbar.  
  
siehe auch: [CHACT](../CHACT/index.md), [CHACTL](../CHACTL/index.md)  
