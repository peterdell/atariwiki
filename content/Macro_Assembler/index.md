# ATARI Macro Assembler (AMAC) DXG 8126; Copyright (C) 1981-1983 ATARI, Inc. & ATARI Elektronik Vertriebsgesellschaft mbH bzw. GmbH  
Der Atari Macro Assembler ist eine Auskopplung aus dem ATARI CAMAC Assembler Ver 1.0A, welcher wiederum eine Auskoppelung aus dem 6502 Macro Assemblers der Firma [Sorcim](https://en.wikipedia.org/wiki/Sorcim) ist. Sorcim überließ Atari ihren 6502 Macro Assembler in Sublizenz. AMAC, wie der Macro Assembler für den Atari Privatanwender auch genannt wird, war der erste Assembler für den Atari, der in der Lage war, Macros zu verarbeiten. Er war sehr erfolgreich, weil lange Zeit nichts besseres auf dem Markt war.  
  
AMAC war aber nicht der erste Assembler für den Atari. Diese Ehre gebührt allein Kathleen Ann O'Brien mit dem von ihr entwickelten [Atari_Assembler_Editor](../Atari_Assembler_Editor/index.md), welcher neben dem Assembler auch über einen Editor und Debugger verfügte und als Steckmodul verfügbar war.  
  
Nur der Macro Assembler selber als Programm wäre schwierig zu verkaufen gewesen, daher wurde das Programm noch durch einen Editor ergänzt. Hier kam der universelle [Programm_Text_Editor](../Programm_Text_Editor/index.md) von Mike Lorenzen zum Einsatz, mit dem man nicht nur Programme in Assembler schreiben konnte, sondern auch in anderen Programmiersprachen sowie einfache Texte verarbeiten konnte. Das Programm war jedoch nicht in AMAC integriert, sondern nur als separates Programm verfügbar und musste jeweils neu gestartet werden. Diese Vorgehensweise machte das Arbeiten mit dem AMAC etwas umständlich, insbesondere, wenn als drittes Programm dann noch ein Debugger hinzu kommt. War man aber auf Macro angewiesen, so kam man am AMAC nicht vorbei.  
  
Obschon der AMAC von ATARI Elektronik Vertriebsgesellschaft GmbH in Deutschland verkauft wurde, waren sowohl er, als auch der [Programm_Text_Editor](../Programm_Text_Editor/index.md) in englischer Sprache! Lediglich das Konfigurationsprogramm für den [Programm_Text_Editor](../Programm_Text_Editor/index.md) war in deutscher Sprache als Basic-Programm verfügbar. Es sei daher an dieser Stelle in Frage gestellt, ob es sich hierbei somit wirklich um ein "deutsches" Programmpaket handelt. Dies insbesondere deshalb, weil der AMAC und der [Programm_Text_Editor](../Programm_Text_Editor/index.md) jeweils separat verkauft wurden. In der deutschen Version des AMAC war zwar der [Programm_Text_Editor](../Programm_Text_Editor/index.md) enthalten, jedoch völlig ohne jegliches Konfigurationsprogramm!  
  
Interessant macht das Programm jedoch die Tatsache, dass der AMAC mit einem deutschen DOS ausgeliefert worden ist. Genauer gesagt mit dem "Disk Betriebssystem II Version D2.0S". Das ist heute schwer zu finden. Es hat jedoch keinerlei Vorteile gegenüber der englischen Originalfassung. Ferner liegt der Diskette eine Datei namens "SYSTEXT" bei, welche wiederum auf der englischen, originalen Diskette fehlte! In der Datei: "SYSTEXT" sind die "Operating System Equates" und "Hardware Registers" als Mnemonics mit ihren hexadezimalen Entsprechungen enthalten. Das macht das Arbeiten mit dem AMAC einfacher und spart Zeit. Ganz besonders soll jedoch das Handbuch in deutscher Sprache hervorgehoben werden, das immerhin einen Umfang von 50 Seiten hat. Damals wurden alle Seiten in rot-schwarz von Atari Deutschland verkauft, um das Fotokopieren nahezu unmöglich zu machen. Mit den heute zur Verfügung stehenden Werkzeugen, z. B. Photoshop, kann man jedoch die rot gefärbten Seiten digital nach weiß färben und somit das Handbuch normal lesbar machen. Eine Anleitung dazu ist mit der deutschen Photoshop-Version CS4 in Form eines Clips [hier](../Convert_red_pages_from_manuals_into_white_pages/index.md) erstellt worden. Die Technik lässt sich auf modernere Versionen sinngemäß übertragen. Ferner war AtariWiki sich auch nicht zu schade, bei einem derartigen Umfang des Handbuchs, OCR zum Einsatz zu bringen.  
  
Ferner gibt es vom AMAC noch verschiedene Versionen, daher stellt AtariWiki nunmehr eine AMAC ultimate Fassung als ATR-Image zur Verfügung, in der alle Versionen, der Editor, das deutsche Konfigurationsgrogramm und die Datei: "SYSTEXT" enthalten sind. Somit fehlt dann nur noch ein Debugger. Hier ergeht die Empfehlung klar für den [BUG/65](../Bug65/index.md) bzw. für [AMOEBA](../AMOEBA/index.md). AMOEBA wurde erst 2017 durch Zufall entdeckt und passt nicht nur optisch in diese Reihe, sondern auch zeitlich. AMOEBA wurde ebenfalls von einer Frau, Amy Chen, programmiert. Auch diese Tatsache kam erst 2017 an die Öffentlichkeit.  
  
## CAMAC  
```
**** Atari S/W Development HCD1 / BATCH OUTPUT FILE ****

AOS/VS  3.07 / EXEC  3.07	19-JAN-84	10:11:01	
QPRI=254	SEQ=31324
INPUT FILE -- :UDD:SYSTEMS:850:?031.CLI.004.JOB (WILL BE DELETED AFTER PROCESSING)
LIST FILE  -- :QUEUE:NORDIN.LIST.31324

--------
LAST MESSAGE CHANGE	12-JAN-84	16:06:08

		Atari S/W Development System HCD1

Backup schedule (system shut down): Saturday  21-Jan-84  9:30-11:30am

Refer to HELP *COMMANDS, HELP *PSEUDO, HELP, APHELP, and ?MHELP.

Refer to DISP FUNC in SED for list of default function key commands.

--------
LAST PREVIOUS LOGON	19-JAN-84	10:09:45
* searchlist :UDD:NORDIN:UTIL :UDD:NORDIN:LINKS :C :UTIL :

AOS/VS CLI   REV 03.03.00.00	19-JAN-84	10:11:05
Ý SEARCHLIST :UDD:SYSTEMS:UTIL,:UDD:NORDIN:UTIL,:UDD:NORDIN:LINKS,:C,:UTIL,:
Ý DIRECTORY :UDD:SYSTEMS:850
Ý DEFACL SYSTEMS,OWARE,A.JOE,OWARE,A.OLIVIA,OWARE,ARKEN,OWARE,BLOTCKY,OWARE,NORDIN,OWARE,TITTSLER,OWARE,FOWKES,OWARE
Ý CAMAC R850AMAC H=R850AMAC.OBJ L=R850AMAC.PRN R=F SL=132 


ATARI CAMAC Assembler Ver  1.0A
Copyright 1981 ATARI Inc.

Enter source file name and options

d:R850AMAC  h=d:R850AMAC.OBJ l=d:R850AMAC.PRN R=F SL=132           

  Pass 1 - Reading D1:R850AMAC.   
  Pass 2 - Reading D1:R850AMAC.   

  no ERRORs,  669 Labels, $67E8 free.
�

ATARI CAMAC Assembler Ver  1.0A
Copyright 1981 ATARI Inc.

Enter source file name and options



Ý 
Ý 
END OF FILE
AOS/VS CLI   TERMINATING	19-JAN-84	10:12:06

PROCESS 42 TERMINATED 
ELAPSED TIME  0:01:06
(OTHER JOBS, SAME USERNAME)
USER 'NORDIN' LOGGED OFF 	19-JAN-84	10:12:07


****
* LIST FILE EMPTY, WILL NOT BE PRINTED
****
```
  
## ATR-Images  
- [Atari_Macro_Assembler_DXG_8126-Original.atr](attachments/Atari_Macro_Assembler_DXG_8126-Original.atr) ; originale, deutsche SD-Diskette mit deutschem DOS II D2.0S ; das Original wurde ohne Kopierschutz ausgeliefert, s.u., mit dem Programm Text Editor aber __ohne__ dem dazugehörigen Konfigurationsprogramm (Basic)!  
- [Atari_Macro_Assembler_DXG_8126-ohne_Schutz-ultimativ.atr](attachments/Atari_Macro_Assembler_DXG_8126-ohne_Schutz-ultimativ.atr) ; ultimative MD-Diskette mit deutschem DOS II 2.5 ; ohne Kopierschutz ; mit AMAC Version A, C, D ; mit Programm Text Editor sowie dem dazugehörigen Konfigurationsprogramm in deutsch (Basic) ; mit Datei: "SYSTEXT" ; mit AMOEBA ; mit BUG/65 Version 2.0 relozierbar ; mit BUG/65 Version 2.0 nicht relozierbar und Startadresse: $9C00 ; mit BUG/65 Patch für DOS 4 (Basic) ; mit Datei: AUTORUN.SYS bzw. COLOR.OBJ zum Anpassen der Farbe  
  
## Handbücher  
- [ATARI Macro Assembler (AMAC) DXG 8126 Handbuch (deutsch)](attachments/Atari_Macro_Assemble__DXG_8126-OCR.pdf) ; Größe: 7,4 MB ; mit Texterkennung OCR (deutsch)  
- [SYSTEXT.txt](attachments/SYSTEXT.txt) ; Ausdruck der "Operating System Equates" und "Hardware Registers" als Mnemonics mit ihren hexadezimalen Entsprechungen in einer Text-Datei  (englisch)  
  
- [Atari_Macro_Assembler_and_Program-Text_Editor.pdf](attachments/Atari_Macro_Assembler_and_Program-Text_Editor.pdf) ; Größe: 12,4 MB ; Hanbuch für den Assembler und Editor (englisch)  
- [Atari_Macro_Assembler.pdf](attachments/Atari_Macro_Assembler.pdf) ; Größe: 10,2 MB ; Hanbuch für den Assembler (englisch)  
- [Atari_Program_Text_Editor.pdf](attachments/Atari_Program_Text_Editor.pdf) ; Größe: 10,4 MB ; Hanbuch für den Editor (englisch)  
- [Atari_Macro_Assembler_Product_Information_Sheet_II.pdf](attachments/Atari_Macro_Assembler_Product_Information_Sheet_II.pdf) ; Größe: 1,6 MB ; Informationsblatt II zum ATARI Macro Assembler (AMAC) vom 14.06.1983 (englisch)  
- [Atari Macro Assembler Reference Card-OCR](attachments/Atari_Macro_Assembler_Reference_Card-OCR.pdf)  
- [Atari Program-Text Editor Reference Card-OCR](attachments/Atari_Program-Text_Editor_Reference_Card-OCR.pdf)  
  
## Manual online  
- [The AMAC Atari Macro Assembler](http://www.mixinc.net/atari/amac.htm) englisch, von Nick Kennedy, sehr zu empfehlen! :-)))  
  
## Kopierschutz  
Die originale Diskette enthält einen Kopierschutz. Im ersten Sektor des Programms AMAC befindet sich die folgende Zeichenkette:  
  
E2 02 E3 02 __00__ 26  
  
ersetzt man diese durch die nachfolgende Zeichenkette:  
  
E2 02 E3 02 __26__ 26  
  
so wird der Kopierschutz umgangen und AMAC kann verwendet werden.  
  
Konkret sieht das so aus:  
![](attachments/AMAC_%28original%2Cprotected%29-Protection-Code-EN.png)  
Atari Macro Assembler Diskette (englisch, vom Original) - Quelltext des Kopierschutzes für den AMAC (ist im 1. Sektor des Programms auf der Diskette zu finden). Der Schutz ist genau genommen gar keiner. Er war scheinbar ursprünglich darauf ausgelegt, auf einen defekten Sektor zu prüfen. Wie es aussieht wurde dann vor der Auslieferung entschieden dies doch nicht zu tun. Vermutlich weil es bei einem DOS Programm keinen Sinn hat, auf bestimmte Sektoren zu prüfen. Um das Programm nicht ganz neu assemblieren zu müssen, wurde der Code so angepasst, dass auf Sektor 0 gelesen wird. Diesen gibt es nicht und die Logik verhält sich so, als hätte sie den defekten Sektor gefunden.  
  
![](attachments/AMAC_%28original%2Cunprotected%29-Protection-Code-DE.png)  
Atari Macro Assembler Diskette (deutsch, vom Original) - der Quelltext des Kopierschutzes für den AMAC wurde entfernt, s. Bild oben, stattdessen wurden NOP-Befehle eingesetzt sowie Befehle zur Änderung der Farbe und des Hintergrundes, s. Bild weiter unten. Vielen lieben Dank an JAC! von AtariAge für die Analyse.  
  
## Film  
- [Atari_Macro_Assembler.mp4](attachments/Atari_Macro_Assembler.mp4) ; Beispielfilm für die Anwendung des Atari Macro Assemblers  
  
## Bilder  
![](attachments/Atari_CAMAC_Assembler_Ver_1.0A.jpg)  
Atari CAMAC Assembler Ver 1.0A - Ausdruck eines Assemblerprogramms von Harry B. Stewart in der Atari Zentrale in Sunnyvale  
  
![](attachments/Macro_Assembler_a.jpg)  
ATARI Macro Assembler (AMAC) DXG 8126 - Boxvorderseite  
  
![](attachments/Macro_Assembler_b.jpg)  
ATARI Macro Assembler (AMAC) DXG 8126 - Boxrückseite  
  
![](attachments/Diskette8126.jpg)  
ATARI Macro Assembler (AMAC) DXG 8126 - Diskette  
  
![](attachments/ATARI_Macro_Assembler_Ver_1.0A.jpg)  
ATARI Macro Assembler (AMAC) DXG 8126 - Startbildschirm der deutschen Version mit deaktiviertem Schutz und anderer Farbe als das US-Original  
  
![](attachments/ATARI_Macro_Assembler_Ver_1.0A-ohne_Schutz.jpg)  
ATARI Macro Assembler (AMAC) DXG 8126 - Startbildschirm der US-Version mit deaktiviertem Schutz  
  
![](attachments/Program-Text_Edior_Version_1.0.jpg)  
ATARI Macro Assembler (AMAC) DXG 8126 - Program-Text Editor Startbildschirm  
  
![](attachments/AMOEBA_Version_3.0.jpg)  
AMOEBA Version 3.0 - Startbildschirm  
  
![](attachments/BUG-65_Version_2.0.jpg)  
BUG/65 Version 2.0 - Startbildschirm  
  
## Reference Cards  
![](attachments/Atari_Program-Text_Editor_Reference_Card.jpg)  
Atari Program-Text Editor - Reference Card  
  
![](attachments/Atari_Macro_Assembler_Reference_Card.jpg)  
Atari Macro Assembler - Reference Card  
  
## Danksagung  
AtariWiki bedankt sich ganz herzlich bei Dirk Tröger! :-) Hätte er diese Software nicht gerettet, wäre sie wohl für immer verloren gegangen. Mega-Danke Dirk!!! :-)))  
