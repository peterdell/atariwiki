||Read/Write||ADR||HEXADR||NAME||Description||shadow||OS  
|Read|53762|$D202|POT2|Pot/paddle 2|626|all  
|Write|53762|$D202|AUDF2| Audio channel 2 frequency |none|all  
  
## Read  
Reads the value of pot (paddle) 2.  
  
## Write  
Frequency of Audio channel 1. This value can be between 0 ($00) and 255 ($FF), where 0 is the highest tone/pitch and 255 is the lowest tone/pitch.  
  
  
With a base frequency of 64kHz, distortion=10 and A3=443Hz the following values define the respective notes for PAL-ATARIs  
||Octave||C||#C||D||#D||E||F||#F||G||#G||A||#A||H  
|2|239|226|213|201|190|179|169|159|150|142|134|126  
|3|119|112|106|100|94|89|84|79|75|70|66|63  
|4|59|56|53|50|47|44|42|39|37|35|33|31  
|5|29|27|26|24|23|22|20|19|18|17|16|15  
|6|14|13|(12)|(12)|11|10| |9| |8| |7  
  
For NTSC-ATARIs use the following values defining the respective notes (distortion=10, A3=443Hz)  
||Octave||C||#C||D||#D||E||F||#F||G||#G||A||#A||H  
|2|243|230|217|204|193|182|173|162|153|144|136|128  
|3|121|114|108|102|96|91|85|81|76|72|68|64  
|4|60|57|53|50|47|45|42|40|37|35|33|31  
|5|29|27|26|24|23|22|20|19|18|17|16|15  
  
  
  
Use [AUDC2](../AUDC2/index.md) to set distortion and volume for channel 2.  
---
  
see also: [Sound_Topics](../Sound_Topics/index.md), [AUDCTL](../AUDCTL/index.md), [STIMER](../KBCODE/index.md)  
  
previous: [AUDC1](../AUDC1/index.md)  
  
next: [AUDC2](../AUDC2/index.md)  
