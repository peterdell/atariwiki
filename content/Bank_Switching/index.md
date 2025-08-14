# Bank Switching (Bankumschaltung)  
Bank Switching bzw. Bankumschaltung und Adressspeicherumschaltung (ASU) sind synonyme Begriffe für die Erweiterung des Computerspeichers eines Computers (RAM oder ROM) über seine natürlichen Adressierungsräume hinaus durch das durch Software gesteuerte, aber in Hardware umgesetzte Umschalten einzelner Speicherbereiche.  
  
Anhand von OSS Super-Cartridges soll Bank Switching im Folgenden erklärt werden:  
  
OSS Module - 043M, M091 ...  
===========================  
  
Es gibt verschiedene Modulversionen die mit M091, 043M und so weiter bezeichnet werden.  
  
Technisch unterscheiden sich die Module in den Adressen, die für die Bankumschaltung verwendet werden. Für die, die nichts über Bankumschaltung wissen: der Atari hat ja einen begrenzten Speicherraum von 64 KiB. Um dem Anwender davon möglichst viel zu lassen, haben sich die Hersteller einiger Module etwas einfallen lassen. Da der Atari ja ohnehin nur auf eine Adresse gleichzeitig zugreifen kann, ist es nicht erforderlich, alles gleichzeitig für den Zugriff bereit zu halten. Also hat man so ein 16K-Modul genommen und es in 4 Teile (Bänke) unterteilt, wobei nur eine Hauptbank und jeweils einer der anderen 3 Bänke gleichzeitig im Speicherzugriff bereit gehalten werden. Die "Neben-"Bänke werden bei Bedarf umgeschaltet. Das nennt sich dann Bankumschaltung oder auf Neudeutsch: bank switching. Als Adresse für die Umschaltung der Bank wird die hexadezimale Adresse $D500 verwendet.  
  
In einem Modul sind die Daten der 4 Bänke (es gibt mittlerweile Module (nicht von OSS) mit sehr viel mehr Bänken) in einem Festspeicher (ROM, EPROM, FLASH, etc.) untergebracht, wobei sich die Abfolge der Bänke unterscheiden kann. Hier erst einmal ein Beispiel, wie so ein OSS-Modul im Atari Speicher eingeblendet wird:  
  
$B000 - $BFFF: Masterbank  
$A000 - $AFFF: Bank x von y  
  
Die Hauptbank (ab jetzt Masterbank genannt, weil in der Modulbezeichnung das "M" für sie steht) muß immer an der Stelle $B000 - $BFFF liegen, weil das Atari Betriebssystem die Adressen $BFFA - $BFFF verwendet, um zu entscheiden, wie mit dem Modul verfahren werden muß. Die genaue Dokumentation hierzu findet sich zum Beispiel im Atari Profibuch.  
  
$BFFE: CARTAD Initialisierungsadresse des Moduls  
$BFFD: CARTFG (Kontrollbyte für verschiedene Optionen)  
$BFFC: CART   Signalisiert das Vorhandensein eines Moduls  
$BFFA: CARTCS Startadresse des Moduls  
  
Anhand dieser Tatsache kann man auch feststellen, welche der 4 Bänke die Masterbank ist, denn normalerweise enthält nur diese in den letzten 6 Bytes Werte, die sinnvolle Start- und Initialisierungsadressen ergeben.  
  
Im weiteren Verlauf betrachten wir den Inhalt eines solchen OSS-Moduls linear, so wie die Daten sich im ROM (...) befinden. Bei einem 16K-ROM geht der Adressbereich von $0000 - $3FFF.  
  
Die 4 Bänke liegen dann in:  
  
$0000 - $0FFF  
$1000 - $1FFF  
$2000 - $2FFF  
$3000 - $3FFF  
  
Gehen wir mal davon aus, das wir die Masterbank im Bereich $3000 - $3FFF gefunden haben, weil nur an den Adressen $3FFA- $3FFF sinvolle Adressen für den Modulstart stehen. Dann müssen zum Identifizieren der restlichen Bänke und des Modultyps nur die jeweils letzte Adresse des jeweiligen Bankbereichs betrachtet werden. Beispiel:  
  
$0FFF: 00  
$1FFF: 04  
$2FFF: 03  
  
In Reihe gelesen ergeben die Datenbytes 043 und wenn wir jetzt noch das M von Masterbank dranhängen, haben wir 043M. Also handelt es sich augenscheinlich um ein Modul vom Typ 043M.  
  
Was bedeuten jetzt aber noch die Werte 0, 4 und 3? Hierbei handelt es sich um den letzten Wert in der Speicheradresse, die zur Bankumschaltung verwendet wird. Also bei 0 -> $D500, bei 4 -> $D504 und bei 3 -> $D503. Folglich wird bei einem M091 Modul für die Schaltung der Bank 9 -> $D509 verwendet. Bitte nicht verwechseln - das sind keine Banknummern! Bei einem Modul mit 4 Bänken gibt es ja auch keine 9te Bank.  
  
So, jetzt mal ein bischen weg von der Theorie. Ich habe auf dem Atari mal den ROM-Inhalt eines Moduls in den Arbeitsspeicher ab Adresse $4000 eingelesen. Die 4 Bänke gehen demzufolge bis $7FFF.  
  
Mit dem Debugger BUG/65 schauen wir uns jetzt mal die Stellen an:  
  
![](attachments/00.png)  
Werte der letzten Stellen der 4 Bänke im BUG/65 Version 2.0 betrachtet  
  
Es handelt sich also um ein Modul vom Typ M091. Demzufolge müßten als Adresen für die Bankumschaltungen $D500, $D501 und $D509 verwendet werden.  
  
