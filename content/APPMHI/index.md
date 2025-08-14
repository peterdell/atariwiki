||ADR||HEXADR||NAME||Description||shadow||OS  
|14,15|$000E,$000F|APPMHI|__APP__lications __M__emory __HI__gh limit| |all  
  
Dieser Zeiger gibt an, bis zu welcher Adresse sich ein Programm oder Daten erstrecken können.  
Damit Benutzerdaten bzw. Programmdaten nicht überschriben werden, wird bei Aufruf eines GRAPHICS-Befehles oder eines OPEN-Befehl für den Bildschirm über die CIO in Maschinensprache oberhalb von APPMHI geprüft ob genügend Speicher für die Bildschirmdaten und die Displayliste zur Verfügung stehen.  
Fällt diese Prüfung postiv aus, wird der Befehl ausgefürt, andernfalls wird in GRAPHICS 0 zurückgeschaltet und ein Fehler ausgegeben.  
  
---
  
Siehe auch:  
*[MEMTOP](../MEMTOP/index.md) - Adresse oberhalb derer die Bildschirmdaten und die Displaylist liegen können  
