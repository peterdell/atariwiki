# Arithmetik  
  
  
## Stacknotation  
  
Im folgenden werden hauptsählich Worte in ihrer Einzelfunktion beschrieben. In dieser Form der Beschreibung, die Sie bereits kennengelernt haben, wird die Wirkung eines Wortes auf den Stack in Klammern angegeben und zwar in folgender Form:  
  
```
vorher - Werte auf dem Stack vor Ausführung des Wortes
nachher - Verte auf dem Stack nach Ausführung des Wortes

In dieser Notation wird das oberste Element des Stacks (tos) immer ganz rechts geschrieben. Sofern nicht anders angegeben, beziehen sich alle Stacknotationen auf die spätere Ausführung des Wortes. Bei immediate Worten wird auch die Auswirkung des Wortes auf den Stack während der Kompilierung angegeben. Worte werden ferner durch folgende Symbole gekennzeichnet:

| c | Dieses Wort kana nur während der Kompilation einer :-Definition benutzt werden.
| I | Dieses Wort ist ein immediate Wort, das auch im kompilierenden Zustand ausgeführt wird.
| 83 | Dieses Wort wird im Forth83-Standard definiert und muß auf allen Standardsystemen äquivalent funktionieren.
| U | Kennzeichnet eine Uservariable.

Weicht die Aussprache eines Wortes von der natürlichen englischen Aussprache ab, so wird sie in Anführungszeichen angegeben. Gelegentlich folgt auch eine deutsche Übersetzung. Die Namen der Stackparameter folgen, sofern nicht suggestive Bezeichnungen ge­wählt wurden, dem nachstehendem Schema. Die Bezeichnungen konnen mit einer nachfolgenden Ziffer versehen sein.

|| Stacknotation || Zahlentyp        || Wertebereich in Dezimal || minimale Feldbreite
| flag            | logischer Wert    | 0=flash, sonst=true      | 16bit
| true (tf)       | logischer Wert    | -1 (als Ergebnis)        | 16bit
| false (ff)      | logischer Wert    | 0                        | 16bit
| b               | Bit               | 0..1                     | 1bit
| char            | Zeichen           | 0..127 (0..255)          | 7(8bit)
| 8b              | 8 beliebige Bits  | nicht anwendbar          | 8bit
| 16b             | 16 beliebige Bits | nicht anwendbar          | 16bit
| n               | Zahl, bewertete Bits | -32768 .. 32767       | 16bit
| +n              | positive Zahl     | 0 .. 32767               | 16bit
| u               | vorzeichenlosen Zahl | 0 .. 65535            | 16bit
| w               | Zahl, n oder u    | -32768..65535            | 16bit
| addr            | Adresse, wie u    | 0..65535                 | 16bit
| 32b             | 32 beliebige Bits | nicht anwendbar          | 32bit
| d               | doppelt genaue Zahl | -2,147,483,648..2,147,483,647 | 32bit
| +d              | positive doppelt genaue Zahl | 0..2,147,483,647 | 32bit
| ud              | vorzeichenlose, doppelt genaue Zahl | 0..4,294,967,295 | 32bit
| sys             | systemabhängige Werte | nicht anwendbar | nicht anwendbar

!!VolksForth Arithmetik

-1     ( -- -1 ) \\
0     ( -- 0 )  \\
1     ( -- 1 )  \\
2     ( -- 2 )  \\
3     ( -- 3 )  \\
4     ( -- 4 )  \\

Oft benutzte Zahlenwerte wurden zu Konstanten gemacht. Definiert in der Form :

{{{ n Constant n }}}

Dadurch	wird Syeicherplatz eingespart und die Ausführungszeit ver­kürzt.

* [1+|one-plus]
* [1-|one-minus]
* [2+|two-plus]
* [2-|two-minus]
* [2*|two-times]
* [2/|two-divide]
* [3+|three-plus]
* [abs|absolute]
* [not]
* [negate]
* [even]
* [max|maximum]
* [min|minimum]
* [+|plus]
* [-|minus]
* [*|times]
* [/|divide]
* [mod]
* [/mod|divide-mod]
* [*/|times-divide]
* [*/mod|times-divide-mod]
* [u/mod|u-divide-mod]
* [umax|u-maximum]
* [umin|u-minimum]

!!VolksForth Logik Worte

* [true]
* [false]
* [0=|Zero-equals]
* [0<>|Zero-noequal]
* [0<|zero-less]
* [0>|zero-greater]
* [=|equals]
* [<|less-than]
* [>|greater-than]
* [u<|u-less-than]
* [u>|u-greater-than]
* [and]
* [or]
* [xor]
* [uwithin]
* [case?|case-question]

!!VolksForth 32bit Worte

* [extend]
* [dabs|d-absolute]
* [dnegate|d-negate]
* [d+|d-plus]
* [d-|d-minus]
* [d*|d-times]
* [d=|d-equal]
* [d<|d-less-than]
* [d0=|d-zero-equals]
* [m*|m-times]
* [um*|u-m-times]
* [m/mod|m-divide-mod]
* [ud/mod|u-d-divide-mod]
* [um/mod|u-m-divide-mod]

!!Stack Operations

Herkömmliche Programmiersprachen enthalten mehr oder weniger ausgeprägt das Konzept der PROZEDUREN: Für bestimmte Programmfunktionen notwendige Operatoren werden in benannten Programmteilen zusammengefasst, um diese Programmfunktionen an mehreren Stellen innerhalb eines Programmes über ihren Namen aktivieren zu können. Da FORTH ohne jede Einschränkung prozedural ist, macht FORTH auch keinen Unterschied zwischen Prozeduren und Funktionen oder seinen Operatoren. Alles wird als ein WORT bezeichnet.

FORTH als Programmier-SPRACHE besteht also aus Wörtern. Somit können FORTH-Wörter sein:

# Datenbereiche 
# Algorithmen (Befehle) 
# Programme

Um Prozeduren sinnvoll benutzen zu können, kennen die meisten Sprachen auch PARAMETER:
Dies sind Daten, die einer Prozedur bei ihrem Aufruf zur Bearbeitung übergeben werden. Daten, die ausschließlich innerhalb einer Prozedur benötigt werden, heißen LOKAL zu dieser Prozedur; im Gegensatz dazu nennt man Daten, die außerhalb von bestimmten Prozeduren zur Verfügung stehen und auf die von allen Prozeduren aus mit allen Operatoren zugegriffen werden kann, GLOBAL.

Die erste Möglichkeit der Parameterübergabe zwischen Prozeduren ist die Vereinbarung von benannten GLOBALEN Variablen. Diese globalen Variablen sind für die gesamte Laufzeit des Programmes statisch existent und können von allen Proze­duren manipuliert werden.

Eine andere Möglichkeit der Parameterübergabe besteht im Einrichten eines Spei­cherbereiches, in dem während des Aufrufes eines Wortes namentlich benannte Parameter dynamisch verwaltet werden. Diesen Mechanismus für benannte lokale Variable stellt Standard-FORTH nicht zur Verfügung, weil die Organisation dieser lokalen Variablen mit einem Verlust sowohl der lokalen Daten nach der Ausführung des Wortes als auch einem Verlust in der Ausführungsgeschwindigkeit des Wortes verbunden sind.

Für das volks4TH wurde in der VD 1/88 eine Implementierung benannter lokaler Variablen vorgestellt.

FORTH benutzt zur gegenseitigen Übergabe von Parametern an Wörter hauptsächlich den STACK, einen bestimmten Speicherbereich, in dem die Wörter ihre Parameter er­warten. Diese Parameter erhalten keine Namen, sondern ihre interpretation ergibt sich aus der Position innerhalb des Stack-Speicherbereiches. Daraus resultiert die Vielzahl von Operatoren zur Anderung der Stack-Position eines Wertes, für die FORTH berühmt/berüchtigt ist.

Damit deutlich wird, welche und wieviele Parameter ein Wort benötigt, werden all­gemein STACK-KOMMENTARE verwendet:

Der öffnenden runden Klammer folgt eine Aufzählung der Parameter. Dabei steht der Parameter, der als oberstes Stack-Element erwartet wird, ganz rechts. Dann folgt ein "--", das die Ausführung des Wortes symbolisieren soll. Anschließend wird der Zustand des Stacks nach der Ausführung des Wortes dargestellt, wobei das oberste Stackelement wieder ganz rechts steht. Die schließende runde Klammer beendet den Stack-Kommentar.

Ein Wort SQRT, das die Quadratwurzel einer Integerzahl liefert, würde in FORTH so benannt und beschrieben:
{{{
sqrt ( number -- sqrt )
```
  
