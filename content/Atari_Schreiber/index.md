---
title: Atari Schreiber
---
# Atari Schreiber RXG/DXG 8036 ; Copyright (C) 1983-1985 Atari Elektronik Vertriebs GmbH  
## Beschreibung  
Ganz gleich ob Sie ein Student, Geschäftsmann oder Hobby-SchriftsteIler sind - der ATARI SCHREIBER hilft Ihnen, Ihre Referate, Reporte und sonstige Schriftstücke schnell und somit zeitsparend zu erstellen. Sie werden sogar Freude an diesen „öden“ Tätigkeiten gewinnen. Das ermüdende Schreiben und Umschreiben von Entwürfen entfällt. Mit dem ATARI SCHREIBER editieren und reorganisieren Sie Ihr Schriftstück solange, bis Sie damit zufrieden sind.  
  
Darüber hinaus stehen Ihnen eine Anzahl an Formatier- und Ausdruckbefehlen zur Verfügung. Sie können sicher sein, dass alles, was Sie schreiben, beim Ausdruck auch so aussieht, wie Sie es wünschen. Diese Beschreibung zeigt Ihnen Schritt für Schritt alles, was Sie für eine problemlose Benutzung des ATARI SCHREIBERs wissen müssen.  
  
Im ersten Abschnitt erklären wir Ihnen, wie Sie den ATARI SCHREIBER in Ihr ATARI Privat Computer System einladen, außerdem geben wir Ihnen einen kurzen Überblick über das Programm. Im zweiten Abschnitt wird an Hand eines Beispieltextes die Eingabe von Text, das Editieren eines Textes und der Ausdruck eines Schriftstückes erläutert. Jeder Schritt wird einzeln erklärt. Nachdem Sie Ihr erstes mit dem ATARI SCHREIBER erstelltes Schriftstück ausgedruckt haben, werden Sie mit dem Speichern und Laden von Schriftstücken vertraut gemacht. Es werden dabei die beiden Speichermedien Kassette und Diskette aufgeführt. Durch die Arbeit mit einem grösseren Schriftstück werden Sie dann schließlich im dritten Abschnitt mit komplexeren Editier-, Formatier- und Ausdruckrnöglichkeiten des ATARI SCHREIBER vertraut gemacht. Abschnitt vier stellt Ihnen zum Abschluss dieser Beschreibung eine Auflistung aller Befehle des ATARI SCHREIBERs mit einer Kurzerklärung des jeweiligen Befehls zur Verfügung. Sie können sogar später problemlos die Bedeutung eines Befehles nachschlagen. Dieser Beschreibung liegt außerdem eine REFERENZKARTE bei. Auf ihr sind alle Befehle und die entsprechenden zu drückenden Tasten aufgeführt. Dies ermöglicht Ihnen ein leichtes Auffinden des Befehlcodes einer bestimmten Funktion.  
  
## ROM-Images  
- [Atari_Schreiber-CART-RXG-8036.rom](attachments/Atari_Schreiber-CART-RXG-8036.rom) ; MD5-Prüfsumme: 41691577c97c18b93de8476d671d49d0 ; das ist ein verifizierter ROM-Dump! Sowohl BigBen von AtariAge, als auch [Atarinside](https://atarinside.dyndns.org/blog/index.php/atarinside-items/atari-schreiber-2/) haben unabhängig voneinander die exakt gleiche Prüfsumme ermitteln können von jeweils ihren eigenen ROM-Cartridges!  
- [Atarischreiber.rom](attachments/Atarischreiber.rom) ; MD5-Prüfsumme: a48dd4c4066debd165bdf7fe345cadc0 ; das ist ein verändertes ROM. Es sind etliche Bytes durch NOP-Befehle ersetzt worden, ferner Befehle, die als Schutz in den ROM-Bereich schreiben. Dennoch funktioniert das ROM-Image ohne Probleme. Die Bytes $00-$13 wurden auf $00 (=BRK) gesetzt. Dann wurden weitere elf Bytes auf $EA (=NOP) gesetzt. Und zwar: $08A3-$08A5, $0D6C, $0D6D, $3F56-$3F5D.  
  
![](attachments/Atari_Schreiber-CART-RXG-8036.jpg) ![](attachments/Cracked_rom.jpg)  
  
Atari Schreiber - Vergleich der beiden ROM-Versionen ; die ersten 20 Bytes wurden auf 00 gesetzt ; vielen lieben Dank an GoodByteXL von AtariAge! :-)))  
  
  
Nachweis, dass 16 KiB RAM verwendet werden und kein Bank Switching zum Einsatz kam (vielen lieben Dank an JAC! von AtariAge für den Nachweis):  
  
