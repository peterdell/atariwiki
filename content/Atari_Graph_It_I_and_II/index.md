# Atari Graph It I & II CX4109 (englisch) bzw. TXG9517 (deutsch), Copyright (C) 1980 - 1983 by:Atari, Inc.; Lane Winner; Howard D. Siebenrock und Atari Elektronik-Vertriebsgesellschaft mbH  
  
Graph It ist ein Basic-Programm zur grafischen Darstellung von Zahlen von 1980. Im Wesentlichen setzt das Programm dort an, wo heutzutage der Diagramm-Assistent in Excel verwendet wird.  
  
In Graph It können Balkendiagramme, Kreisdiagramme, Polardiagramme, 2D-Diagramme und 3D-Diagramme dargestellt werden. Beispiele hierzu finden sich weiter unten auf der Seite.  
  
Da das Programm in Basic geschrieben worden ist, darf der Leser sich ruhig angesprochen fühlen, es in seinen Funktionen zu erweitern. Ein Anfang ist ja gemacht. ;-)  
  
Das Handbuch in elektronischer Form (PDF-Datei, s. u.) entspricht dem originalen Handbuch, jedoch wurden alle bekannten Fehler beseitigt sowie Formeln ergänzt bzw. richtig gestellt. Ferner sind jeweils im Inhaltsverzeichnis, als auch am Seitenrand Hyperlinks gesetzt.  
  
Erst in 2017 konnten die folgenden Entdeckungen gemacht werden und in die Seite eingearbeitet werden:  
  
- Die 1. Version erschien 1980 von Atari und wurde von Lane Winner programmiert. Alle Programme mussten mit einem Vorprogramm von Kassette geladen werden  
- Eine [2. Version](../Enhancements_to_Graph_It/index.md) erschien 1982 zuerst unter dem Label APX-20074, indem Howard D. Siebenrock die bestehende 1. Version wesentlich erweiterte.  
- Eine 3. Version erschien 1983 von Atari in Deutschland, indem Code der 2. Version von Howard D. Siebenrock in die 1. Version eingebaut wurde und abschließend offiziell von Atari Elektronik-Vertriebsgesellschaft mbH als Graph It II verkauft wurde. Interessant ist hierbei, dass auf dem Box-Cover lediglich Graph It zu lesen ist, jedoch das Handbuch, als auch die Kassetten das Label "Graph It II" tragen. Bei dieser Version wurde jeweils auf das Vorprogramm beim Laden von Kassette verzichtet, siehe Boxcover 2 im Kapitel Bilder weiter unten. Ferner wurde auch die ursprüngliche Reihenfolge der Programme auf den Kassetten geändert, s. Bilder weiter unten.  
  
Nach derzeitigem Stand sieht es so aus, als ob Atari bei allen Kassettenprogrammen, welche ein derartiges Cover hatten, gänzlich auf ein Vorladeprogramm verzichtet hat.  
  
## Kurzübersicht zu Graph It:  
  
### a) Balkendiagramme:  
- Die Beschreibung des Diagramms darf maximal 20 Zeichen lang sein.  
- Es sind maximal 32 Spalten darstellbar.  
- Jeder Balken kann in bis zu 3 Unterteilungen dargestellt werden.  
- Die jeweilige Balkenbezeichnung darf maximal 3 Zeichen betragen.  
- Die letzt Eingabe muss mit Drücken der Start-Taste abgeschlossen werden.  
- Die Darstellung der Ordinate (y-Achse) ist stets wissenschaftlich und wird immer mit "E" angezeigt.  
- Die Darstellung der Abszisse (x-Achse) wird hingegen linear wiedergegeben.  
  
### b) Kreisdiagramme:  
- Kreisdiagramme dürfen maximal 12 Teile (Segmente) enthalten.  
- Die Beschreibung des Diagramms (oben) bzw. des Untertitels (unten) darf maximal 20 Zeichen lang sein.  
- Die Bezeichnung eines Teiles (Segmentes) darf maximal 3 Zeichen lang sein.  
- Sofern ein Kreissegment weniger als 1/14 des Gesamtkreises einnimmt, wird dieser Teil als "ETC." dargestellt.  
- Bei vorliegenden Daten können die Prozentanteile der Segmente jeweils automatisch ermittelt werden.  
  
