---
title: How to create new pages in the Atari Wiki
---
# How to create new pages in the Atari Wiki  
__ First, you need an account on the AtariWiki__  
  
__Still a working place, please stand by for more info in the future__  
  
Many tools are collected in this rtf file: [AtariWiki-Tools.rtf](attachments/AtariWiki-Tools.rtf)  
  
  
- [TextFormattingRules](../TextFormattingRules/index.md)  
  
  
![](attachments/Atari_Calculator.jpg)  
Calculator after a little calculation   
  
  
```
ORG+$068B LDX #36
          LDY #E4
          JMP 2777
```
  
- [Atari XF551](http://www.strotmann.de/~cas/Infothek/XF551formate/XF551Formate.pdf)  
  
# Wiki site  
  
%%tabbedSection  
%%tab-English  
by ...  
  
  
## Introduction  
  
  
/%  
%%tab-deutsch  
  
## Einleitung  
  
  
  
/%  
%%tab-français  
  
## Introduction  
  
  
/%  
%%tab-español  
  
## Introducción  
  
  
/%  
%%tab-italiano  
  
## Introduzione  
  
  
/%  
%%tab-Nederlands  
  
## Introductie  
  
  
/%  
%%tab-polski  
  
## Przedmowa  
  
  
/%  
%%tab-český  
  
## Zavedení  
  
  
/%  
/%  
  
  
  
### 1) Auszeichnung (Formatierung) im Wiki sollte immer nach semantischen Kriterien erfolgen, d.h. danach *was* etwas ist (Ueberschrift,  
Quelltext, Link) und nicht danach *wie* etwas am Bildschirm dargestellt wird (Fett, Kursiv etc). Die Darstellung richtet sich nach der *Art* der  
Information. Wenn die Darstellung verbessert werden kann, dann koennen wir das Stylesheet des Wiki anpassen  
  
### 2) ein Ziel des Wikis ist Informationen schnell findbar zu machen.  
Dazu zählt, die Informationen so aufzubereiten das Suchmaschinen die Daten gut finden koennen (Google, Bing, DuckDuckGo, Suchfunktion im Wiki ...).  
Umdas moeglich zu machen, sollten Inhalte moeglichst als Text-Artikel im Wiki erscheinen, weniger als Anhang.  
  
Beispiele:  
  
 * ein MAC65 Programm lieber als Listing im Artikel anstatt als M65-Datei in Anhang  
 * ein Basic Programm lieber als LST im Artikel als BAS-Datei im Anhang  
 * Lieber eine TXT-Datei als eine DOC/PDF-Datei  
 * ZIP, RAR, TAR-Archive auspacken und die einzelnen Dateien in den  
Anhang anstatt das ganze Archiv, Texte aus dem Archiv als Wiki-Artikel aufbereiten  
  
  
## Skript-Beispiele:  
  
  
|  
  
data.atariwiki.org/DATA  
  
data.atariwiki.org/FLAC  
  
data.atariwiki.org/MOVIE  
  
  
---
         = force a line break  
  
[link](../link/index.md)     = create a hyperlink to an internal WikiPage called 'Link'.  
[this_is_also_a_link](../this_is_also_a_link/index.md) = create a hyperlink to an internal WikiPage called  
'ThisIsAlsoALink' but show the link as typed with spaces.  
[a sample](../link/index.md) = create a hyperlink to an internal WikiPage called  
'Link', but display the text 'a sample' to the  
user instead of 'Link'.  
[linkheadline](../linkheadline/index.md) = create a hyperlink to an internal WikiPage called 'link' and use anchor 'headline'  
~NoLink    = disable link creation for the word in CamelCase.  
[1](../1/index.md)        = make a reference to a bartnote numbered 1.  
[1](../1/index.md)       = mark the bartnote number 1.  
\[link\]     = create text '[link](../link/index.md)'.  
  
### heading   = small heading with text 'heading'  
## heading  = medium heading with text 'heading'  
# heading = large heading with text 'heading'  
  