08a3: Kein Kaltstart wenn Öffnen des Editors "E:" schief geht  
8881: 45 9B             EOR $9B  
8883: A2 00     L8883   LDX #$00  
8885: A9 03             LDA #$03  
8887: 9D 42 03          STA ICCMD,X  
888A: A9 81             LDA #$81  
888C: 9D 44 03          STA ICBAL,X  
888F: A9 88             LDA #$88  
8891: 9D 45 03          STA ICBAH,X  
8894: A9 0C             LDA #$0C  
8896: 9D 4A 03          STA ICAX1,X  
8899: A9 00             LDA #$00  
889B: 9D 4B 03          STA ICAX2,X  
889E: 20 56 E4          JSR CIOV  
88A1: 10 03             BPL $88A6  
88A3: 4C 77 E4          JMP COLDSV => NOP NOP  
  
0d6c: Kein Schreiben von Zufallswerten in den ROM Bereich (Crack-Schutz vor Ausfühung im RAM)  
8D59: A9 00             LDA #$00  
8D5B: 85 64             STA ADRESS  
8D5D: AD 0A D2          LDA RANDOM  
8D60: 29 3F             AND #$3F  
8D62: 09 80             ORA #$80  
8D64: 85 65             STA ADRESS+1  
8D66: AD 0A D2          LDA RANDOM  
8D69: AC 0A D2          LDY RANDOM  
8D6C: 91 64             STA (ADRESS),Y => NOP NOP  
  
3f5f: Kein Setzen von VSEROR auf $8838. Ursprünglich Version führt eigene SIO Checksummen vor der Standardroutine Berechnung durch  
BF47: 78                SEI  
BF48: AD 0C 02          LDA VSEROR  
BF4B: 8D 30 05          STA $0530  
BF4E: AD 0D 02          LDA VSEROR+1  
BF51: 8D 31 05          STA $0531  
BF54: A9 38             LDA #$38  
BF56: 8D 0C 02          STA VSEROR  => NOP NOP  
BF59: A9 88             LDA #$88  
BF5B: 8D 0D 02          STA VSEROR+1 => NOP NOP  
BF5E: 58                CLI  
BF5F: 60                RTS  
8838: A5 31             LDA CHKSUM  
883A: D0 13             BNE $884F  
883C: 68                PLA  
883D: 85 31             STA CHKSUM  
883F: 8C 2F 05          STY $052F  
8842: A0 01             LDY #$01  
8844: 18                CLC  
8845: B1 32             LDA (BUFRLO),Y  
8847: 65 31             ADC CHKSUM  
8849: 69 00             ADC #$00  
884B: 48                PHA  
884C: AC 2F 05          LDY $052F  
884F: 6C 30 05          JMP ($0530)  
  
## PRO-Image  
- [Atari_Schreiber_DXG_8036.pro](attachments/Atari_Schreiber_DXG_8036.pro) ; von [Atarinside](https://atarinside.dyndns.org/blog/index.php/atarinside-items/atari-schreiber/), vielen lieben Dank, Du machst soviel für die deutsche Atarisoftware, vor allem gründlich und ordentlich, vieles wäre ohne Dich verloren gegangen. Wir schulden Dir wirkich viel! Ganz lieben Dank aus Deutschland. :-)  
  
## ATX-Images  
- [Atari_Schreiber-DjayBee.atx](attachments/Atari_Schreiber-DjayBee.atx) ; MD5-Prüfsumme: 057ae25dc3eba037396fc315e09b9064 erstes ATX-Image überhaupt von DjayBee veröffentlicht auf AtariAge ; Mega-Danke von der deutschen Atari-Gemeinde. :-)  
- [Atari_Schreiber.atx](attachments/Atari_Schreiber.atx) ; MD5-Prüfsumme: 057ae25dc3eba037396fc315e09b9064 ; von [Atarinside](https://atarinside.dyndns.org/blog/index.php/atarinside-items/atari-schreiber/), vielen lieben Dank, Du machst soviel für die deutsche Atarisoftware, vor allem gründlich und ordentlich, vieles wäre ohne Dich verloren gegangen. Wir schulden Dir wirkich viel! Ganz lieben Dank aus Deutschland. :-)  
- [Atari_Schreiber_DXG8036__Atari_Germany.atx](attachments/Atari_Schreiber_DXG8036__Atari_Germany.atx) ; MD5-Prüfsumme: 5ed746a6e0c5f1734f0983fc3893a516 ; von BigBen von AtariAge, erstellt mit SuperCard Pro, besser geht es nicht! Mega-Danke BigBen, wir stehen tief in Deiner Schuld! :-)  
  
