---
title: VFHandbuchKapitel2
---
# Einstieg ins volksFORTH  
  
  
  
[Google Machine Translation](http://translate.google.de/translate?js=y&prev=_t&hl=de&ie=UTF-8&layout=1&eotf=1&u=http%3A%2F%2Fwiki.strotmann.de%2Fwiki%2FWiki.jsp%3Fpage%3DVFHandbuchKapitel2&sl=de&tl=en)  
  
Damit Sie sofort beginnen können, wird in diesem Kapitel beschrieben,  
  
- wie man das System startet  
- wie man sich Im System zurechtfindet  
- wie man ein fertiges Anwendungsprogramm erstellt  
- wie man ein eigenes Arbeitssystem zusammenstellt  
  
## Die Oberfläche  
  
Wenn Sie VOLKS4TH von der DOS-Ebene starten, meldet sich volksFORTH83 mit einer Einschaltmeldung, die die Versionsnummer rev. <xxxx> enthält.  
  
Was Sie nun von volksFORTH sehen, ist die Oberfläche des Interpreters. FORTH-Systeme und damit auch volksFORTH sind fast immer Interaktive Systeme, in denen Sie einen gerade entwickelten Gedankengang sofort überprüfen und verwirklichen können.  
  
''MS-DOS / ATARI PORTFOLIO''  
  
Das Auffälligste an der volksFORTH-Oberfläche ist die inverse Statuszelle In der unteren Bildschirmzeile, die sich mit __status off__ aus- und mit __status on__ wieder einschalten lässt.  
  
Diese Statuszeile zeigt von links nach rechts folgende Informationen, wobei "/" für "oder" steht,  
  
| <2/8/10/16>  |  die zur Zeit gültige Zahlenbasis (dezimal)  
| s <xx>  | nennt die Anzahl der Zahlenwerte, die zum Verarbeiten bereitliegen  
| Dic <xxxx>  | nennt den freien Speicherplatz  
| Scr <xx>  | Ist die Nummer des aktuellen Quelltextblocks  
| A: / C:  | gibt das aktuelle Laufwerk an (MS-DOS)  
| &lt;name&gt;.&lt;ext&gt; | zeigt den Namen der Datei, die gerade bearbeitet wird. Dateien haben im MS-DOS sowohl einen Namen <name> als auch eine dreibuchstabige Kennung, die Extension <ext>, wobei auch Dateien ohne Extension angelegt werden können.  
| FORTH&nbsp;FORTH&nbsp;&nbsp;FORTH | zeigt die aktuelle Suchreihenfolge gemäß dem Vokabularkonzept. Ein Beispiel dafür sind die Assembler-Befehle: Diese befinden sich In einem Vokabular namens __ASSEMBLER__ und __assembler words__ zeigt ihnen den Befehlsvorrat des Assemblers an. Achten Sie bitte auf die rechte Seite der Statuszeile. wo jetzt __assembler forth forth__ zu sehen ist. Da Sie aber jetzt - noch - keine Assembler-Befehle einsetzen wollen, schalten Sie bitte mit __forth__ die Suchlaufpriorität wieder um. Die Statuszeile zeigt wieder das gewohnte __forth forth forth__ .  
  
  
  
Zur Orientierung Im Arbeitssystem stellt das volksFORTH einige standardkonforme Wörter zur Verfügung:  
  
| words | zeigt Ihnen die Befehlsliste von FORTH, die verfügbaren Wörter. Diese Liste stoppt bei einem Tastendruck mit der Ausgabe oder bricht bei einem <ESC> ab.  
| files | __MS-DOS__: zeigt alle im System angelegten logischen Datei-Variablen, die zugehörigen Handle Nummern, Datum und Uhrzeit des letzten Zugriffs und ihre entsprechenden physikalischen DOS-Dateien. Eine solche FORTH-Datei wird allein durch die Nennung ihres Namens angemeldet. Die MSDOS-Dateien im Directory werden mit __dir__ angezeigt.  
| path  | __MS-DOS__: informiert über eine vollständige Pfadunterstützung nach dem MSDOS-Prinzip, allerdings vollkommen unabhängig davon. Ist kein Suchpfad gesetzt. so gibt __path__ nichts aus.  
| order | beschreibt die Suchreihenfolge In den Befehlsverzeichnissen (Vokabular).  
| vocs  | nennt alle diese Unterverzeichnisse (vocabularies).  
  
## Arbeiten mit Programm- und Datenfiles (MS-DOS / ATARI-ST / CP/M )  
  
Um überhaupt Programmtexte (Quellentexte) schreiben zu können, brauchen Sie eine Datei, die diese Programmtexte aufnimmt. Diese Datei muss zur Bearbeitung angemeldet werden.  
  
volksFORTH geht nach dem Systemstart erst einmal von der Datei VOLKS4TH.SYS als aktueller Datei aus. VOLKS4TH.SYS ist aber die Steuerdatei, aus der Ihr FORTH-System aufgebaut wurde; deshalb deklarieren Sie die Datei. die Sie bearbeiten wollen, mit dieser Befehlsfolge:  
  
```
use <name>.<ext>
```
  
Als Beispiel wird die Datei __test.scr__ mit __use test.scr__ angemeldet.  
  
Möchten Sie allerdings eine vollkommen neue Datei für Ihre Programme benutzen. so überlegen Sie sich einen Namen <name>, eine Kennung <extension> und eine vernünftige Größe in KByte. Anschließend geben Sie ein:  
  
  
```
makefile <name>.<ext> <Größenangabe> more
```
  
Daraufhin wird die Datei auf dem Laufwerk angelegt und zum Bearbeiten angemeldet. Ein __use__ ist danach nicht mehr notwendig.  
  
## Der Editor  
  
''Atari ST, MS-DOS, CP/M''  
  
Zum Bearbeiten von Quellentext-Blöcken enthalten ältere PORTH-Systeme meist Editoren, die diesen Namen höchstens zu einer Zelt verdient haben, als man noch die Bits einzeln mit Lochzange und Streifenleser an die Hardware übermitteln musste. Demgegenüber bot ein Editor, mit dem man jeweils eine ganze Zelle bearbeiten kann, sicher schon einigen Komfort. Da man jedoch mit solch einem Zeileneditor heute keinen Staat mehr machen und erst recht nicht mit anderen Sprachen konkurrieren kann, können Sie im volksFORTH selbstverständlich mit einem komfortablen Fullscreen-Editor arbeiten.  
  
In diesem Editor kann man zwei Dateien gleichzeitig bearbeiten:  
  
Eine Vordergrund-Datei, das aktuelle __isfile__ und ein Hintergrundfile __fromfile__. Daher werden Im Editor zwei Dateinamen angezeigt. Das Wort __use__ meldet eine Datei automatisch sowohl als __isfile__ als auch als __fromfile__ an, so dass sich Verschiebe- und Kopieroperationen nur auf diese eine Datei beziehen.  
  
Im Editor wird Immer ein FORTH-Screen - also 1024 Bytes - In der üblichen Aufteilung in 16 Zellen mit je 64 Spalten dargestellt.  
  
Es gibt einen Zeichen- und einen Zellenspeicher. Damit lassen sich Zeichen bzw. Zellen Innerhalb eines Screens oder auch zwischen zwei Screens bewegen oder kopieren. Dabei wird verhindert, dass versehentlich Text verloren geht, in dem Funktionen nicht ausgeführt werden, wenn dadurch Zeichen nach unten oder zur Seite aus dem Bildschirm geschoben würden.  
  
### HELP und VIEW  
  
Der Editor unterstützt das 'Shadow-Konzept'. Zu jedem Quellentext-Screen gibt es einen Kommentar-Screen. Dieser erhöht die Lesbarkeit von FORTH-Programmen erheblich, Sie wissen ja, guter FORTH-Stil Ist selbstdokumentierend! Auf den Tastendruck CRTL-F9 stellt der Editor den Kommentar-Screen zur Verfügung. So können Kommentare 'deckungsgleich' zu den Quellentexten angefertigt werden. Dieses Shadow Konzept wird auch bei dem Wort __help__ ausgenutzt, das zu einem Wort einen erklärenden Text ausgibt. Dieses Wort wird so eingesetzt:  
  
```
help <name>
```
  
HELP zeigt natürlich nur dann korrekt eine Erklärung an, wenn ein entsprechender Text auf einem shadow screen vorhanden ist.  
  
Häufig möchte man sich auch die Definition eines Wortes ansehen, um z.B. den Stackkommentar oder die genaue Arbeitsweise nachzulesen. Dafür gibt es das Kommando  
  
```
view <name>
```
  
Damit wird der Screen - und natürlich auch das File - aufgerufen, auf dem <name> definiert wurde. Dieses Verfahren ersetzt (fast) einen Decompiler, weil es natürlich sehr viel bequemer Ist und Ihnen ja auch sämtliche Quellentexte des Systems zur Verfügung stehen.  
  
Werfen Sie doch bitte mit __view u?__ einen Blick auf das Wort, das Ihnen den Inhalt einer Variablen ausgibt. Benutzen Sie  
  
```
fix <name>
```
  
( fix - engl. = reparieren), so wird zugleich der Editor zugeschaltet, so dass Sie sofort gezielt Änderungen im Quellentext vornehmen können. Im Editor werden Sie zuerst nach einer Eingabe gefragt "Enter your Id:", die Sie einfach mit dem Druck auf die <cr>-Taste beantworten.  
  
Dann befinden Sie sich Im Editor, mit dem man die Quelltext-blöcke bearbeitet. Der Cursor steht hinter dem gefundenen Wort __u?__. Nun können Sie mit PgUp oder PgDn In den Screens blättern oder mit <ESC> aus dem Editor zum FORTH zurückkehren.  
  
Natürlich müssen für __view__, __fix__ und __help__ die entsprechenden Files auf den Laufwerken 'griffbereit' sein, sonst erscheint eine Fehlermeldung. Die VIEW-Funktion steht auch innerhalb des Editors zur Verfügung, man kann dann mit dem Tastendruck CTRL-F das rechts vom Cursor stehende Wort anfordern. Dies ist insbesondere nützlich, wenn man eine Definition aus einem anderen File übernehmen möchte oder nicht mehr sicher ist, wie der Stackkommentar eines Wortes lautet.  
  
### Öffnen und Editieren eines Flies  
  
Nun aber zum Erstellen und Ändern von Quellentexten für Programme - eine schöne Definition von Editieren. Sie haben sich bestimmt eine Datei __test.scr__ wie oben beschrieben mit  
  
```
makefile test.scr 6 more
```
  
angelegt. Damit haben Sie ein File namens __TEST.SCR__ mit einer Länge von 6 Blöcken (6144 Byte = 6KB), bestehend aus den Screens 0 bis 5; davon sind die Nummern 0 bis 2 für Quellentexte, die anderen für Kommentare bestimmt.  
  
Um In den Editor zu gelangen gibt es drei Möglichkeiten:  
```
<screen#> edit
```
oder  
```
<scr#> l
```
  
ruft den Screen mit der Nummer <scr#> auf. Hat man bereits editiert. ruft  
  
```
v
```
den zuletzt bearbeiteten Screen wieder auf. Dies ist der zuletzt editierte oder aber, und das ist sehr hilfreich, derjenige, der einen Abbruch beim Kompilieren verursacht hat. volksFORTH bricht - wie die meisten modernen Systeme - bei einem Programmfehler wahrend des kompilieren ab und markiert die Stelle, wo der Fehler auftrat. Dann brauchen Sie nur __v__ einzugeben. Der fehlerhafte Screen wird in den Editor geladen und der Cursor steht hinter dem Wort, das den Abbruch des Kompiliervorgangs verursachte.  
  
Als Beispiel soll der Block 1  
editiert werden:  
  
```
1 edit
```
Sie werden nach der Eingabe des dreibuchstabigen Kürzels gefragt. Dieses Kürzel wird dann rechts oben in den Screen eingetragen und gibt die "programmer's id" wieder. Wenn Sie nichts eingeben möchten, drücken Sie bitte nur <cr>. Zum Benutzen dieser Blöcke gibt es noch einige Vereinbarungen, von denen ich hier zwei nennen möchte:  
  
1. wird der Block Nr #0 nie !! für Programmtexte benutzt - dort finden sich meist Erklärungen und Hinweise zum Programm und zum Autor.  
1. In die Zelle 0 eines Blockes wird immer ein Kommentar eingetragen, der mit  (skip Line) eingeleitet wird. Dieser Backslash sorgt dafür, dass die nachfolgende Zeile als Kommentar überlesen wird. In diese Zelle 0 schreibt man dort die Namen der Wörter, die Im Block definiert werden.  
  
  
### Tastenbelegung des Editors  
  
''MS-DOS''  
  
Beim Editieren stehen Ihnen folgende Funktionen zur Verfügung:  
  
  
|| Taste || Funktion  
| F1 | gibt Hilfestellung für den Editor  
| ESC | verlässt den Editor mit dem sofortigen Abspeichern der Änderungen.  
| CTRL-U | (undo) macht alle Änderungen rückgängig, die noch nicht auf Disk zurückgeschrieben wurden.  
| CTRL-E | verlässt den Editor ohne sofortiges Abspeichern.  
| CTRL-F | (fix) sucht das Wort rechts vom Cursor, ohne den Editor zu verlassen.  
| CTLR-L | (showioad) lädt den Screen ab Cursorposition.  
| CTRL-N | fügt an Cursorposition eine neue Zelle ein.  
| CTRL-PgDn | splittet Innerhalb einer Zelle diese Zeile.  
| CTRL-S  | (Scr#) zeigt die Nummer des gerade editierten Screens auf dem Stack ab: z.B. für ein folgendes load oder plist.  
| CTRL-Y | löscht die Zelle an Cursorposition  
| CTRL-PgUp | fügt innerhalb einer Zelle den rechten Teil der unteren Zelle an die obere Zeile ein (join).  
| TAB | bewegt den Cursor einen großen Tabulator vor.  
| SHIFT-TAB | bewegt den Cursor einen kleinen Tabulator zurück.  
| F2 | (suchen/ersetzen) erwartet eine Zeichenkette, die gesucht werden soll und eine Zeichenkette, die statt dessen eingefügt werden soll. Wird eins Übereinstimmung gefunden, kann man mit R (replace) die gefundene Zeichenkette ersetzen, mit <cr> den Suchvorgang abbrechen oder mit jeder anderen Taste die nächste Übereinstimmung suchen. Auf diese Weise kann man die Quellentexte auch nach einer Zeichenkette durchsuchen lassen. Als Ersatz-String wird dann <CR> eingegeben.  
| F3 | bringt eine Zelle In den Zellenpuffer und löscht sie im Screen.  
| F5 | bringt die Kopie einer Zelle In den Zeilenpuffer.  
| F7 | fügt die Zelle aus dem Zellenpuffer In den Screen ein.  
| F4 | wie F3, nur für ein einzelnes Zeichen.  
| F6 | wie F5, jedoch für ein einzelnes Zeichen.  
| F8 | entspricht F7, bezogen auf ein Zeichen.  
| F9 | vertauscht die aktuelle Datei (__isfile__) mit der Hintergrunddatei (__fromfile__). Erneutes F9-Drücken vertauscht erneut und stellt damit den alten Zustand wieder her. Diese Funktion ist dann sinnvoll, wenn Sie eine Datei bearbeiten, sich zwischendurch aber mit CRTL-F ein Wort anzeigen lassen. Dann stellt F9 (=fswap) die alte Dateiverteilung wieder her, die sich durch das __fix__ geändert hat.  
| SHIFT-F9 | schaltet auf die Kommentartexte (shadowscreens) um und beim nächsten Drücken wieder zurück.  
| F10 | legt den aktuellen Screen kurz beiseite, um ihn dann mit einem Druck auf F9 wieder bearbeiten zu können. Sollte Ihnen das volksFORTH eine der Kopierfunktionen __copy__ oder __convey__ mit der Meldung ''TARGET BLOCK NOT EMPTY'' verweigern, weil __isfile__ und __fromfile__ unterschiedlich sind, so sorgt F10 wieder für klare Verhältnisse.  
  
  
Noch ein Hinweis zum Editor:  
  
Der Editor unterstützt nur das Kopieren von Zellen. Man kann auf diese Art auch Screens kopieren, aber beim gelegentlich erforderlichen Einfügen von Screens in der Mitte eines Files ist das etwas mühselig. Zum Kopieren ganzer Screens innerhalb eines Files oder von einem File in ein anderes werden im volksFORTH die Worte __COPY__ und __CONVEY__ verwendet,  
  
### Beispiel: CLS  
  
Für Ihr erstes Programm tragen Sie nun bitte den folgenden Quellentext In Screen 1 ein:  
  
```
\ CLS löscht den gesamten Bildschirm
: cls (--) full page,
```
  
Nun drücken Sie SHIFT-F9 und tragen einen Kommentar in diesen Screen ein, wobei die Erklärung zu __CLS__ in der gleichen Zelle, wie die Definition des Quellentextes, z.B.:  
  
```
\\ CLS

CLS löscht den gesamten Bildschirm, indem es auf die Worte 
full (Bildschirmfenster auf volle Größe) und PAGE (Bild- 
schirmfenster löschen) zurückgreift.
```
  
Ein nochmaliges SHIFT-F9 bringt Sie wieder zum Quellentext (source code) zurück. Damit bekommen Sie diesen erklärenden Text nach dem Kompilieren mit __help cls__ angezeigt.  
  
Wenn Sie einen Block vollgeschrieben haben, blättern Sie nur mit PgUp vor oder mit PgDn zurück zum nächsten Block. Sind Sie mit Ihrem Programm zufrieden, so drücken Sie ESC ; dann wird der geänderte Screen sofort abgespeichert.  
  
Danach werden Sie wieder etwas bemerken: Der Bildschirm arbeitet nicht mehr korrekt, es bleiben oben Zeilen stehen, die nicht scrollen,  
  
Das ist richtig, damit der zuletzt bearbeitete Quellentext nicht nach oben weggescrollt. Um nicht weitere zwei Zeilen des Bildschirms zu verlieren, hat das Fenster, In dem Sie gerade arbeiten, keinen Rahmen. Wie man mit Rahmen und Fenstern arbeitet, wird im Editor vorgeführt, der wie alle anderen Systemteile im Quellentext vorliegt.  
  
Um sich In Zukunft schnell aus der misslichen Lage mit der reduzierten Bildschirmgröße zu befreien, benutzen Sie Ihr erstes selbstgeschriebenes Programm __cls__. Denn die Eingabe von __full__ stellt Ihnen wieder die gesamten Bildschirm zur Verfügung, wogegen __page__ nur das aktuelle Fenster löscht.  
  
In volks4TH wird das Kompilieren - wie In den meisten FORTH-Systemen - über <scr#> load durchgeführt:  
```
1 load
```
  
kompiliert Ihr Wort __CLS__ mit für 'C'- oder Pascal-Programmierer unvorstellbarer Geschwindigkeit ins FORTH. Damit steht Ihr Mini-Programm jetzt zur Ausführung bereit. Zugleich erhalten Sie die Meldung, dass ein Wort namens __CLS__ bereits besteht: ~~CLS exists~~ . Dies hat nur die Konsequenz, dass nach einer Redefinition das alte Wort gleichen Namens nicht mehr zugegriffen werden kann. Eine Möglichkeit, diese Namensgleichheit mit einem bereits existierenden Wort zu vermelden, wäre der Einsatz eines Vokabulars.  
  
Geben Sie einmal __words__ ein, dann werden Sie feststellen, dass Ihr neues Wort __CLS__ ganz oben Im Dictionary steht (drücken Sie die <ESC>-Teste, um die Ausgabe von __words__ abzubrechen oder irgendeine andere Taste, um sie anzuhalten),  
  
Um das Ergebnis Ihres ersten Programmierversuchs zu überprüfen, geben Sie nun ein:  
  
```
cls
```
  
Und siehe da, der gesamte Bildschirm wird dunkel. Schöner wäre es allerdings, wenn Ihr Programm seine Arbeit mit einer Meldung beenden würde. Um dies zu ändern, werfen Sie bitte erst einmal das alte Wort __CLS__ weg:  
  
```
forget cls
```
  
Bitte kontrollieren Sie mit __words__, ob __CLS__ wirklich vergessen wurde. Rufen Sie dann erneut den Editor mit __v__ auf. Nun benutzen Sie das Wort für den Beginn einer Zeichenkette __."__ , das Wort für Ihr Ende __"__ und das Wort für einen Zeilenvorschub __cr__. Ihr Screen 1 sieht dann so aus :  
  
```
\ CLS löscht den Bildschirm mit Meldung
: CLS (--)
   full page
   ." Bildschirm ordnungsgemäß gelöscht!" cr ;
```
  
Nach dem __."__ Muss ein Leerzeichen stehen. Denn FORTH benutzt standardmäßig das Leerzeichen als Trennzeichen zwischen einzelnen Worten, so dass dies Leerzeichen nicht mit zur Zeichenkette (string) zählt. Dann verlassen Sie den Editor und kompilieren Sie Ihr Programm wie gehabt und starten es. Die Änderung erweist sich als erfolgreich, und Sie haben gelernt, wie einfach in FORTH das Schreiben, Austesten und Ändern von Programmteilen ist.  
  
Eine große Hilfe sowohl für den Programmierer als auch für den späteren Benutzer sind Informationen darüber, was gerade geladen wird und was schon kompiliert wurde. Fügt man  
  
```
cr .( Funktion installiert )
```
  
ein, so werden während des Ladens diese Meldungen ausgegeben. Das Wort __.(__ leitet einen Kommentar im Interpreter ein, die schließende Klammer __)__ beendet ihn und __cr__ ist natürlich für den Zeilenvorschub, das carriage return, verantwortlich.  
  
### Compilierung Im Editor - Showload  
  
Eine Besonderheit von volksFORTH ist, dass selbst im Editor Funktionen des Interpreters/Compilers zur Verfügung stehen. Dieses Interpretieren und Kompilieren im Editor nennt sich Showload.  
  
  
| CTRL-F | (fix) sucht und zeigt das Wort rechts vom Cursor, ohne den Editor zu verlassen.  
| CTRL-L | (showload) lädt den Screen ab Cursorposition.  
  
  
Um zu sehen. was diese Showload-Funktion leistet, geben Sie nun bitte folgenden Screen ein:  
  
```
\ Ein Test für das showload
: inc 1+ ;
: dec 1- ;
\\

15 inc .
15 inc dec .
15 15 + 2 spaces .
```
  
Dieser Screen soll jetzt im Editor kompiliert und interpretiert werden !!  
  
Dazu setzen Sie bitte den Cursor durch die Taste CTRL-Home In die erste Zeile auf das Zeichen {pre}{/pre} (skip line). Drücken Sie nun CTRL-L zum Laden des Screens. volksFORTH kompiliert nun bis zu der Zeile, die mit {pre}{/pre} (skip screen) beginnt. Die Wörter __inc__ und __dec__ sind dem System jetzt bekannt und können benutzt werden. Anschließend bewegen Sie den Cursor hinter das {pre}{/pre} und drücken CTRL-L zum weiteren interpretieren im Editor. Sofort sehen Sie die Ausgaben an der entsprechenden Stelle im Editor erscheinen. Dabei bleibt der Inhalt des Screens selbstverständlich unversehrt - verlassen Sie den Editor mit ESC und sehen Sie sich den Inhalt den Screens mit __<scr#> list__ an; Sie sehen nur die Anweisungen, aber nicht mehr die Ausgaben vor sich.  
  
Eine typische Anwendung dieses __showload__ wäre das Neukompilieren eines Wortes nach einer kleinen Änderung oder das interaktive Hinzufügen von Wörtern. die man gerade mal braucht.  
  
  
## Erstellen einer Applikation  
  
''MS-DOS / ATARI-ST / CP/M / ATARI 8Bit''  
  
Sie wollen Ihr 'Programm' nun als eigenständige Anwendung abspeichern. Dazu erweitern Sie es zunächst ein klein wenig. Fügen Sie nun noch folgende Definition in einer neuen Zelle hinzu:  
  
```
: runalone
    cls bye ;
```
  
__RUNALONE__ führt zuerst __CLS__ aus und kehrt dann zum Betriebssystem zurück. Kompilieren Sie nun erneut. Sie führen __RUNALONE__ aber nicht aus, sonst würden Sie FORTH ja verlassen (__bye__).  
  
Das Problem besteht vielmehr darin, das System so abzuspeichern, dass es gleich nach dem Laden __RUNALONE__ ausführt und sonst gar nichts. volksFORTH833 ist an zwei Stellen für solche Zwecke vorbereitet. In den Worten __COLD__ und __RESTART__ befinden sich zwei 'deferred words' namens __'COLD__ bzw. __'RESTART__, die im Normalfall nichts tun, vom Anwender aber nachträglich verändert werden können.  
  
Sie benutzen hier __'COLD__, um auch schon die Startmeldung zu unterbinden. Geben Sie also ein  
  
```
' runalone Is 'cold
```
  
und speichern Sie das Ganze mit __savesystem cls.com__ auf Disk zurück. Sie haben Ihre erste Applikation erstellt, die Sie von der Betriebssystem Ebene aus mit __CLS__ aufrufen können!  
  
Etwas enttäuschend ist es aber schon. Das angeblich so kompakte FORTH benötigt Über 20KByte. Um eine so lächerliche Funktion auszuführen?? Da stimmt doch etwas nicht. Natürlich, es wurden ja eine Reihe von Systemteilen mit abgespeichert, vom Fileinterface über den Assembler, den Editor usw., die für unser Programm Überhaupt nicht benötigt werden.  
  
Um dieses und ähnliche Probleme zu lösen, gibt es das File KERNEL.COM. Dieses Programm enthält nur den Systemkern und das Fileinterface und entspricht damit der Laufzeit-Bibliothek (runtime library) anderer Sprachen.  
__MS-DOS__: Laden Sie also KERNEL.COM und kompilieren Sie Ihre Applikation mit __include multi.vid include test.scr__  
  
Das vorherige Laden von __MULTI.VID__ ist nötig, weil FORTH-Systeme selten über Linker verfügen; wird __MULTI.VID__ nicht vorher geladen, so ist dem FORTH-System das Wort __full__ unbekannt. Dann wie gehabt __RUNALONE__ in __'COLD__ eintragen und das System auf Disk zurückspeichern. Von der MS-DOS Ebene aus lässt sich diese Programmerstellung mit  
```
kernel include multit.vid include test.scr
```
  
durchführen, wobei diese beiden Zellen  
```
' runalone Is 'cold
savesystem dark.com
```
  
die letzten Anweisungen auf Ihrem Screen sind. Damit wird der FORTH-Interpreter angewiesen, die fertige Anwendung __DARK.COM__ auf Disk zu speichern.  
  
Sie haben jetzt eine verhältnismäßig kompakte Version vorliegen. Natürlich ließe sich auch diese noch erheblich kürzen, aber dafür bräuchten Sie einen TargetCompIler, mit dem Sie nur noch die wirklich benötigten Systemteile selektiv aus dem Quellentext zusammenstellen könnten. Mit der beschriebenen Methode lassen sich aber auch größere Programme kompilieren und als Stand-alone-Applikationen abspeichern.  
  
## Das Erstellen eines eigenen FORTH-Systems  
''MS-DOS / CP/M''  
  
Das File VOLKS4TH.COM ist als Arbeitsversion gedacht.  
  
Es enthält alle wichtigen System Teile wie Editor, Drucker-Interface, Tools, Decompiler, Tracer usw. Sollte Ihnen die Zusammenstellung nicht gefallen, können Sie sich jederzeit ein Ihren speziellen Wünschen angepasstes System zusammenstellen.  
  
Schlüssel dazu ist der Loadscreen des Files __VOLKS4TH.SYS__. Sie können dort Systemteile, die Sie nicht benötigen, mit dem Backslash {pre}{/pre} wegkommentieren oder die entsprechenden Zellen ganz löschen. Ebenso können Sie natürlich dem Loadscreen eigene Files hinzufügen. Entspricht der Loadscreen Ihren Wünschen, speichern Sie Ihn mit <ESC> zurück, und verlassen Sie das System mit __BYE__. Laden Sie nun das File __KERNEL.COM__. Geben Sie dann ein,  
```
include volks4TH.sys
```
  
Ist das System fertig kompiliert. schreibt die Anweisung  
```
savesystem volks4th.com
```
  
des Load-Screens eine neue Version von volks4TH.com auf Disk. Damit wird Ihr altes File Überschrieben (Sicherheitskopie!!), sodass Sie beim nächsten Laden von volks4TH.com Ihr eigenes System erhalten.  
  
Natürlich können Sie 'Ihr' System auch unter einem anderen Namen abspeichern. Ebenso können Sie Systemvoreinstellungen ändern. Unsere Arbeitsversion arbeitet - voreingestellt - neuerdings im dezimalen Zahlensystem. Natürlich können Sie mit __hex__ auf Hexadezimalsystem umstellen; wir halten das für sehr viel sinnvoller, weil vor allem Speicheradressen im Dezimalsystem kaum etwas aussagen (oder wissen Sie, ob Speichersteile 978584 Im Bildschirmspeicher liegt oder nicht ?). Wollen Sie bereits unmittelbar nach dem Laden im Hexadezimalsystem arbeiten, können Sie sich dies mit __SAVESYSTEM__ abspeichern, indem Sie von der FORTH Kommandozelle aus __savesystem volks4TH.com__ eingeben.  
  
Im Übrigen empfehlen wir bei allen Zahlen über 9 dringend die Benutzung der so genannten Prefixe,  
  
  
|| prefix || Zahlensystem  
| $      | für Hexadezimal-,  
| &      | für Dezimal- und  
| %      | für Binarzahlen.  
  
  
Man vermeldet so, dass irgendwelche Dateien nicht - oder noch schlimmer, falsch - kompiliert werden, weil man gerade im anderen Zahlensystem ist. Außerdem Ist es möglich, hexadezimale und dezimale Zahlen beliebig zu kombinieren. Je nachdem, was gerade sinnvoller ist. In den Quellentexten finden Sie genug entsprechende Beispiele.  
  
Besonders schnell und komfortabel arbeitet volksFORTH natürlich, wenn alle Teile das Systems auf einer Festplatte abgelegt sind. Sie sollten dafür ein eigenes Directory einrichten und __PATH__ und __DIR__ entsprechend einstellen.  
  
Auch die Arbeit mit einer RAM-Disk ist prinzipiell möglich, allerdings nicht sehr zu empfehlen. FORTH Ist sehr maschinennah und Systemabstürze daher vor allem zu Anfang nicht so ganz auszuschließen.  
  
Das Ausdrucken der Quellentexte des Systems ist sicher sinnvoll, um Beispiele für den Umgang mit voiksFORTH83 zu sehen. So stellen z.B. der Screen-Editor und der Kommando-Editor vollständige Anwendungen dar, die im Quellentext vorliegen.  
  
Welche Flies sich im Einzelnen auf Ihren Disketten befinden und ob sie Kommentarscreens enthalten, steht in der Datei __README.DOC__. Zunächst müssen Sie das Drucker-Interface hinzuladen, falls es nicht schon vorhanden Ist. Reagiert Ihr volksFORTH83 auf die Eingabe von __PRINTER__ mit einem __?__, so Ist das Drucker-Interface nicht vorhanden.  
## Ausdrucken von Screens  
''MS-DOS / ATARI-ST / CP/M''  
  
Sollte In Ihrem System kein Druckerinterface vorhanden sein, so laden Sie es von der FORTH-Kommandozeile aus mit  
  
```
include <Druckername>.prn
```
  
nach. Sollte Ihr Drucker In der Liste nicht erscheinen. so benutzen Sie statt dessen __graphic.prn__ oder __epson.prn__. Die meisten Drucker können als IBM-GraphicPrinter oder als EPSON FX/LX-Drucker arbeiten.  
  
Im Printer-Interface sind einige Worte zur Ausgabe eines formatierten Listings enthalten. __PTHRU__ druckt einen Bereich von Screens, jeweils 6 Screens auf einer DIN A4 Seite In komprimierter Schrift. Ganz ähnlich arbeitet das Wort __DOCUMENT__, jedoch wird bei diesem Wort neben einen Quelltextscreen der zugehörige Shadowscreen gedruckt. __LISTING__ druckt ein ganzes File so aus, man erhält so ein übersichtliches Listing eines Datei mit ausführlichen Kommentaren.  
  
### Glossar  
  
  
|| wort || Stack-Kommentar || Beschreibung  
| pthru | ( von bis -- ) | druckt die angegebenen Blöcke immer zu sechst auf einer Seite aus.  
| document | ( von bis -- ) | arbeitet wie __pthru__, druckt aber jeweils drei Quelltextblöcke und drei Kommentarblöcke auf einer Seite aus  
| listing | ( -- ) | erstellt ein Listing der gesamten Datei, indem jeweils drei Quelltextblöcke und drei Kommentar-Blöcke auf einer Seite ausgedruckt werden  
| plist | ( scr# -- ) | druckt einen angegebenen Block auf dem Drucker aus  
| scr | ( -- addr ) | Ist eine Variable, die die Nummer des gerade editierten Screens enthält. Vergleiche {pre}r#, list, (error{/pre}  
| r# | ( -- addr ) | ist eine Variable, die den Abstand des gerade editierten Zeichens von Anfang des gerade editierten Screens enthält.  
  
  
## Druckeranpassung  
  
Die Druckeranpassung das Arbeitssystems wird Im Falle VOLKS4TH.SYS durch die Zeile  
```
include <printer>.prn
```
  
vorgenommen. In dieser Anpassung sind - zusätzlich zu den reinen Ausgaberoutinen - eine Reihe nützlicher Worte enthalten, mit denen die Druckersteuerung sehr komfortabel vorgenommen werden kann.  
  
Im Arbeitssystem ist das Drucker-Interface bereits enthalten. Müssen Sie Änderungen vornehmen, können Sie mit dem Editor den Loadscreen von VOLKS4TH.SYS ändern und sich ein neues Arbeitssystem zusammenstellen mit:  
```
kernel include volks4TH.sys
```
  
Sie können natürlich auch den Loadscreen in seiner jetzigen Fassung benutzen und das Printer-Interface jedesmal 'von Hand' mit  
```
include <printer>. prn
```
nachladen.  
  
Leider sind im Moment im volksFORTH noch deutsche und engllsche Fehlermeldungen gemischt und die __heip__ Funktion zeigt Ihnen einen erklärenden Text nur, wenn dieser vorhanden ist.  
  
## Überblick  
  
Die wichtigsten Befehle noch einmal im überblick:  
  
  
| status | steuert die Status-Zelle  
| words  | zeigt die gerade verfügbaren Befehle an  
| files | zeigt die angemeldeten Dateien  
| path | verändert oder nennt den Datei-Suchpfad  
| order | listet die Suchreihenfolge der Befehlsgruppen auf  
| vocs | nennt alle verfügbaren Befehlsgruppen  
| view | zeigt und  
| fix | editiert den Quellentext eines bestimmten Wortes  
| help | zeigt - wenn vorhanden - den Kommentartext eines Wort  
| full | schaltet das Blidschirmfenster auf die volle Größe  |  
| page | löscht das aktuelle Fenster / den Bildschirm  
| index | - nicht resident - zeigt den Inhalt einer Block-Datei |  
| list | zeigt den Inhalt eines Screens.  
| include | lädt eine ganze Befehlsgruppe oder einen Programmteil  
  
  