''text''   = print 'text' in italic.  
__text__   = print 'text' in bold.  
{{text}}   = print 'text' in monospaced font.  
[text](..//index.md)    = print 'text' underscored (dummy hyperlink)  
- text     = make a bulleted list item with 'text'  
1. text     = make a numbered list item with 'text'  
;term:ex   = make a definition for 'term' with the explanation 'ex'  
  
Hier ist eine kurze Zusammenfassung der zur Verfügung stehenden Formatierungen#  
---
so siehts aus:  
  
                  Erzwungener Zeilenumbruch  
Bsp: TextText  
Text  
Text  
[link](../link/index.md)              Erzeugt einen Hyperlink zu "link", wobei "link"  
sowohl ein interner WikiName  
oder ein externer Link (http://) sein kann.  
Bsp.: [Main](../Main/index.md)  
Main  
[text](../link/index.md)         Erzeugt einen Hyperlink, wobei der angezeigte Text  
und der Link unterschiedlich sind.  
Bsp.: [Hauptseite](../Main/index.md)  
Hauptseite  
[linkheadline](../linkheadline/index.md)     Erzeugt einen Hyperlink und nutzt eine Überschrift als Anker.  
link#headline  
[text](../wiki:link/index.md)    Erzeugt einen Hyperlink, wobei der angezeigte Text  
und der Link unterschiedlich sind und der Hyperlink  
zu einem anderen Wiki zeigt. Dies unterstützt  
interWiki Linking.  
Derzeit ist kein verlinktes Wiki definiert...  
- Aufzählungszeichen Punkte (Der Stern muss in der  
Zeile an erster Stelle stehen.  
Benutze mehrere Sterne (**) um einen tieferen Einzug  
zu erzeugen.  
Bsp.:  
*Erste Ebene  
*Zweiter Punkt  
**Zweite Ebene  
***Dritte Ebene  
Erste Ebene  
Zweiter Punkt  
Zweite Ebene  
Dritte Ebene  
1. Aufzählungszeichen Nummerierung  
(muss als erstes Zeichen einer Zeile stehen).  
Benutze mehrere Zeichen (##, ###) für einen tieferen Einzug.  
Bsp.:  
#Erste Ebene  
#Zweiter Punkt  
##Zweite Ebene  
###Dritte Ebene  
Erste Ebene  
Zweiter Punkt  
Zweite Ebene  
Dritte Ebene  
### , !!, !!!          Ausrufezeichen zu Beginn einer Zeile machen diese  
zur Überschrift.  
Je mehr Ausrufezeichen, desto grösser die Überschrift.  
Bsp.:  
### Überschrift 1  
## Überschrift 2  
# Überschrift 3  
Überschrift 1#  
Überschrift 2#  
  
Überschrift 3#  
__text__            formatiert Text fett.  
Bsp.: __Fetter__ Text  
Fetter Text  
''text''            formatiert Text kursiv (beachte, dass es jeweils zwei  
aufeinander folgende Zeichen sind ('))  
Bsp.: ''kursiver'' Text  
kursiver Text  
{{text}}            formatiert Text mit nicht proportionaler Schrift.  
Bsp.: {{Formatierter}} Text  
Formatierter Text  
;term:def           Erklärt 'term' mit 'def'. Benutze dies mit leerem  
'term', um Kurzkommentare anzubringen.  
Bsp.: ;Ausdruck:Erklärung  
Ausdruck  
Erklärung  
||ÜSp1||ÜSp2        Erzeugt eine Tabelle. Doppelte Balken für eine  
|text1|text2        Tabellenüberschrift.  
ÜSp1  
ÜSp2  
text1  
text2  
  
HTML funktioniert nicht.  
Um einen Codeblock darzustellen, setzt du diesen zu Beginn in dreifach geschweifte Klammern '{' und am Ende '}'.  
Falls eckige Klammern ([]) in einer Seite erforderlich sind, ohne einen Link erzeugen zu wollen, müssen zwei einleitende klammern gesetzt werden. Der Text \[Beispiel Kein Link\] erscheint als [Beispiel_Kein_Link](../Beispiel_Kein_Link/index.md).  
  
  
### BIN-Image  
- [Atari_Assembler_Editor.bin](attachments/Atari_Assembler_Editor.bin)  
  
  
  
  
### CAR-Image  
- [Assembler_Editor.car](attachments/Assembler_Editor.car)  
  
### Manual online  
- [Mac/65 Manual](http://www.mixinc.net/atari/mac65.htm) by Nick Kennedy (highly recommended!)  
  
  
### Pictures  
![](attachments/Assembler+Editor+Brown+front.jpg)  
Assembler Editor Cartridge  
  
  
![](attachments/Atari_Calculator4.jpg)  
Calculator after a little calculation   
  
  
![](attachments/img.jpg)  
  
  
  
  
  
  
[c65-front.png](attachments/c65-front.png)  
  
  
  
[linkheadline](../linkheadline/index.md) = create a hyperlink to an internal WikiPage called 'link' and use anchor 'headline'  
  
  
```
ORG+$068B LDX #36
          LDY #E4
          JMP 2777
```
  
  
}}}  
  
## RELGEN.ACT  
```
* [Atari XF551|http://www.strotmann.de/~cas/Infothek/XF551formate/XF551Formate.pdf]


* Atari DOS 1 [PDF, 3.2MB|Atari DOS 3/dos 3 handbuch.pdf]



[Software|Articles#section-Articles-Software]

```