Wird dieses neue Wort aufgerufen, so werden alle darin enthaltenen Wörter ausgeführt, eventuell bereitgestellte Parameter bearbeitet und daraus resultierende Ergebnisse auf dem Stack übergeben.  
  
Der Aufruf von Prozeduren erfolgt in FORTH implizit durch die Nennung des Namens, ebenso wie auch die Datenübergabe zwischen Wörtern meist implizit erfolgt.  
  
  
- [drop](../drop/index.md)  
- [2drop](../two-drop/index.md)  
- [dup](../dup/index.md)  
- [?dup](../question-dup/index.md)  
- [2dup](../two-dup/index.md)  
- [swap](../swap/index.md)  
- [2swap](../two-swap/index.md)  
- [nip](../nip/index.md)  
- [over](../over/index.md)  
- [2over](../two-over/index.md)  
- [under](../under/index.md)  
- [rot](../rot/index.md)  
- [-rot](../minus-rot/index.md)  
- [roll](../roll/index.md)  
- [-roll](../minus-roll/index.md)  
- [pick](../pick/index.md)  
- [.s](../dos-s/index.md)  
- [clearstack](../clearstack/index.md)  
- [depth](../depth/index.md)  
- [s0](../s-zero/index.md)  
- [sp!](../s-p-store/index.md)  
- [sp@](../s-p-fetch/index.md)  
