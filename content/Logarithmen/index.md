---
title: Logarithmen
---
# Logarithmen Berechnung in Atari BASIC:  
  
Die Progrmme sind exklusiv beim PD-Service des WASEO erhältlich, Diskette 1.000):  
  
Der Logarithmus ist eine der wichtigsten elementaren Funktionen in der Mathematik, daher hat dessen Berechnung immer eine sehr hohe Priorität. Umso wichtiger ist es daher, diese Berechnung möglichst korrekt durchzuführen. Früher mussten dazu sogenannte Logarithmen-Tafeln herhalten, dann Rechenschieber und später sogenannte Rechenautomaten mit manueller Bedienung. Computer, die ganze Räume füllten, konnten das natürlich, waren jedoch für den normalen Bürger nicht erschwinglich. Mit dem Aufkommen der Taschenrechner Anfang der 1970er-Jahre eröffnete sich nunmehr eine elegante Möglichkeit solche Berechnungen durchführen zu können. Dass digitale Rechner korrekt mit Nullen und Einsen rechnen können, sollte als vorausgesetzt betrachtet werden. Nur handelt es sich hier dann um ganze Zahlen, während Logarithmen meist rationale Zahlen sind, also einen Nachkommaanteil haben. Daher ist ein Algorithmus erforderlich, der hier schnell, aber auch präzise Abhilfe schafft.  
  