## ATR-Image  
- [Atari_Schreiber_cracked_DjayBee.atr](attachments/Atari_Schreiber_cracked_DjayBee.atr) ; erstes ATR-Image überhaupt von DjayBee veröffentlicht auf AtariAge ; Mega-Danke von der deutschen Atari-Gemeinde. Wir stehen tief in Deiner Schuld! :-)  
- [Atari_Schreiber.atr](attachments/Atari_Schreiber.atr) ; Version von 1983 ; total entschützt, als Datei mit DOS 2.0S auf einer Diskette  
- [AtariSchreiber1985_2AD_2AE_Schutz.atr](attachments/AtariSchreiber1985_2AD_2AE_Schutz.atr) ; Version von 1985 ; Man braucht dies nur auf eine Disk kopieren und die Sektoren 685 & 686 auf den Status gemäß nachstehendem Bild zu setzen und schon hat man eine Originalkopie! Weitere Infos dazu hier: [Info1](attachments/AtariSchreiber1985_2AD_2AE_ohne_Schutz_bootlog.txt) und [Info2](attachments/AtariSchreiber1985protected_bootlog.txt) ; Ganz herzlichen Dank an GoodByteXL von AtariAge, super Arbeit! :-)))  
![](attachments/AtariSchreiber1985_Kopierschutz.jpg)  
Atari Schreiber 1985 - Kopierschutz - Ganz herzlichen Dank an GoodByteXL von AtariAge  
  
- [Office_mit_Visicalc_1.74a_Calculator_Atari_Schreiber_Bilanz_Ermittlung.atr](attachments/Office_mit_Visicalc_1.74a_Calculator_Atari_Schreiber_Bilanz_Ermittlung.atr) ; bitte OS A oder OS B verwenden  
  
## Handbücher  
- [ATARI_Schreiber_1985_Handbuch.pdf](attachments/ATARI_Schreiber_1985_Handbuch.pdf) ; size: 14,7 MB ; Handbuch von GoodByteXL von AtariAge, es gibt keine besseren PDF-Dateien, nirgends! Danke vielmals GoodByteXL, Du machst wirklich die besten PDF-Dateien, die wir haben. :-) Bitte weiter so!  
- [ATARI_Schreiber_1985_Referenzbeschreibung.pdf](attachments/ATARI_Schreiber_1985_Referenzbeschreibung.pdf) ; size: 12 MB ; Referenzbeschreibung von GoodByteXL von AtariAge, es gibt keine besseren PDF-Dateien, nirgends! Danke vielmals GoodByteXL, Du machst wirklich die besten PDF-Dateien, die wir haben. :-) Bitte weiter so!  
- [Atari_Schreiber_Referenzkarten.pdf](attachments/Atari_Schreiber_Referenzkarten.pdf) ; size: 261 KB ; Copyright (C) 1984 Atari Elektronik Vertriebs GmbH in Hamburg ; vielen lieben Dank an [Atarinside](https://atarinside.dyndns.org/blog/index.php/atarinside-items/atari-schreiber-2/) für das Scannen, Du bist wirklich eine große Hilfe! Bitte weiter so! :-)  
- [Atari_Schreiber_Handbuch.pdf](attachments/Atari_Schreiber_Handbuch.pdf) ; size: 2,5 MB ; Copyright (C) 1984 Atari Elektronik Vertriebs GmbH in Hamburg ; vielen lieben Dank an [Atarinside](https://atarinside.dyndns.org/blog/index.php/atarinside-items/atari-schreiber-2/) für das Scannen, Du bist wirklich eine große Hilfe! Bitte weiter so! :-)  
- [Atari_Schreiber_Referenzbeschreibung.pdf](attachments/Atari_Schreiber_Referenzbeschreibung.pdf) ; size: 1,7 MB ; Copyright (C) 1984 Atari Elektronik Vertriebs GmbH in Hamburg ; vielen lieben Dank an [Atarinside](https://atarinside.dyndns.org/blog/index.php/atarinside-items/atari-schreiber-2/) für das Scannen, Du bist wirklich eine große Hilfe! Bitte weiter so! :-)  
  
## Freier Speicher  
Die große Frage ist immer, wieviele Seiten lassen sich mit dem Atari Schreiber in einem Dokument bearbeiten? Dazu muss zunächst der freie Speicher ermittelt werden. Dafür gibt es 2 Optionen. Einmal den Schreiber als a) Disketten-Version und einmal als b) ROM-Version. In beiden Fällen muss die gelbe OPTION-Taste und die Taste F gedrückt werden:  
  
![](attachments/Atari_Schreiber-freier_Platz_mit_DOS1.jpg)  
Atari Schreiber - a) freier Speicher mit geladenem DOS  
  
