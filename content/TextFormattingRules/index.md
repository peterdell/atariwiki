---
title: TextFormattingRules
---
```
----       = make a horizontal ruler. Extra '-' is ignored.
\\         = force a line break

[link]     = create a hyperlink to an internal WikiPage called 'Link'.
[this is also a link] = create a hyperlink to an internal WikiPage called
             'ThisIsAlsoALink' but show the link as typed with spaces.
[a sample|link] = create a hyperlink to an internal WikiPage called
             'Link', but display the text 'a sample' to the
             user instead of 'Link'.
[link#headline] = create a hyperlink to an internal WikiPage called 'link' and use anchor 'headline'          
~NoLink    = disable link creation for the word in CamelCase.
[1]        = make a reference to a footnote numbered 1.
[#1]       = mark the footnote number 1.
[[link]     = create text '[link]'.

!heading   = small heading with text 'heading'
!!heading  = medium heading with text 'heading'
!!!heading = large heading with text 'heading'

''text''   = print 'text' in italic.
__text__   = print 'text' in bold.
{{text}}   = print 'text' in monospaced font.
[ text|]    = print 'text' underscored (dummy hyperlink)
* text     = make a bulleted list item with 'text'
# text     = make a numbered list item with 'text'
;term:ex   = make a definition for 'term' with the explanation 'ex'

```
  
### Hier ist eine kurze Zusammenfassung der zur Verfügung stehenden Formatierungen  
```
so siehts aus:
----
{{{\\                  Erzwungener Zeilenumbruch
Bsp: Text\\Text}}}
Text\\Text
{{{
[link]              Erzeugt einen Hyperlink zu "link", wobei "link" 
                    sowohl ein interner WikiName 
                    oder ein externer Link (http://) sein kann.
Bsp.: [Main]
```
[Main](../Main/index.md)  
```
[text|link]         Erzeugt einen Hyperlink, wobei der angezeigte Text 
                    und der Link unterschiedlich sind.
Bsp.: [Hauptseite|Main]
```
[Hauptseite](../Main/index.md)  
```
[link#headline]     Erzeugt einen Hyperlink und nutzt eine Überschrift als Anker.
```
[linkheadline](../linkheadline/index.md)  
  
```
[text|wiki:link]    Erzeugt einen Hyperlink, wobei der angezeigte Text 
                    und der Link unterschiedlich sind und der Hyperlink
                    zu einem anderen Wiki zeigt. Dies unterstützt 
                    interWiki Linking.
```
Derzeit ist kein verlinktes Wiki definiert...  
```
*                   Aufzählungszeichen Punkte (Der Stern muss in der 
                    Zeile an erster Stelle stehen. 
                    Benutze mehrere Sterne (**) um einen tieferen Einzug 
                    zu erzeugen.
Bsp.:
*Erste Ebene
*Zweiter Punkt
**Zweite Ebene
***Dritte Ebene
```
*Erste Ebene  
*Zweiter Punkt  
**Zweite Ebene  
***Dritte Ebene  
```
#                   Aufzählungszeichen Nummerierung 
                    (muss als erstes Zeichen einer Zeile stehen). 
                    Benutze mehrere Zeichen (##, ###) für einen tieferen Einzug.
Bsp.:
#Erste Ebene
#Zweiter Punkt
##Zweite Ebene
###Dritte Ebene
```
#Erste Ebene  
#Zweiter Punkt  
##Zweite Ebene  
###Dritte Ebene  
```
!, !!, !!!          Ausrufezeichen zu Beginn einer Zeile machen diese 
                    zur Überschrift.
                    Je mehr Ausrufezeichen, desto grösser die Überschrift.
Bsp.:
!Überschrift 1
!!Überschrift 2
!!!Überschrift 3
```
### Überschrift 1  
## Überschrift 2  
# Überschrift 3  
  
```
Bsp.: __Fetter__ Text}}}
__Fetter__ Text
{{{
''text''            formatiert Text kursiv (beachte, dass es jeweils zwei
                    aufeinander folgende Zeichen sind ('))
Bsp.: ''kursiver'' Text
```
''kursiver'' Text  
```
{{text}}            formatiert Text mit nicht proportionaler Schrift.
Bsp.: {{Formatierter}} Text
```
{{Formatierter}} Text  
```
;term:def           Erklärt 'term' mit 'def'. Benutze dies mit leerem  
                    'term', um Kurzkommentare anzubringen.
Bsp.: ;Ausdruck:Erklärung
```
;Ausdruck:Erklärung  
```
||ÜSp1||ÜSp2        Erzeugt eine Tabelle. Doppelte Balken für eine 
|text1|text2        Tabellenüberschrift.
```
||ÜSp1||ÜSp2  
|text1|text2  
  
  
  
HTML funktioniert __''nicht''__.  
  
Um einen Codeblock darzustellen, setzt du diesen zu Beginn in dreifach geschweifte Klammern '{' und am Ende '}'.  
  
Falls eckige Klammern ({{\[\]}}) in einer Seite erforderlich sind, ohne einen Link erzeugen zu wollen, müssen zwei einleitende klammern gesetzt werden. Der Text {{\[[Beispiel Kein Link\]}} erscheint als {{\[Beispiel Kein Link\]}}.  
  