### c) Parametrische Polar-Diagramme:  
  
- Benötigt wird der Start- und Endwert von Winkel sowie Radius.  
- Optional kann eine Autoskalierung erfolgen.  
  
### d) 2D-Diagramme:  
  
- Es können maximal 3 Plots, Kurven, etc. gleichzeitig dargestellt werden.  
- Vier verschiedene Plotgeschwindigkeiten sind verfügbar.  
- Unabhängig davon lässt sich die Plotgeschwindigkeit erhöhen, indem man in den Gleichungen statt: x^2 einfach x*x verwendet.  
- Optional ist eine automatische Skalierung der Ordinate (y-Achse) möglich.  
  
### e) 3D-Diagramme:  
  
- Zwei verschiedene Plotgeschwindigkeiten sind verfügbar.  
- Optional können verborgene Linien entfernt werden.  
  
  
Für a) bis e) einschließlich gilt:  
  
- Eine nachträgliche Änderung von Grenzwerten ist durch Antippen der Leertaste beim fertigen Diagramm möglich.  
- Es können nur Funktionen verwendet werden, die in Atari Basic definiert sind bzw. sich als Kombinationen daraus ergeben. Dies stellt jedoch keinen Nachteil dar, schließlich lassen sich alle Funktionen auf Grundfunktionen zurückführen.  
- Die Verwendung der Autoskalierung bedingt die Erzeugung wenigerer Plotpunkte als bei manueller Festlegung.  
- Mit 16K RAM muss das jeweilige Programm neu geladen werden, mit mehr als 16K RAM ist das nicht erforderlich.  
- Die Kassettenversion benötigt 16K RAM, die Diskettenversion 24K RAM.  
  
Für c) bis e) einschließlich gilt:  
  
- Mit dem Joystick kann man sich x-, y- und z-Werte anzeigen lassen sowie die Steigung bzw. den Winkel Theta (T) bei Polar-Diagrammen.  
  
## CAS-Images:  
  