![](attachments/Atari_Schreiber-freier_Platz_mit_ROM_ohne_DOS.jpg)  
Atari Schreiber - b) freier Speicher ohne geladenem DOS, nur ROM-Modul und Speicherung auf Kassette  
  
In Version a) stehen somit 20.446 Bytes zur Verfügung und in Version b) 26.075 Bytes. Zum Vergleich: beim [The Writer's Tool von OSS](https://atariwiki.org/wiki/Wiki.jsp?page=The%20WriterS%20Tool) stehen dem Anwender in Version a) 23.071 Bytes zur Verfügung. Hätte Atari es geschafft, statt eines 16-KiB-ROMs ein Bank Switching-ROM zu bauen, dass lediglich 8 KiB Speicher benötigt, wären weitere 8.192 Bytes zur Verfügung gewesen.  
  
Was bedeutet dies nun? Ein Byte entspricht circa einen eingegebenen Buchstaben. Eine normale Seite mit jeweils einer Zeile Abstand zwischen den einzelnen Textzeilen benötigt ungefähr 1.500 Bytes. Es ist ratsam in jedem Schriftstück eine ausreichende Menge an Speicherplatz zu reservieren, damit Sie zu einem späteren Zeitpunkt bei Korrekturen keine Speicherplatzprobleme bekommen. Dies erfordert etwa noch einmal 1.500 Bytes. Der Atari Schreiber warnt den Anwender jedoch bei Erreichen dieser Grenze. Somit ergibt sich folgende Berechnung für Option:  
  
a) 20.446 - 1.500 = 18.946 Bytes = 18,5 KiB = 12,63 Seiten  
b) 26.075 - 1.500 = 24.575 Bytes = 24 KiB = 16,38 Seiten  
c) 23.071 - 1.500 = 21.571 Bytes = 21 KiB = 14,38 Seiten im Falle von [The Writer's Tool von OSS](https://atariwiki.org/wiki/Wiki.jsp?page=The%20WriterS%20Tool)  
d) Platz für 62 Seiten fand sich allerdings bereits schon 2 Jahre früher auf dem [Atari_Word_Processor](../Atari_Word_Processor/index.md). Diese Angabe bezog sich allerdings auf die Speicherung der Anzahl von Seiten auf einer SSSD-Diskette mit DOS II 2.0S, nicht auf das Vorhalten von Seiten im Arbeitsspeicher (RAM)! Wäre sie wahr, dann überträfe sie mit etwa 94.500 Bytes bei weitem den in 1981 auf Atari Computern verfügbaren Speicherplatz! Des Weitern wurde in: [inverseatascii 1](https://inverseatascii.info/2014/09/23/s1e1-atari-word-processor/) und [inverseatascii 2](https://inverseatascii.info/2014/09/23/s1e1-atari-word-processor-2/) bereits nachgewiesen, dass jeweils nur eine Seite sich im RAM befinden sollte und nicht mehr als 10.000 Bytes belegen sollte. Atari emphielt jede Seite einzeln zu speichern und somit bei Beginn einer 2. Seite eine neue Datei anzulegen. Danke Wade, great job! :-)  
  
Zu bedenken ist, dass es sich hierbei um reinen Text handelt, keine Grafiken, keine Tabellen. Sollten wir eines Tages an den Source Code des Programms herankommen, wäre es ggf. möglich entsprechende Erweiterungen durchzuführen. Derzeit sind Erweiterungen bis 4 MB RAM möglich.  
  
## Bilder  
  
![](attachments/Atari_Schreiber-Boxhu%CC%88lle-RXG_8036.jpg)  
Atari Schreiber - Boxhülle für die ROM-Version - Mega-Danke an [Atarinside](https://atarinside.dyndns.org/blog/index.php/atarinside-items/atari-schreiber-2/) für den guten Scan und danke fürs Weiterleiten an uns. Gute Arbeit! Bitte weiter so. :-)  
  
![](attachments/Atari_Schreiber_DXG_8036-Cover.jpg)  
Atari Schreiber - Boxhülle für die Disketten-Version - Mega-Danke an [Atarinside](https://atarinside.dyndns.org/blog/index.php/atarinside-items/atari-schreiber/) für den guten Scan und danke fürs Weiterleiten an uns. Gute Arbeit! Bitte weiter so. :-)  
  
![](attachments/Atari_Schreiber_Diskversion.jpg)  
Atari Schreiber - Hülle für die deutsche Disketten-Version inkl. Umlaute ; bitte beachten: ATARI Corp. (Deutschland) GmbH, Frankfurter Str. 89-91, 6096 Raunheim, PLZ heute: 65479 ; dies scheint die absolut letzte Version des Atari Schreibers von 1985 zu sein. Mega-Danke an GoodByteXL von AtariAge! :-)))  
  
