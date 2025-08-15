---
title: CSM_ASM_Teil1
---
# 6502 Programmieren - Teil 1  
### von R. Wilde  
  
  
Zu Beginn dieses Maschinensprache-Lehrganges möchte ich Euch die wichtigsten  
Bauteile (IC's) des ATARI XL/XE und deren Funktion vorstellen. Danach erfolgt eine  
Aufgliederung des Speicherbereiches, in der nächsten Ausgabe dann die  
Zusammenfassung aller Maschinenbefehle.  
  
  
Viele der für Euch vielleicht unverständlichen Begriffe findet Ihr in dem Anhang  
"Begriffserläuterungen" genauer erklärt.  
Alle Adressangaben sind in Hexadezimal mit vorangestelltem "$" gemacht. Dezimale  
Angaben sind mit einem "#" versehen.  
  
## Der Mikroprozessor  
Der Mikroprozessor ist das Gehirn des Computers. Er interpretiert die im Speicher  
stehenden Zahlen als Befehle, die in diesem Lehrgang beschrieben werden sollen.  
Seine Tätigkeit besteht darin, zu rechnen und die Werte eines Registers (siehe unten)  
oder einer Speicherstelle in ein anderes Register oder eine andere Speicherstelle zu  
kopieren.  
  
Die Geschwindigkeit, mit der der Prozessor arbeitet, wird durch einen Quarz  
bestimmt. Dieser Quarz ist das Herz des Computers, nur dass dieses Herz nicht  
schlägt, sondern elektrische Schwingungen erzeugt. Die Anzahl der Schwingungen  
pro Sekunde stellt die sogenannte Taktfrequenz dar. Eine Schwingung oder Periode  
bezeichnen wir als Taktzyklus. Die Zeit, die der Prozessor für die Ausführung eines  
Befehles benötigt, ist durch eine bestimmte Anzahl von Taktzyklen festgelegt. Der  
kürzeste Befehl braucht 2 Taktzyklen, der längste braucht 7 Taktzyklen.  
  
Die Taktfrequenz bestimmt auch die Arbeitsgeschwindigkeit aller anderen Bausteine  
des Computers. Sie beträgt ca. 1,78 Megahertz also ca. 1780000 Hz. (Abkürzung für  
Hertz = Schwingungen pro Sekunde).  
  
## Der ANTIC  
Auch er zählt zu den Mikroprozessoren, da er ebenfalls die im Speicher stehenden  
Werte als Befehle interpretiert. Seine Aufgabe besteht zum einen darin, je nach  
Grafikmodus, die Werte im Bildschirmspeicher umzuwandeln und dem eigentlichen  
Grafikprozessor zur Verfügung zu stellen. Eine weitere Aufgabe besteht darin, die  
Werte für eine spezielle Grafik, der sogenannten Player-Missile-Grafik, dem  
Grafikprozessor zur Verfügung zu stellen. Außerdem fragt er die Position eines  
Ligthpen (Lichtgriffel) ab.  
  
Das ANTIC-Programm wird als Display-List bezeichnet.  
  
## Der GTIA  
Das ist der Grafikprozessor. Er erzeugt das Bild anhand der Daten, die er vom  
ANTIC erhält. Bei der Player-Missile-Grafik kann man dem GTIA die Grafikdaten  
auch direkt übergeben, ohne über den ANTIC zu gehen. Diese Methode verbraucht  
aber sehr viel an Rechenzeit. Eine weitere Funktion des GTIA besteht in der Abfrage  
der Triggereingänge und Konsolentaster (START, SELECT usw.)  
  
## Der POKEY  
Der POKEY hat gleich mehrere wichtige Funktionen. Seine Aufgaben sind die  
Sounderzeugung, die Tastatur- und Paddleabfrage, sowie die serielle  
Datenübertragung.  
  
## Der PIA  
Der PIA ist im Gegensatz zu den vorher beschriebenen IC's kein Spezialbaustein  
sondern ein normaler Portbaustein. Er dient zum einen der Joystickabfrage. Zum  
anderen hat er aber eine noch sehr wichtige Funktion. Über ihn können das  
Betriebssystem, der Selbsttest und das BASIC ein- bzw. ausgeschaltet werden. Bei  
einem Computer mit zusätzlichem Speicher (RAM), wie dem 130XE oder einem  
aufgerüsteten 800XL, werden hier die sogenannten Bänke der Speichererweiterung  
umgeschaltet. Nebenbei wird der PIA auch zur Steuerung der seriellen  
Datenübertragung benutzt.  
  
Für eine genauere Beschreibung der einzelnen IC's verweise ich vorläufig auf spätere  
Ausgaben des Magazins. Diverse Kurzbeschreibungen werden aber auch innerhalb  
dieses Maschinensprache-Lehrganges an geeigneten Stellen zu finden sein.  
  
Nun kommen wir zu den Registern der CPU und deren Funktion. Diese haben die  
Aufgabe, Werte bzw. Zahlen zu speichern oder von einer Quelle zu einem Ziel zu  
transportieren.  
  
![](attachments/Register6502_crop.JPG)  
  
Der Akkumulator (Accu) ist das wichtigste Register des Prozessors. Nur mit ihm  
kann man Rechenoperationen ausführen.  
  
Die sogenannten Indexregister "X" und "Y" werden zur besonderen Adressierung von  
Speicherstellen verwendet.  
  
Das Statusregister "S" dient der Überwachung und Steuerung von Rechenoperationen  
und Programmabläufen.  
  
Damit der Prozessor weiß, welchen Befehl er abarbeiten soll, benötigt er den  
Programmzähler "PC". Dieser beinhaltet die Adresse des gerade zu bearbeitenden  
Befehles.  
  
Zuletzt noch der Stackpointer, der auf einen festen Speicherbereich zeigt, den  
sogenannten "Stack", der bei jedem 6502-System auf Page 1 liegt, also in dem  
Adressbereich zwischen $100-$1FF (in Hexadezimal). Das Register des  
Stackpointers ist 16 Bit groß, wobei die obersten 8 Bit immer mit $01 belegt sind.  
Auf dem Stack legt der Prozessor Werte bzw. Rücksprungadressen ab. Der  
Stackpointer zeigt auf die nächste "leere" Speicherstelle auf dem Stack. Hierzu in den  
nächsten Ausgaben des Magazins noch mehr.  
  
Auf das Statusregister und den Programmzähler hat man keinen direkten Zugriff.  
  
Die folgende Grafik zeigt eine Übersicht über den gesamten Speicherbereich des  
ATARI 800XL :  
  
![](attachments/RAM_crop.JPG)  
  
  
Die älteren Modelle ATARI 400 und ATARI 800 besitzen im Adressbereich $C000  
bis $FFFF allerdings kein RAM (Der ATARI 400 auch im Speicherbereich $4000 bis  
$BFFF nicht). Daher kann bei diesen Modellen das ROM nicht weggeschaltet  
werden. Bei allen XL- und XE-Geräten befindet sich im Adressbereich von $D000  
bis $D7FF, verdeckt durch die Register der Bausteine GTIA, POKEY, PIA und  
ANTIC, das Selbsttest-ROM, welches bei Bedarf mittels einer Portleitung (PB7) des  
PIA über den RAM-Bereich $5000 bis $57FF eingeblendet wird.  
  
## ANHANG – BEGRIFFSERKLÄRUNGEN  
Hier noch eine Beschreibung einiger Begriffe, die in diesem Teil des Lehrganges  
Verwendung fanden:  
;IC's: Integrierte Schaltkreise. Das sind Bausteine, die wie plattgedrückte, auf der  
Seite liegende Quader aussehen. An den Längsseiten befinden sich die Beinchen,  
über die der Kontakt mit der restlichen Schaltung hergestellt wird. Die Anzahl der  
Beinchen und damit auch die Größe der Gehäuse sind unterschiedlich und richten  
sich hauptsächlich nach der Anzahl der winzigen Schaltungen im Inneren.  
;RAM: Random Access Memory. Dies ist ein frei zugreifbarer Schreib/Lese -  
Speicher. Im 800XL ohne Speichererweiterung befinden sich acht von diesen IC's,  
die zusammen den 64k Arbeitsspeicher ergeben. Dieser Arbeitsspeicher dient der  
CPU zum Ablegen bzw. Auslesen von Daten (Werte zwischen 0 und 255).  
;ROM: Read Only Memory. Wie der Name schon sagt, ist das ein Speicherbaustein,  
der nur ausgelesen werden kann - im Gegensatz zum RAM, wo auch Daten bzw.  
Programme abgelegt werden können. Die Daten in den ROM's werden entweder  
direkt bei der Herstellung eingearbeitet oder nachträglich mit einem speziellen  
Programmiergerät "eingebrannt".  
;HEX/Hexadezimal: Das ist ein Zahlensystem, das gerade in Computersystemen  
sinnvolle Anwendung findet. Wie die Bezeichnung sagt, wird hier bis 16 (10+6)  
gezählt, bevor die nächst höhere Stelle raufgezählt wird. Da Zahlen über 9 nicht als  
eine Ziffer dargestellt werden können, verwendet man hier die Buchstaben A-F (A für  
10 und F für 15). Gezählt wird also folgendermaßen:  
```
0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F,10,11,12,
13,14,15,16,17,18,19,1A,1B,1C,1D,1E,1F,
20,21 ...................... 98,99,9A,
9B,9C,9D,9E,9F,A0,A1,A2 usw.
```
  
Hexadezimale Zahlen stellen wir mit einem vorangestelltem "$" dar, dezimale Zahlen  
mit einem vorangestellten "#". Wird weder "#" noch "$" angegeben, so handelt es  
sich zumeist um dezimale Zahlen. Wer mit dieser Kurzbeschreibung noch nicht allzu  
viel anfangen konnte, den verweise ich auf den Artikel "Zahlensysteme im  
Computer" der in der April Ausgabe des CSM erschienen ist.  
  
  
Bis zur nächsten Ausgabe Euer R. Wilde.  
CSM / 6.1988  
---
Der Artikel entstammt der Kursreihe „6502 Programmieren“ des Compy Shop  
Diskettenmagazins. Die Kursreihe besteht aus 14 Kursen, die im Laufe des Jahres 2011 in  
unregelmäßigen Abständen einzeln veröffentlicht werden, bzw. anschließend als Zusammenzug als  
ABBUC-Buch „6502 Programmieren“ erscheinen.  
Koordination: Volkert Barr (volkert@nivoba.de)  
Version 1.2 / 2011-02-12  
