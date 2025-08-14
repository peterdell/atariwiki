||ADR||HEXADR||NAME||Description||shadow||OS  
|1|$0001|NGFLAG| | |X  
  
Diese Speicherzelle dient zur Feststellung ob RAM- oder ROM-Fehler bei der Speicherüberprüfung während des Bootvorgangs aufgetreten sind.  
  
Dazu wird im Flag beim Start des Bootvorgangs Bit Null gesetzt. Bei jedem Fehler wird das Register um ein Bit nach rechts verschoben.  
  
||Null:|es wurden Speicher-Fehler während des Bootvorgangs festgestellt  
||Eins:|keine Speicherfehler  