![](attachments/Box.png)  
Atari Schreiber - Inhalt der Box zur deutschen Disketten-Version ; vielen lieben Dank an GoodByteXL von AtariAge! :-)))  
  
![](attachments/Atari-Schreiber-CART-RXG-8036.jpg)  
Atari Schreiber - ROM - Mega-Danke an [Atarinside](https://atarinside.dyndns.org/blog/index.php/atarinside-items/atari-schreiber-2/) für den guten Scan und danke fürs Weiterleiten an uns. Gute Arbeit! Bitte weiter so. :-)  
  
![](attachments/Keyboard_Stickers.jpg)  
Atari Schreiber - Tastatur-Aufkleber für die deutsche Version inkl. Umlaute ; Vielen lieben Dank an [Atarinside](https://atarinside.dyndns.org/blog/index.php/atarinside-items/atari-schreiber/)  
  
![](attachments/Atari_Schreiber-Diskette2.jpg)  
Atari Schreiber Diskette - Version 1 - von [Atarinside](https://atarinside.dyndns.org/blog/index.php/atarinside-items/atari-schreiber/), vielen lieben Dank fürs Scannen  
  
![](attachments/Atari+Schreiber+Diskette.jpg)  
Atari Schreiber Diskette - Version 2  
  
![](attachments/Atari_Schreiber_Diskette.png)  
Atari Schreiber Diskette - Version 3 ; vielen lieben Dank an GoodByteXL von AtariAge! :-)))  
  
![](attachments/Schreiber_Intro.jpg)  
Atari Schreiber - Startbildschirm 1983  
  
![](attachments/Startscreen1985.jpg)  
Atari Schreiber - Startbildschirm 1985  
  
![](attachments/Schreiber_Main.jpg)  
Atari Schreiber - Hauptmenü vom ATR-Image  
  
![](attachments/Schreiber_Main_ATX.jpg)  
Atari Schreiber - Hauptmenü vom ATX-Image  
  
![](attachments/Inhaltsverzeichnis.jpg)  
Atari Schreiber - Inhaltsverzeichnis vom Hauptmenü aus aufgerufen mit eingelegter leerer Diskette mit DOS  
  
![](attachments/Atari_Schreiber_-_leeres_Dokument.jpg)  
Atari Schreiber - leeres Dokument  
  
![](attachments/Referenz-Karten_001.png)  
Atari Schreiber - Referenz-Karten, Seite 1  
  
![](attachments/Referenz-Karten_002.png)  
Atari Schreiber - Referenz-Karten, Seite 2  
  
![](attachments/Referenz-Karten_003.png)  
Atari Schreiber - Referenz-Karten, Seite 3  
  
![](attachments/Referenz-Karten_004.png)  
Atari Schreiber - Referenz-Karten, Seite 4  
  
![](attachments/Referenz-Karten_005.png)  
Atari Schreiber - Referenz-Karten, Seite 5  
  
![](attachments/Referenz-Karten_006.png)  
Atari Schreiber - Referenz-Karten, Seite 6  
  
![](attachments/Raunheim.jpg)  
Atari Adresse nach dem Umzug von Hamburg nach Raunheim in 1985  
  
## Referenz  
- AtariWiki emphielt [Atarinside](https://atarinside.dyndns.org/) als einer der besten Webseiten für deutsche Atarisoftware überhaupt!  
