---
title: TURBAN
---
# Turban - TURboBAsic Nifty  
  
  
%%tabbedSection  
%%tab-english  
by Daniel Serpell, Matthias Reichl, Christian Krüger, Sascha Kriegel and Roland B. Wassenberg  
  
## ---(EN) Introduction  
TURBAN - __TUR__bo__BA__sic __N__ifty  
  
The main part of TURBAN was done by Daniel Serpell, dmsc at AtariAge. He is the author of [FastBasic](https://atariwiki.org/wiki/Wiki.jsp?page=FastBasic), too. Highly recommended!  
  
Hias has written [dir2atr](http://www.horus.com/~hias/atari/#tools-win32). Thank you so much Hias for your help, greatly needed here.  
  
The ATR image is bootable and can work with the following DOS versions: Atari DOS 2.0 and 2.5 with 720 and 1040 sectors, MyDos, TurboDos, XDos and MyPicoDos. Thank you so much Matthias Reichl, such a great work, not just for TURBAN.  
  
The script is from Christian Krüger, Irgendwer from AtariAge. Thank you so much Christian, that was a great help for us all!  
  
Sascha Kriegel, skr from AtariAge, has made the port of the script for the Mac and the plug-in for BBEdit for markup the commands. Roland B. Wassenberg, luckybuck from AtariAge, has enhanced the script, so it now runs on all Macs with Sublime Text and BBEdit while wiping-out the nasty invisible files created by macOS and not needed for the Atari.  
  
__So, who is providing us with a tutorial for UltraEdit or Geany?__  
  
__And even more important, who is making a parser for ACTION!, too? - A ten liner contest for ACTION! will be possible then. :-)__  
  
## Tutorial for Windows 10  
Sadly, we could not make yet a translation into English by now. But ggn from AtariAge has made a tutorial and files to make TURBAN running under Windows 10. Thank you so much ggn, that is of great help for the community. Greatly appreciated. Please go ahead.  
  
Quick instructions from ggn:  
"  
1. Unpack the zip file wherever you want (hopefully!) ; please see below for the attached zip file  
2. Open turban.w10npp.7.7 and execute notepad++.exe  
3. Open turban.w10testproject1sample-2.tur or turban.w10testproject2sample-3.tur  
4. Press F7. A dialog will pop up, just press ok. The program will compile and altirra will execute.  
  
A few notes about the package:  
  
- I used Altirra 64bit version. If you have a 32bit version of windows then replace with that version.  
- Prior to executing TURBAN, F7 will also auto save your source so it will compile the most current version.  
- While compiling, a pop up window at the bottom of the screen will show the build progress, so you can see any errors (you can set up the plugin to highlight errors and possibly jump on them by double click, but I did not set this up).  
- Hopefully authors of the software I bundled inside that zip won't be angry about me! If they do, I'll simply remove the zip altogether.  
- The package was hacked in a hurry but then I might have some prior experience :-).  
- If something not working or you need help? Let me know. ; please contact ggn at atariage.com, thank you.  
"  
  
## Tutorial for macOS  
  
Not yet available in English, please try to help yourself with the German version. Sorry, for the inconveniences. When time, the version will be here, too.  
  
## Tutorial for Linux  
  
## ATR images  
- [Characters.atr](attachments/Characters.atr) ; all Atari special characters for use in TURBAN in one file.  
  
## ZIP file  
- [Attachment für TURBAN under Windows 10](attachments/turban.w10.zip) ; size: 8 MB ; thank you so much ggn from AtariAge for your help. The community is in your debt.  
  
## Pictures  
![](attachments/Beispielcode-Basic-Monokai.jpg)  
Code example with theme: 'Basic-Monokai' in Sublime Text 2  
  
![](attachments/Special+Characters+43.jpg)  
43 special characters in the Atari font  
  
![](attachments/Sublime+Text-TURBAN-Special+Characters.jpg)  
Sublime Text - TURBAN special characters  
  
