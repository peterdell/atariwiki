# Modulo Funktion: a MOD b  
  
Die Progrmme sind exklusiv beim PD-Service des WASEO erhältlich, Diskette 1.000):  
  
Aufgrund der Beschränkungen durch die ROMs in den 1970er-Jahren, wurden nur die wichtigsten Funktionen in das Atari-BASIC integriert. Das soll mit der hiermit beginnenden Serie: „Atari BASIC–Funktionenerweiterung“ nachgeholt werden. Dazu werden u. a. auch Algorithmen verwendet, die erst gegen Ende der 2010er-Jahre zur Verfügung standen.  
  
Beginnen wollen wir mit der Modulo-Funktion (MOD): Division mit Rest.  
Bereits auf der JHV 2019 hatte ich dazu die von Walter und mir entwickelte Formel vorgetragen, jedoch waren zu diesem Zeitpunkt noch nicht die erforderlichen Tests durchgeführt worden. Das ist nunmehr erfolgt und die Formel kann somit als final den Mitgliedern vorgestellt werden:  
  
Voraussetzung:  
a MOD b mit b <>0:  
  
Formel:  
REST=a-INT(a/b))*b  
  
Wir verwenden hier die in Atari BASIC eingebaute Funktion: INT, wie in der Formel oben zu sehen ist.  
  
In der Praxis wurden meist immer nur positive Werte sowie ganze Zahlen verwendet. Die Natur hat aber viel mehr zu bieten. Genau genommen wurden damit nur lediglich maximal 25 % der Fälle abgedeckt. Es sind jedoch viermal so viele Fälle, welche den Mitgliedern nunmehr vorgestellt werden sollen:  
  
7 MOD  3 = 2 Rest 1  
−7 MOD  3 = −3 Rest 2  
7 MOD −3 = −3 Rest −2  
−7 MOD −3 =  2 Rest −1  
  
Zur Normierung wird in der Mathematik die Konvention verwendet, die Vorzeichen der Reste aus denen der Teiler zu beziehen, wie in den Beispielen oben dargestellt.  
  
Das Top-Modell von Texas Instruments, der TI-30X Pro MathPrint, von den Kultusministerien empfohlen, scheitert daran (Stand: 2024). Nicht jedoch das Atari BASIC mit der Formel von oben. Ihr meint, das ist schlimm? Es kommt noch dicker: Der CASIO fx-991DE X Classwiz, vielfach eingesetzt in den Schulen, liefert hier sogar falsche Ergebnisse! Der Rechner von Texas Instruments ist zumindest so fair und gibt: „Error Syntax“ wieder. Angesichts der Tatsache, dass sich viele Schüler blind auf den Taschenrechner verlassen, ist das schon tragisch. Ihr meint, das ist schlimm? Es kommt noch dicker!  
  
Obschon man in den 1970er-Jahren bereits wusste, wie MOD korrekt berechnet wird, definierte man beispielsweise in der ISO 1990 für PASCAL falsch! Das Problem: Eine ISO gilt weltweit! Somit auch in der EU und somit auch als DIN-Norm. Wollte man nun sein Programm verkaufen und den Normen gerecht werden, musste man es daher falsch implementieren! Daran haben sich auch alle gehalten, z. B. PASCAL, MAC/65, ACTION!, TurboBasic XL etc. um nur einige Beispiele zu nennen. Wer hat sich nicht daran gehalten und den Kopf zum Denken verwendet? Ihr ahnt es, Carol Show. Daher ist es im Calculator richtig implementiert worden! Aus diesen und anderen Gründen kann daher „so etwas“ natürlich nicht in den Handel gegeben werden. Schafft es doch Carols Calculator darüber hinaus auch noch rationale Zahlen richtig mit der Modulo-Funktion zu behandeln! Der Leser darf das gerne einmal bei aktuellen(!) Rechnern (Stand: 2024) versuchen. ;-)  
  
Ihr denkt jetzt bestimmt, ja, das war in der Vergangenheit, so etwas passiert nicht mehr, wir haben ja schließlich daraus gelernt. Mitnichten wie der Skandal um [De-Mail](https://de.wikipedia.org/wiki/De-Mail) zeigt: dort dann Fußnote 40. Obwohl wissend, dass es nicht sicher ist, definierte man es einfach als „juristisch sicher“ und fertig. Ohne Kommentar an dieser Stelle.  
  
Ihr meint, das ist schlimm? Es kommt noch dicker! Nicht nur, dass falsch oder auch gar nicht berechnet wurde, nein, es gibt darüber hinaus noch jede Menge an verschiedenen Operatoren für ein die gleiche Operation:  
  
Liste von Operatoren für den Rest einer Division  
|https://de.wikipedia.org/wiki/Liste_von_Operatoren_f%C3%BCr_den_Rest_einer_Division] ; unterschiedliche Operatoren für die Modulo-Funktion  
  
damit es den Anwendern auch richtig schön schwer gemacht wird.  
  
Wir hier beim ABBUC wollen uns daher auf: „MOD“ als Operator einigen.  
  
Wer exakte Ergebnisse haben möchte, kann sich auch an den kostenlosen „Mathe-Prof.“ im Internet wenden:  
  
[Beispiel für 5 MOD 10](https://www.wolframalpha.com/input/?i=5+mod+10) ; MOD-Funktion bei WolframAlpha am Beispiel von 5 MOD 10  
  
dort ist bereits ein Beispiel eingefügt.  
  
Wir wünschen viel Spaß beim Rechnen,  
  
GBXL & Luckybuck  
