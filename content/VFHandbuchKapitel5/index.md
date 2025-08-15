---
title: VFHandbuchKapitel5
---
# Ein- / Ausgabe im volksFORTH  
  
  
## Ein- / Ausgabebefehle im volksFORTH  
  
Alle Eingabe- und Ausgabeworte (__KEY__ __EXPECT__ __EMIT__ __TYPE__ etc.) sind im volksFORTH vektorisiert, d.h. bei ihrem Aufruf wird die Codefeldadresse des zugehörigen Befehls aus einer Tabelle entnommen und ausgeführt. So ist im System wine Tabelle mit Namen DISPLAY enthalten, die für die Ausgabe auf dem Bildschirmterminal sorgt.  
  
Dieses Verfahren der Vektorisierung bietet entscheidende Vorteile:  
  
- Nit der Input-Vektorisierung kann man z.B. mit einem Schlag die Eingabe von der Tastatur auf ein Modem umschalten.  
*Durch die Output-Vektorisierung konnen mit einer neuen Tabelle alle Ausgaben auf ein anderes Gerät (z.B. einen Drucker) geleitet werden, ohne die Ausgabebefehle selbst ändern zu müssen.  
- Mit einem Wort (__DISPLAY__, __PRINT__) kann das gesamte Ausgabeverhalten geändert werden. Gibt man z.B, ein: {{{ print 1 list display }}} wird Screen 1 auf einen Drucker ausgegeben und anschließend wieder auf den Bildschirm zurückgeschaltet. Man braucht also kein neues Wort, etwa PRINTERLIST, zu definieren.  
  
Eine neue Tabelle wird mit dem Wort __OUTPUT:__ erzeugt. Die Definition konnen Sie mit {{{view output:}}} nachsehen. __OUTPUT:__ erwartet eine Liste von Ausgabeworten, die mit ; abgeschlossen werden muß.  
  
Beipsiel:  
```
Output: >PRINTER
   pemit  pcr  ptype  pdel  ppage  pat  pat? ;
```
  
Damit wird eine neue Tabelle mit dem Namen __>PRINTER__ angelegt. Beim späteren Aufruf von __>PRINTER__ wird die Adresse dieser Tabelle in die Uservariable __OUTPUT__  
geschrieben. Ab sofort führt __EMIT__ ein __PEMIT__ aus, __TYPE__ ein __PTYPE__ usw.  
  
Die Reihenfolge der Worte nach __OUTPUT:__  
userEMIT userCR userTYPE userDEL userPAGE userAT userAT?  
muß unbedingt eingehalten werden. Entsprechend wird die Input-Vektorisierung gehandhabt.  
  
## Ein- / Ausgaben über Terminal  
  
Das volksFORTH verfügt über eine Reihe von Konstanten, die der besseren Lesbarkeit dienen:  
  