## Recommended editors  
- for Windows and macOS:  
- [Sublime Text](https://www.sublimetext.com/)  
- [UltraEdit](https://www.ultraedit.com/)  
- [Geany](https://www.geany.org/Download/Releases)  
  
- for Windows only:  
- [Notepad++](https://notepad-plus-plus.org/) and [themes](https://www.groovypost.com/howto/notepad-plus-plus-change-font-color/) for the editor  
  
- for macOS only:  
- [BBEdit](https://www.barebones.com/products/bbedit/)  
  
The editor must be sriptable. Plug-ins should be possible, too.  
  
/%  
%%tab-deutsch  
von Daniel Serpell, Matthias Reichl, Christian Krüger, Sascha Kriegel und Roland B. Wassenberg  
  
## ---(DE) Einleitung  
TURBAN - __TUR__bo__BA__sic __N__ifty  
  
TURboBAsic Nifty (TURBAN) würde man ins Deutsche als TURBO-BASIC XL elegant übersetzen. Was hat es damit auf sich? Kurz und knapp erklärt handelt es sich hierbei um das bekannte TURBO-BASIC XL, nur eben mit der Technik des 21. Jahrhunderts. Dazu waren mehrere Autoren erforderlich, da es sich um die gemeinsame Anwendung verschiedener Programme zu einem funktionierenden Ganzen handelt. Es sind immer wieder diese Gemeinschaftsproduktionen, die Atari sowie die Gemeinschaft so stark machen und die Freude am Hobby so lange erhalten. Man sagt, ein Bild sagt mehr als tausend Worte:  
  
![](attachments/Beispielcode-Basic-Monokai.jpg)  
Beispielcode mit dem Farbschema: Basic-Monokai in Sublime Text 2  
  
Im vorstehenden Bild ist ein Quelltext von TURBO-BASIC XL im Editor "Sublime Text 2" dargestellt. Hierbei wurde das Farbschema "Basic-Monokai" verwendet, um die verschiedenen Parameter entsprechend hervorzuheben. Die Programme werden nämlich nicht, wie gewohnt im Atari BASIC- oder TURBO-BASIC XL-Editor geschrieben, sondern auf modernen, aktuellen Hochleistungseditoren, wie z. B. die plattformübergreifenden Programme: [Sublime Text](https://www.sublimetext.com/) oder [UltraEdit](https://www.ultraedit.com/). Es gibt auch kostenfreie Editoren wie z. B. [Geany](https://www.geany.org/Download/Releases). Hat man nun den Quelltext eingegeben, drückt man eine Taste und startet somit ein Skript, dass das Programm in Atari BASIC oder TURBO-BASIC XL blitzschnell übersetzt, als Datei für den Atari erzeugt, auf ein ATR-Image schreibt, um anschließend vom Emulator nach Wunsch geöffnet und automatisch gestartet werden zu können! Hat man hierbei einen Fehler gemacht, gibt es eine Rückmeldung in welcher Zeile des Quelltextes das passierte (1. Spalte im Bild oben, die grauen Zahlen). In der 2. Spalte sind die eigentlichen Zeilennummerierungen des BASIC-Programms zu sehen. Schön zu sehen sind die farblichen Unterscheidungen sowie das Einrücken von Schleifen. Das Kopieren und Einfügen geht selbstverständlich auch sehr elegant mit den modernen Editoren. Nachstehend werden einige Editoren vorgestellt:  
  
- für Windows und macOS:  
- [Sublime Text](https://www.sublimetext.com/)  
- [UltraEdit](https://www.ultraedit.com/)  
- [Geany](https://www.geany.org/Download/Releases)  
  
- für Windows zusätzlich:  
- [Notepad++](https://notepad-plus-plus.org/)  
  
- für macOS zusätzlich:  
- [BBEdit](https://www.barebones.com/products/bbedit/)  
  
Wichtig ist, dass der Editor skriptfähig ist und idealerweise durch Erweiterungen, sogenannte Plug-ins, an die Bedürfnisse angepasst werden kann. Dazu gehören z. B. alle Befehle aller Programmiersprachen. Es gibt sogar ein FORTH-Plug-in! Die oben stehenden Links führen dazu Beispiele an.  
  
Den Löwenanteil von TURBAN steuerte Daniel Serpell bei, auch als dmsc auf AtariAge bekannt. Daniel ist übrigens auch der Autor von [FastBasic](https://atariwiki.org/wiki/Wiki.jsp?page=FastBasic). Hierbei darf „fast“ ruhig wörtlich verstanden werden! Ich empfehle jedem Atari User, sich seine Arbeit einmal anzusehen. Ganz große Leistung!  
  
Daniel hat im Rahmen von TURBAN den sogenannten Parser entwickelt. Er übersetzt den Text in das vom Atari einlesbare Format. Bislang kam sein Programm hauptsächlich für den 10-Zeilen Wettbewerb zum Einsatz. Er hat jedoch eine Anpassung vorgenommen, die es dem Team zur Erhaltung von Abtipp-Listings gestattet, sein Werk auch dort einzusetzen. Daher noch einmal ein großes Dankeschön an Daniel! :-) Seine aktuelle Version mit allen Möglichkeiten ist [hier](https://github.com/dmsc/tbxl-parser) beschrieben, die aktuellen Programme für alle Plattformen findet man [hier](https://github.com/dmsc/tbxl-parser/releases).  
  
Hat nun der Parser die Datei: „AUTORUN.BAS“ fehlerfrei erzeugt, wird diese mittels der Software von Hias: „dir2atr“ auf ein ATR-Image geschrieben, von wo aus sie gestartet werden kann. Die aktuelle Version von dir2atr findet man [hier](http://www.horus.com/~hias/atari/#tools-win32).  
  
Bitte nicht falsch verstehen, es handelt sich hier nicht nur um eine Windows-Version, das Programm wird für alle Plattformen angeboten! Ganz dickes Lob an Hias!  
  
Doch damit nicht genug, das ATR-Image ist natürlich voll bootfähig und beherrscht ferner folgende DOS-Varianten: Atari DOS 2.0 und 2.5 mit 720 sowie 1040 Sektoren, MyDos, TurboDos, XDos und MyPicoDos. Super Arbeit, vielen lieben Dank geht noch einmal an Matthias Reichl.  
  
Nach der Erstellung des ATR-Images übergibt dann das Skript die Datei an einen Emulator nach Wahl. Somit bleibt eigentlich kein Wunsch mehr offen für eine moderne Programmierumgebung.  
  
Das Skript, welches die ganzen Prozesse steuert, hat Christian Krüger, auch als Irgendwer von AtariAge bekannt, für Windows geschrieben. Den aktuellen Stand der Diskussion findet man [hier](http://atariage.com/forums/topic/244686-turban-turbobasic-nifty/). Ferner hat er alle wichtigen Plug-ins für Sublime Text erstellt sowie das Farbschema. Vielen lieben Dank Christian, damit hast Du uns allen sehr geholfen.  
  
Sascha Kriegel, skr auf AtariAge, hat die Portierung des TURBAN-Skriptes für seinen Mac geschrieben und für den Editor BBEdit das Plug-in zur Markierung der Befehle. Darauf aufbauend, hat Roland B. Wassenberg, luckybuck auf AtariAge, das Skript so umgeschrieben, dass es nun für alle Macs einsetzbar ist, mit Sublime Text läuft sowie mit BBEdit. Da BBEdit nicht so smart ist, wie Sublime Text, musste eigens dafür noch ein weiteres Skript geschrieben werden, welches das TURBAN-Skript selber aufruft. An dieser Stelle darf sich der Leser gerne beteiligen und einen entsprechenden Beitrag für UltraEdit oder Geany beisteuern.  
  
Leider ist die Anleitung nur für den Mac und nur für Sublime Text und BBEdit, es würde mich aber freuen, wenn der Leser sich angesprochen fühlt und ggf. weitere Beiträge, insbesondere für Windows, hinzufügen könnte. Insgeheim hoffe ich, dass vielleicht sogar jemand den Parser für ACTION! programmieren könnte. Aber das wird die Zukunft zeigen.  
  
## Anleitung für den PC  
  
Zur Zeit nur im englischen Reiter für Windows 10  
  
## Anleitung für den Mac  
  
## ATR-Images  
- [Characters.atr](attachments/Characters.atr) ; alle Atari Spezialzeichen für den direkten Einsatz in TURBAN in einer Datei.  
  
## Bilder  
![](attachments/Special+Characters+43.jpg)  
43 Spezialzeichen im Atari Zeichensatz  
  
![](attachments/Sublime+Text-TURBAN-Special+Characters.jpg)  
Alle Spezialzeichen in Sublime Text: TURBAN Spezialzeichen  
  
/%  
%%tab-français  
  
/%  
%%tab-espagnol  
  
/%  
%%tab-italiano  
  
/%  
%%tab-Nederlands  
  
/%  
%%tab-Polska  
  
/%  
%%tab-Czech  
  
/%  
/%  
  
