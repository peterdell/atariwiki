---
title: RAMLO
---
||ADR||HEXADR||NAME||Description||shadow||OS  
|4,5|$0004,$0005|RAMLO| | |all  
  
RAMLO hat mehrere Verwendungsmöglichkeiten, allerdings keine, die für den Nutzer relevant sind.  
  
Diese Speicherzelle wird als Zeiger für den Speichertest während des Einschaltvorgangs benutzt.  
(RAMLO, [TRAMSZ](../TRAMSZ/index.md) und [TSTDAT](../TSTDAT/index.md) arbeiten hierbei zusammen.)  
  
Hier wird auch die Adresse für die Fortsetzung des Disketten- oder Kassettenbootvorgangs (dies ist die Ladeadresse plus sechs - normalerweise 1798;$0706) abgelegt.  