In der Vergangenheit kam dabei meist der sogenannte [CORDIC-Algorithmus](https://de.wikipedia.org/wiki/CORDIC) zum Einsatz. Er zählt zu den sogenannten „Shift-and-add-Algorithmen“, die auf bitweiser Verschiebung und ganzzahliger Additionen in Addierwerken basieren.  
  
Erst im Jahre 1994 wurde der [BKM-Algorithmus](https://de.wikipedia.org/wiki/BKM-Algorithmus) vorgestellt. Hier erfolgt die Berechnung mittels eines Iterationsverfahrens mit einer Konvergenzrate von ungefähr einem Bit pro Durchlauf. Aufgrund dieses Umstandes wird der Algorithmus manchmal auch als Bitalgorithmus bezeichnet.  
  
Kern beider Algorithmen ist die Tatsache, dass sich alle höheren Funktionen in der Mathematik auf die vier Grundrechenarten: +, -, * und / zurückführen lassen. Genau das ist der Trick, den man nutzen kann, wenn ein Berechnungsfehler im ROM vorliegt, der nicht behoben werden kann. Auf diese Weise bekommt man genaue Ergebnisse ohne(!) das ROM tauschen zu müssen.  
  
Auf einen weiteren Trick hatte mich Stefan Dorndorf aufmerksam gemacht. Für den Computer ist die Ermittlung des dekadischen Logarithmus einfacher. Hinzu kommt noch die Periodizität, welche sich gut nutzen lässt und einer einfacheren Berechnung entgegenkommt. Daher wird im Folgenden nur der dekadische Logarithmus berechnet und alle anderen Logarithmen dann aus den ermittelten Werten davon. Schließlich kann man mittels einer Konstanten jeden beliebigen Logarithmus in einen anderen umwandeln:  
  
LOG(zur Basis 10)(x) = LOG(zur Basis e)(x) / LOG(zur Basis e)(10)  
  
mit:  
  
LOG(zur Basis e)(10)=2.30258509 als Konstante  
  
und  
  
LOG = Logarithmus (allgemein) im Beispiel oben bzw. LOG(zur Basis e) (LN auf den Taschenrechnern) als natürlicher Logarithmus.  
  
Diese Gleichung zeigt den Zusammenhang und die Umrechnung vom dekadischen Logarithmus zum natürlichen Logarithmus auf. CLOG zu LOG bei Atari BASIC bzw. LOG zu LN bei den Taschenrechnern.  
  
Das Atari BASIC ist 1979 von SMI hergestellt worden. 3 Jahre später gab es dazu von dann OSS eine Korrektur in:  
  
Atari Basic Reference Manual-Product Update-C061038 Rev. A-©1982 Atari, Inc.  
  
Hierin wird beschrieben, dass die ermittelten Werte von 0 bis 1 in CLOG bzw. LOG inakkurat seien. Nach 42 Jahren können wir aber sagen, dass dies aus Bescheidenheit erfolgte und heute eher als eine Korrektur von der Korrektur betrachtet werden kann.  
Eine forensische Analyse ergab nämlich, dass ein Fehler frühestens ab der 7. Nachkommastelle anzutreffen ist! Daher sollte die Näherung für einfache Berechnungen den meisten Anwendern genügen. Vorsicht ist nach wie vor bei Berechnungsketten zu walten, da sich hier der „Fehler“ ggf. weiter auswirken kann.  
  
Der Leser kann die Werte auch selber überprüfen, vorausgesetzt er verwendet keinen Taschenrechner, der ebenfalls den Logarithmus nicht richtig berechnen kann, so wie das z. B. bei Texas Instruments über Jahrzehnte(!) der Fall war:  
  
[Logarithmus-Bug in Taschenrechnern](http://www.datamath.org/Story/LogarithmBug.htm) ; Darstellung der Näherungsfehler bei Taschenrechnern  
  
Hier ist der Atari deutlich flexibler. :-)  
  
Alternativ kann man in den XL- und XE-Rechnern auch das ganze Fließkommapaket austauschen, gegen eines, das fehlerfrei funktioniert:  
  
[Fließkommaberechnung für den Atari](https://atariwiki.org/wiki/Wiki.jsp?page=FAST%20FLOATING%20POINT%20source%20code%20for%20the%20ATARI) ; Schnelle und korrekte Fließkommaberechnung für den Atari  
  
Unser großer Dank geht hier an: Newell Industries & Charles W. Marslett für die Bereitstellung des Quelltextes und Konrad M. Kokoszkiewicz für die Korrektur.  
  
Peter Dell war so nett und erstellte fertige Lösungen auf der Fujiama für uns:  
  
[Fließkommapakete für den Atari](https://atariwiki.org/wiki/attach/Articles/Atari_OS_Rev._A_%26_B_%281979%29_Rev_2_%281983%29_%28Atari%29_%28NTSC_%26_PAL%29_%28400-800-XL-XE%29_with_FastFP.zip) ; Fließkommapakete für den Atari bereits in das OS integriert  
  
so dass die User nach nunmehr 45 Jahren korrekte Berechnungen mit dem Atari durchführen können, wahlweise mit oder ohne Austausch der ROMs.  
  
Ihr denkt, das war es jetzt? Weit gefehlt! Wir wären nicht der ABBUC, wenn wir da nicht noch einen drauf setzen könnten. Die WWK macht Werbung dafür, dass sie eine starke Gemeinschaft sei, der ABBUC hat das nicht nötig, er ist(!) eine starke Gemeinschaft.  
  
Der Algorithmus kann bzgl. der Präzision eingestellt werden. Hier habe ich 8 Stellen Genauigkeit eingerichtet, die in den meisten Fällen auch reichen. Wer nun mehr Ziffern verwenden möchte, sei auf die Arbeiten von Dieter Gretzschel (Old-Man-Tower) verwiesen. Bzgl. des dekadischen Logarithmus kann dazu folgendes Bild verwendet werden:  
  
![](attachments/Logarhitmus-Berechnung.png)  
Logarhitmus-Berechnung: Schritt für Schritt, Stelle um Stelle  
  
was pro Iterationsschritt eine Stelle an Genauigkeit erzielt und somit beliebige Genauigkeit ermöglicht! Wieder einmal bewahrheitet sich: 8 Bit sind genug. ;-)  
  
Das Schema im Bild oben ist einfach erklärt: Man nehme eine beliebige Zahl M von der man den dekadischen Logarithmus bestimmen möchte, hier: 1234,56. Nun sieht man, dass links vom Komma 4 Stellen vorhanden sind. Hat man diese Zahl ermittelt, zieht man davon immer(!) 1 ab. Somit ergibt das im Beispiel oben die Zahl a0=3, welche bereits die Ergebniszahl links vom Komma darstellt (unterste Zeile im Bild). Im 2. Schritt, nimmt man nun das ermittelte a0 (=3 im Beispiel oben) und potenziert damit die Zahl 10. Der Nenner ist dann fertig. In den Zähler kommt als Startwert die Zahl M (=1234.56 im Beispiel oben). Der Quotient wird in Klammern gesetzt und mit 10 potenziert. Daraus ergibt sich eine neue Zahl (=8.2247369382767 im Beispiel oben). Hier sieht man, dass nur eine Stelle links vom Komma existiert, nämlich 8. 1 Stelle, von der eine Stelle abgezogen wird, ergibt 0 Stellen, somit ist a1=0. Der Wert wird dann wieder als Exponent an der Zahl 10 verwendet und ergibt somit den neuen Nenner. Der neue Zähler ist nun die eben berechnete Zahl: (=8.2247369382767 im Beispiel oben). Der Quotient wird wieder in Klammern gesetzt und mit 10 potenziert. Daraus ergib sich dann der Wert: 1416511689,4063. Links vom Komma befinden sich 10 Stellen. Wieder ziehen wir eine Stelle ab und erhalten 9 als Ergebnis. a2=9 ist die 3. Ziffer des Endergebnisses. Auf diese Art und Weise können somit beliebig viele Nachkommastellen ermittelt werden.  
  
Und nun viel Spaß beim Rechnen,  
  
Euer  
  
Luckybuck  
