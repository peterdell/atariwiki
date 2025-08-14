||R/W||ADR||HEXADR||NAME||DESCRIPTION||OS  
|W|54282|$D40A|WSYNC|Stops CPU until end of scanline is reached|all  
  
Wird eine beliebige Zahl in dieses Register geschrieben, wird die CPU (6502) solange angehalten, bis das Ende der Scanline (Bildschirmzeile) erreicht ist. Es ist sinnvoll einen Display List Interrupt in der Zeile VOR der gewünschten Zeile zu setzen, damit beim Zeilen-Strahlrücklauf der Interrupt abgearbeitet werden kann, ohne z.B. Flackern bei einer Farbumschaltung zu verursachen.  
  
Die "Klick"-Routine der Tastatur benutzt dieses Register zur Verzögerung.  
  
---
see also: [Interrupts](../Interrupts/index.md)  
  
previous: [CHBASE](../CHBASE/index.md)  
  
next: [VCOUNT](../VCOUNT/index.md)  