Hier die Bilder mit dem Suchergebnis:  
  
![](attachments/01.png)  
Adresen für die Bankumschaltungen eines Moduls vom Typ M091 in den Speicherstellen $D500, $D501 und $D509 im BUG/65 Version 2.0  
  
Wie man sieht, liegen alle Fundstellen im Bereich $4000 - $4FFF. Das ist die Masterbank. Macht ja auch Sinn, denn diese Bank ist immer an, solange nicht das ganze Modul aus ist, denn das kann man über die Adresse $D508 ausschalten.  
  
Schauen wir uns mal noch so ein oder zwei Fundstellen an. Bitte beachten, daß hier das Disassemblieren ein Byte vor der Fundstelle anfangen muß, damit man den eigentlichen Befehl mitbekommt:  
  
![](attachments/02.png)  
Fundstellen für die Bankumschaltungen eines Moduls vom Typ M091 im BUG/65 Version 2.0  
  
Hier wird in allen Fällen der 6502-Mikroprozessorbefehl STA verwendet (Befehl zum Schreiben in das CPU-Register A).  
  
Was muß man denn nun tun, um aus einem M091-Modul ein 043M-Modul zu machen, zumindest was die Daten im ROM betrifft?  
  
Nun, erst einmal müssen die 4 Bänke neu angeordnet werden. Als erstes könnte man die Bank M in unserem Beispiel von $4000 - $4FFF nach $8000 - $8FFF verschieben. Damit ergibt sich dann für den neuen Bereich $5000 - $8FFF die Bankfolge 091M. Ein Problem hierbei ist, daß man jetzt nicht wirklich weiß, ob aus der Bank mit der Bezeichnung 9, die neue Bank 4 oder 3 werden muß. Im Zweifelsfall benötigt man dann zwei Versuche.  
  
Hier gehen wir davon aus, daß aus 9 -> 4 werden muß und aus 1 -> 3. Damit stimmt in unserem Beispiel schon einmal die Anordnung im ROM. Als nächstes müssen die IDs der Bänke korrigiert werden und zwar wie folgt:  
  
$5FFF: 00 -> 00  
$6FFF: 09 -> 04  
$7FFF: 01 -> 03  
  
Als nächstes müssen alle Umschaltbefehle angepaßt werden. Aus allen Bytefolgen "01 D5" muß "03 D5" werden und aus allen "09 D5" muß "04 D5" werden. Dabei muß man auch sicherstellen, daß bei dieser Ersetzerei auch nur Befehle zur Bankumschaltung geändert werden und nicht etwa Zeichenfolgen wie "TAB invU".  
  
Richtig schwierig könnte es werden, wenn indizierte Adressierung verwendet wird, so etwas wie STA $D500,X. Da muß man in die Anpassung deutlich mehr Energie reinstecken. Glücklicherweise hatte ich bislang einen solchen Fall nicht, aber ich hab ja auch erst ein paar Module angepaßt.  
  
FloppyDoc, im Februar 2017  
  
  
In Ergänzung hierzu soll anhand eines Beispiels von einem bestehenden OSS Modul der Typ ermittelt werden.  
  
Man muss versuchen unterschiedliche Bänke einzuschalten und dann schauen, was in den Speicherstellen $A000-$AFFF steht.  
Beispiel: Type 15: OSS 'M091' 16 KiB Super-Cartridge:  
Dies ist ein einfaches Schema, es verwendet nur A0 und A3 Adresslinien:  
  
0: A3=0, A0=0 - $A000-$AFFF: Bank B, $B000-$BFFF: Bank A  
9: A3=1, A0=1 - $A000-$AFFF: Bank C, $B000-$BFFF: Bank A  
1: A3=0, A0=1 - $A000-$AFFF: Bank D, $B000-$BFFF: Bank A  
X: A3=1, A0=0 - Cartridge deaktivieren  
  
Bank A ist immer bei $B000-$BFFF:  
  
LDA #$0__0__  
STA $D500 ; aktiviert Bank B in $A000-$AFFF  
  
LDA #$0__9__  
STA $D500 ; aktiviert Bank C in $A000-$AFFF  
  
LDA #$0__1__  
STA $D500 ; aktiviert Bank D in $A000-$AFFF  
  
Jeweils so schalten und den entsprechenden Speicherbereich damit herausspeichern.  
  
Ggf. steht am Ende jeder Bank auch noch einmal die Banknummer als Kontrolle, aber das findet man am bestem im herausgespeicherten Bereich direkt. Das sieht man gut auf dem ersten Screenshot oben.  
  
JAC! von AtariAge, im Juli 2017  
  
## Referenzen  
- [Bank Switching deutsch](https://de.wikipedia.org/wiki/Bank_Switching)  
- [Bank Switching englisch](https://en.wikipedia.org/wiki/Bank_switching)  
  
## Danksagung  
- Dieser Artikel ist möglich dank vieler ausführlicher Informationen von Hias  
- Er ist vom [Abbuc](http://www.abbuc.de/) Magazin #128 übernommen und etwas erweitert worden  
- Dank an FloppyDoc für den Artikel aus dem [Abbuc](http://www.abbuc.de/) Magazin #128 und die Idee, das einmal in ausführlicher Weise, verständlich und didaktisch aufzubereiten  
- Dank an JAC! von AtariAge für spezifische, zusätzlich Infos zu den OSS Cartridges  
- Dank an Wolfgang vom [Abbuc](http://www.abbuc.de/) für die Genehmigung der Übernahme des Artikels aus dem Magazin #128  