(englisch):  
- [Atari_Graph_It_CX4109_tape_A_side_1.cas](attachments/Atari_Graph_It_CX4109_tape_A_side_1.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
- [Atari_Graph_It_CX4109_tape_A_side_2.cas](attachments/Atari_Graph_It_CX4109_tape_A_side_2.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
- [Atari_Graph_It_CX4109_tape_B_side_1.cas](attachments/Atari_Graph_It_CX4109_tape_B_side_1.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
- [Atari_Graph_It_CX4109_tape_B_side_2.cas](attachments/Atari_Graph_It_CX4109_tape_B_side_2.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
  
(deutsch):  
- [Atari_Graph_It_CX4109_Band_A_Seite_1.cas](attachments/Atari_Graph_It_CX4109_Band_A_Seite_1.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
- [Atari_Graph_It_CX4109_Band_A_Seite_2.cas](attachments/Atari_Graph_It_CX4109_Band_A_Seite_2.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
- [Atari_Graph_It_CX4109_Band_B_Seite_1.cas](attachments/Atari_Graph_It_CX4109_Band_B_Seite_1.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
- [Atari_Graph_It_CX4109_Band_B_Seite_2.cas](attachments/Atari_Graph_It_CX4109_Band_B_Seite_2.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
  
(deutsch):  
- [Graph_It_II_TXG_9517_Kassette_A_Seite_1.cas](attachments/Graph_It_II_TXG_9517_Kassette_A_Seite_1.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
- [Graph_It_II_TXG_9517_Kassette_A_Seite_2.cas](attachments/Graph_It_II_TXG_9517_Kassette_A_Seite_2.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
- [Graph_It_II_TXG_9517_Kassette_B_Seite_1.cas](attachments/Graph_It_II_TXG_9517_Kassette_B_Seite_1.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
- [Graph_It_II_TXG_9517_Kassette_B_Seite_2.cas](attachments/Graph_It_II_TXG_9517_Kassette_B_Seite_2.cas) ; bitte mit BASIC-Modul starten, dann den Befehl "CLOAD" eingeben und 2 x RETURN drücken  
  
## ATR-Images:  
Atari Graph It CX4109 (englisch, 1980) alle Kassetten-Images auf einem Disk-Image __ohne__ Vorprogramm: [Atari_Graph_It_CX4109_Basic.atr](attachments/Atari_Graph_It_CX4109_Basic.atr)  
Atari Graph It CX4109 (englisch, 1980) alle Kassetten-Images auf einem Disk-Image __mit__ Vorprogramm: [Atari_Graph_It_CX4109_Basic_Complete_Cassette_Import.atr](attachments/Atari_Graph_It_CX4109_Basic_Complete_Cassette_Import.atr)  
  
Atari Graph It TXG9517 (deutsch, 1980) alle Kassetten-Images auf einem Disk-Image __ohne__ Vorprogramm: [Atari_Graph_It_TXG9517_deutsch_Basic.atr](attachments/Atari_Graph_It_TXG9517_deutsch_Basic.atr)  
Atari Graph It TXG9517 (deutsch, 1980) alle Kassetten-Images auf einem Disk-Image __mit__ Vorprogramm: [Atari_Graph_It_CX4109_Basic_Complete_Cassette_Import_deutsch_mit_Vorprogramm.atr](attachments/Atari_Graph_It_CX4109_Basic_Complete_Cassette_Import_deutsch_mit_Vorprogramm.atr)  
  
Enhancements to Graph It, APX-20074 (englisch, 1982) (C) Howard D. Siebenrock  
[Enhancements_to_Graph_It_APX-20074_C_1982_Howard_D._Siebenrock-final.atr](attachments/Enhancements_to_Graph_It_APX-20074_C_1982_Howard_D._Siebenrock-final.atr)  
  
Atari Graph It TXG9517 (deutsch, 1983) alle Kassetten-Images auf einem Disk-Image __ohne__ Vorprogramm: [Graph_It_TXG_9517_C_1983_by_Atari_Deutschland_GMBH.atr](attachments/Graph_It_TXG_9517_C_1983_by_Atari_Deutschland_GMBH.atr)  
  
## Handbücher:  
Für den Bildschirm optimiertes Handbuch (englisch) als PDF-Datei (3,1 MB): [Graph_It_CX4109_Screen_Version.pdf](attachments/Graph_It_CX4109_Screen_Version.pdf)  
Für den Drucker optimiertes Handbuch (englisch) als PDF-Datei (849,6 MB): [Graph_It_CX4109_Print_Version.pdf](attachments/Graph_It_CX4109_Print_Version.pdf)  
  
## Source Codes:  
1. Version von 1980: [1Balken-alt-190_lines.txt](attachments/1Balken-alt-190_lines.txt) ; vom Unterprogramm: Kreis- und Balkendiagramme; 69 Sektoren ; 190 Zeilen Code  
2. Version von 1982: [3Balken-HOWARD-274_lines.txt](attachments/3Balken-HOWARD-274_lines.txt) ; vom Unterprogramm: Kreis- und Balkendiagramme; 92 Sektoren ; 274 Zeilen Code  
3. Version von 1983: [2Balken-neu-237_lines.txt](attachments/2Balken-neu-237_lines.txt) ; vom Unterprogramm: Kreis- und Balkendiagramme; 81 Sektoren ; 237 Zeilen Code  
  
## Bilder:  
![](attachments/Cover.jpg)  
Boxcover 1 von Graph It (englisch) 1980  
  
![](attachments/Back.jpg)  
Boxrückseite 1 von Graph It (englisch) 1980  
  
![](attachments/front.jpg)  
Boxcover 2 von Graph It II (deutsch) 1983 ; Danke an Mr. Bacardi!  
  
![](attachments/back.jpg)  
Boxrückseite 2 von Graph It II (deutsch) 1983 ; Danke an Mr. Bacardi!  
  
![](attachments/Graph_It.jpg)  
Cover vom Handbuch von Graph It (englisch) 1980  
  
![](attachments/manual.jpg)  
Cover vom Handbuch von Graph It II (deutsch) 1983 ; Danke an Mr. Bacardi!  
  
![](attachments/Graph+It-Intro.jpg)  
Graph It-Intro  
  
![](attachments/Graph_It_01.jpg)  
Beispiel für ein Balkendiagramm  
  
![](attachments/Graph_It_03.jpg)  
Beispiel für ein Balkendiagramm mit dreigeteilten Balken  
  
![](attachments/Graph_It_02.jpg)  
Beispiel für ein Kreisdiagramm  
  
![](attachments/Graph_It_04.jpg)  
Beispiel für ein Polardiagramm 1  
  
![](attachments/Graph_It_07.jpg)  
Beispiel für ein Polardiagramm 2  
  
![](attachments/Graph_It_08.jpg)  
Beispiel für ein Polardiagramm 3  
  
![](attachments/Graph_It_10.jpg)  
Beispiel für ein Polardiagramm 4  
  
![](attachments/Graph_It_11.jpg)  
Beispiel für ein Polardiagramm 5  
  
![](attachments/Graph_It_21.jpg)  
Beispiel für ein 2D-Diagramm mit der Funktion: y=x*sin(1/x) - Zoom 1  
  
![](attachments/Graph_It_25.jpg)  
Beispiel für ein 2D-Diagramm mit der Funktion: y=x*sin(1/x) - Zoom 2  
  
![](attachments/Graph_It_05.jpg)  
Beispiel für ein 2D-Diagramm mit 2 Funktionen-1  
  
![](attachments/Graph_It_06.jpg)  
Beispiel für ein 2D-Diagramm mit 2 Funktionen-2  
  
![](attachments/Graph_It_13.jpg)  
Beispiel für ein 3D-Diagramm-1  
  
![](attachments/Graph_It_14.jpg)  
Beispiel für ein 3D-Diagramm-2  
  
![](attachments/Graph_It_18.jpg)  
Beispiel für ein 3D-Diagramm-3  
  
![](attachments/A1.jpg)  
Graph It - Cassette A - side 1 - Bar Charts and Pie Graphs  
  
![](attachments/A2.jpg)  
Graph It - Cassette A - side 2 - Two-Dimensional X, Y Plots  
  
![](attachments/B1.jpg)  
Graph It - Cassette B - side 1 - Polar Plots  
  
![](attachments/B2.jpg)  
Graph It - Cassette B - side 2 - Three-Dimensional X, Y, Z Plots  
  
![](attachments/xy__tape_a_side_1.jpg)  
Graph It II- Kassette A - Seite 1 - 2D-Grafiken ; Danke an Mr. Bacardi!  
  
![](attachments/Balken-Kreis_tape_a_side_2.jpg)  
Graph It II- Kassette A - Seite 2 - Balken- und Kreisdiagramme ; Danke an Mr. Bacardi!  
  
![](attachments/xyz_tape_b_side_1.jpg)  
Graph It II- Kassette B - Seite 1 - 3D-Grafiken ; Danke an Mr. Bacardi!  
  
![](attachments/Polar_tape_b_side_2.jpg)  
Graph It II- Kassette B - Seite 2 - Polardarstellung ; Danke an Mr. Bacardi!  
  
## Autoren:  
  
Version 1980: [Lane Winner](http://www.atarimania.com/list_utilities_atari-400-800-xl-xe-winner-lane_team_2574_8_U.html)  
Version 1982-1983: [Howard D. Siebenrock](../Enhancements_to_Graph_It/index.md)  
  
## Danksagung:  
  
Ohne die folgenden Personen wäre dieses Projekt nicht möglich gewesen, ihnen gilt daher der Dank:  
  
- Carsten Strotmann  
- [Mathy van Nisselroy](http://www.mathyvannisselroy.nl/)  
- Bradley Koda  
- Benjamin Daniel Smith  
- Dirk Tröger  
- Marc Behrens  
- Lothar Strohbusch  
- Erhard Pütz  
- ebay-Verkäufer: happiestsellerever!  
- [Atarimania](http://www.atarimania.com/utility-atari-400-800-xl-xe-graph-it_26990.html)  
- [Mr. Bacardi](http://mrbacardi.000space.com/games/Atari_Germany/Atari_ger_hb.html)  
- [Atarinside](http://atarinside.dyndns.org/blog/index.php/atari-deutschland/) ; Thank you so much Marceau!  
- [Atarimuseum in den Niederlanden](https://atarimuseum.nl/atari-8-bit-software/) ; Thank you so much Fred!  
- ...  