- [c/row](../characters-per-row/index.md)  
- [c/col](../characters-per-column/index.md)  
- [c/dis](../characters-per-display/index.md)  
- [c/l](../characters-per-line/index.md)  
- [l/s](../lines-per-screen/index.md)  
- [bl](../bl/index.md)  
- [#esc](../number-escape/index.md)  
- [#cr](../number-carriage-return/index.md)  
- [#lf](../number-linefeed/index.md)  
- [#bel](../number-bell/index.md)  
- [#bs](../number-backspace/index.md)  
- [standardi/o](../standard-input-output/index.md)  
- [inputkol](../inputkol/index.md)  
- [outputkol](../outputkol/index.md)  
- [area](../area/index.md)  
- [areakol](../areakol/index.md)  
- [terminal](../terminal/index.md)  
- [window](../window/index.md)  
- [full](../full/index.md)  
- [curat?](../cursor-at-question/index.md)  
- [cur!](../cursor-store/index.md)  
- [setpage](../setpage/index.md)  
- [video@](../video-fetch/index.md)  
- [savevideo](../savevideo/index.md)  
- [restorevideo](../restorevideo/index.md)  
- [catt](../catt/index.md)  
- [list](../list/index.md)  
- [(page](../paren-page/index.md)  
- [page](../page/index.md)  
- [(del](../paren-delete/index.md)  
- [del](../del/index.md)  
- [(cr](../paren-carriage-return/index.md)  
- [cr](../cr/index.md)  
- [?cr](../question-carriage-return/index.md)  
- [(at](../paren-at/index.md)  
- [(at?](../paren-at-question/index.md)  
- [at](../at/index.md)  
- [at?](../at-question/index.md)  
- [col](../col/index.md)  
- [row](../row/index.md)  
- [curoff](../curoff/index.md)  
- [curon](../curon/index.md)  
- [curshape](../curshape/index.md)  
- [printer](../printer/index.md)  
- [print](../print/index.md)  
- [+print](../plus-print/index.md)  
- [lst!](../list-store/index.md)  
  
## Ein- / Ausgabe von Zahlen  
  
Die Eingabe von Zahlen erfolgt im interpretativen Modus über die Tastatur, wobei grundlegende Eingabeworte mit __number__ __numbers__ und den verwandten Worten definiert werden. Bei der Ausgabe von Zahlen ist wieder die fehlende Typisierung von FORTH zu beachten — für ein bestimmtes Datenformat (integer, unsigned, double) ist jeweils der geeignete Operator auszuwählen.  
  
- [.](../dot/index.md)  
- [u.](../unsigned-dot/index.md)  
- [d.](../double-dot/index.md)  
- [.r](../dot-right-justified/index.md)  
- [u.r](../unsigned-dot-right-justified/index.md)  
- [d.r](../double-dot-right-justified/index.md)  
  
## Ein- / Ausgabe über einen Port  
  
''MS-DOS''  
- [pc@](../port-char-fetch/index.md)  
- [pc!](../port-char-store/index.md)  
  
## Eingabe von Zeichen  
  
In FORTH wird man immer einen Speicherbereich benennen, in dem Zeichen und Zeichenketten verarbeitet werden. Hierfür verwendet man meistens einen kleinen, 80 Zeichen langen Speicherbereich namens __PAD__. Dieser Notizblock — so die deutsche Übersetzung von pad — belegt keinen festen Speicherbereich und steht sowohl dem FORTH-System als auch dem Programmierer zur Verfügung.  
  
Dann mochte ich Ihnen mit dem Texteingabe-Puffer __TIB__ einen weiteren wichtigen Speicherberelch vorstellen, der den vernünftigen Umgang mit den angeschlossenen Geräten sicherstellt. Weil die Texteingabe über die Tastatur relativ langsam vorsichgeht, werden die Zeichen hier erst in einem freien Speicherbereich, dem Pufferspeicher __TIB__, gesammelt und dann abgearbeitet.  
  
- [tib](../tib/index.md)  
- [#tib](../number-tib/index.md)  
- [>tob](../to-tib/index.md)  
- [>in](../to-in/index.md)  
- [pad](../pad/index.md)  
- [input](../input/index.md)  
- [keyboard](../keyboard/index.md)  
- [empty-keys](../empty-keys/index.md)  
- [(key?](../paren-key-question/index.md)  
- [key?](../key-question/index.md)  
- [(key](../paren-key/index.md)  
- [key](../key/index.md)  
- [(decode](../paren-decode/index.md)  
- [(expect](../paren-expect/index.md)  
- [expect](../expect/index.md)  
- [span](../span/index.md)  
- [>expect](../to-expect/index.md)  
- [nullstring?](../nullstring-question?/index.md)  
- [stop?](../stop-question/index.md)  
- [source](../source/index.md)  
- [word](../word/index.md)  
- [parse](../parse/index.md)  
- [name](../name/index.md)  
- [find](../find/index.md)  
- [execute](../execute/index.md)  
- [perform](../perform/index.md)  
- [query](../query/index.md)  
- [interpret](../interpret/index.md)  
- [output](../output/index.md)  
- [display](../display/index.md)  
- [(emit](../paren-emit/index.md)  
- [emit](../emit/index.md)  
- [charout](../charout/index.md)  
- [tipp](../tipp/index.md)  
- [(type](../paren-type/index.md)  
- [type](../type/index.md)  
- [ltype](../long-type/index.md)  
- [space](../space/index.md)  
- [spaces](../spaces/index.md)  
