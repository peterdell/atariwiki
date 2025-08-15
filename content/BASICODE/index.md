---
title: BASICODE
---
# BASICODE  
  
Ein Esperanto für Computer.  
  
BASICODE wurde von niederländischen Computerspezialisten um 1979 entwickelt, um einen einheitlichen Sprachstandard für die Programmiersprache [BASIC](http://en.wikipedia.org/wiki/BASIC) festzulegen.  
BASICODE ermöglicht , dass unabhängig vom verwendeten Rechnertyp Programme ausgetauscht und im Rundfunk übertragen werden können.  
Auch der WDR-Computerclub und die BBC haben derzeit Basicode-Programme ausgestrahlt.  
  
Die bis zum Jahre 1991 in den Niederlanden bestehende Stiftung "BASICODE" unter dem Vorsitz von Klaas Robert hat dem Rundfunk der DDR die Rechte zur Anwendung übertragen.  
In diesem Zuge sind dann auch die Bascoder für die folgenden Computertypen entwickelt worden:  
  
AC1, Z1013, die KC-Reihe aus DDR-Produktion, CPC 464 und 6128, C 64 und C 128, C plus 4 und C 16, Atari XL/XE, Atari ST, ZX-Spectrum, IBM-kompatible PC`s u.a.  
  
Weiterhin mussten durch die Definition eines einheitlichen Datenformats für die damals als Datenträger üblichen Compact Cassetten die Datenrekorder etwas modifiziert werden.  
  
## Der Atari-Bascoder V1.1 für ATARI 800XL/XE 600XL 130XE  
  
von Andreas Graf,  
  
Diplomphysiker, ehem. wissenschaftlicher Mitarbeiter an der Akademie der Wissenschaften der DDR. Er beschäftigte sich mit Systemsoftwareentwicklung für spezielle Rechnersysteme und schrieb den Bascoder für die ATARI-Typen XL und XE, wobei auch ein spezieller BASIC-Interpreter entstand. Weiter fertigte er die hier vorliegende Beschreibung des Bascoders an.  
  
  
## Anleitung für Atari:  
  
- [atari_basicode.pdf](attachments/atari_basicode.pdf) ; aus:"BASICODE mit Programmen auf Schallplatte für Heimcomputer", Prof. Völz, 1990, 208 S. & 1 Datenplatte  
  
  
### ATR-Images  
- [xdos_basicode_v11.atr](attachments/xdos_basicode_v11.atr) ; Atari-Bascoder V1.1 von Andreas Graf  
  
### Ladeanweisung:  
  
Bitte die Diskette mit OPTION booten. Danach LOAD"D:ROOT:BC3" eingeben. Nach dem READY ist BASICODE betriebsbereit. Nun kann mit LOAD"D:*.BC3 ein BASICODE-3 Programm geladen und mit RUN gestartet werden. Um wieder ins DOS zu gelangen bitte POKE 9,1 eigeben und RESET drücken. Einen DOS-Befehl gibt es leider nicht. Um sich das Directory einer Diskette anzusehen, ist etwas Programmcode erforderlich. Einfach Zeile 15 mit folgendem Code hinzufügen:  
  
15 O. "D:*.*",6,0:FORI=1TO36:D$=R.(0):PRINTD$;" ";:NEXTI  
  
Diese kann dann mit Goto 15 angesprungen werden und stört den weiteren BASICODE-Betrieb nicht.  
  
### Referenz  
- [Wikipedia: BASICODE (deutsch)](https://de.wikipedia.org/wiki/BASICODE?oldformat=true)  
- [Wikipedia: BASICODE (englisch)](https://en.wikipedia.org/wiki/BASICODE?oldformat=true)  
- [BASICODE auf www.joyce.de (deutsch)](https://www.joyce.de/basicode/index.htm)  
  
## Images  
![](attachments/screen.jpg)  
ATARI-BASICODE startscreen  
  
## In BASICODE gültige Befehle  
  
| ABS | AND | ASC | ATN | CHR$ | COS  
| DATA | DIM | EXP | FOR | GOSUB | GOTO  
| IF | INPUT | INT | LEFT$ | LEN | LET  
| LOG | MID$ | NEXT | NOT | ON | OR  
| PRINT | READ | REM | RESTORE | RETURN | RIGT$   
| SGN | SIN | SQR | STEP | TAB | TAN   
| THEN | TO | VAL  
| + | - | * | / | ^ | =   
| < | > | <= | >= | <> |   
In begrenztem Umfang ist DEF FN möglich.  
  
  
## Abweichungen bei den erlaubten BASIC-Befehlen  
  
### AND  
Es darf nur auf logische Ausdrücke (Vergleiche) bezogen werden. Die zugehörigen Ausdrücke sollten immer geklammert werden. Also z.B. (X>45) AND (X<70). Zuweisungen von logischen Ergebnissen an eine Variable sind zur besseren Übersicht und Verkürzung zulässig. Also z.B.:  
Q=(A=5)AND(B=0):IF Q THEN...  
  
### ASC  
Nicht alle Computer liefern in allen Fällen exakt den gleichen Wert. Das ist jedoch für die Buchstaben weitgehend erfüllt. Die Nutzung der Funktion sollte daher mit Umsicht und für nur ein Zeichen erfolgen (Besonderheiten des Coomodore beachten!).  
  
### CHR$  
Bei Werten, die kleiner als 32 sind (Steuerzeichen), empfiehlt sich Vorsicht. Die Besonderheiten des Commodore sind zu berücksichtigen.  
  
### DEF FN NAME  
Nur in der einfachen Form mit einer Variablen anwendbar.  
  
### DIM  
Hat immer vor der Nutzung von Feldern zu erfolgen. In BASICODE sind maximal 2 Dimensionen, also z.B. DIM A(3,15), zugelassen. Das Feld beginnt stets mit dem nullten Element, also A(0,0).  
  
### FOR...TO...STEP...NEXT  
Die Schleife wird mindestens einmal durchlaufen. STEP und der Wert danach dürfen weggelassen werden, dann beträgt die Schrittweise 1. Nach NEXT muss immer die zugehörige Variable stehen. Zu einem FOR ist auch nur ein NEXT zulässig. Das Heißt, die Schleife kann nur an einer einzigen Stelle verlassen werden. Aus der Schleife darf nicht herausgesprungen werden. Vorzeitiges Verlassen über eine Bedingung erfolgt durch Setzen des Laufparameters auf seinen Endwert und Sprung zum NEXT.  
  
### GOSUB  
Es muss eine Zahl und keine Variable als Zeilennummer folgen. Eine nicht existierende Zeilenzahl darf nicht verwendet werden. IF...GOSUB ist nicht zulässig, richtig ist IF...THEN GOSUB.  
  
### Goto  
Wie GOSUB, mit Ausnahme von 20 und 950. Auch wenn bei den meisten Rechnern IF...THEN GOTO <Zeilennummer> bzw. IF...GOTO <Zeilennummer> funktioniert, soll konsequenterweise IF...THEN <Zeilennummer> benutzt werden.  
  
### INPUT  
Kann nur eine Variable übernehmen. INPUT A,B ist nicht zugelassen.  
  
### LOG  
Bezieht sich auf die Basis e. Es ist zu beachten, dass in einigen Rechnern hierfür auch LN existiert, was nicht verwendet werden darf. Bei solchen Rechnern kann sich LOG fälschlicherweise auf den dekadischen Logarithmus beziehen. Die Bascoder sorgen für die richtige Umkodierung.  
  
### MID$  
Erfordert drei oder zwei Werte. MID$(A$,5) ist erlaubt.  
  
### NEXT  
Verlangt die Laufvariable, siehe FOR.  
  
### NOT  
Verlangt Klammern, siehe AND.  
  
### ON  
Nach ON darf die Variable nur die zulässigen Werte annehmen, also von 1 bis zur Anzahl der nach GOTO bzw. GOSUB stehenden Adressen.  
  
### OR  
Siehe Bemerkungen unter AND.  
  
### PRINT  
Zur Formatierung existieren nur das Komma, Semikolon und TAB. Mehrere Druckaufträge hinter PRINT müssen generell durch ein Semikolon getrennt werden. Es wird empfohlen, TAB oder Komma durch GOSUB 110 zu ersetzen.  
  
### REM  
Es gibt nur REM und keine alternativen Zeichen, wie ! oder `. In einer REM-Zeile sollte kein Doppelpunkt verwendet werden.  
  
### RESTORE  
Existiert nur ohne Zeilenzahl.  
  
### TAB  
TAB(0) ist nicht erlaubt. Vorsicht! Es gibt einige Computer, die mit 1 zu zählen beginnen. Für die meisten ist die erste Position 0. Subroutine GOSUB 110 befreit von dieser Unsicherheit.  
  
### VAL  
Nimmt bei nicht rein numerischen Argumenten in verschiedenen Rechnern unterschiedliche Werte an.  
  
  
## Kurze Übersicht der BASICODE-GOSUB-Routinen  
  
Die rechts stehenden BASIC-Befehle zeigen Ähnlichkeiten auf und sollen den Überblick erleichtern. Sie wurden in erster Linie aus dem KC-BASIC gewählt.  
  
| 20 Programmstart, System_Reset, Variable löschen usw.| CLEAR  
|100 Text-Modus einschalten und Bildschirm löschen| CLS  
|110 Cursor auf die Position HO,VE| LOCATE  
|120 Cursor-Position in HO,VE zurückholen| VGET, POS  
|150 Auffälliges Anzeigen von SR$; rechts und links 3 Spaces| kein  
|200 Daten einer eventuell gedrückten Taste in IN$ und IN| INKEY$  
|210 wie 200, jedoch mit Warten auf Tastendruck| kein  
|220 Holen des Zeichens aus Schirmposition HO,VE auf IN| VGET$  
|250 Erzeugen eines kurzen Aufmerksamkeitstones| BEEP  
|260 Zufallsvariable in RV mit 0<=RV<1| RND  
|270 Ausführen von garbage collection und Speicherplatz in FR| FRE(X)  
|280 Aus- bzw. Einschalten der STOP/BRK-Taste FR=0 bzw. 1| kein  
|300 SR wird ohne Space in SR$ gewandelt| STR$  
|310 wie 300, jedoch als Zahl mit CT und CN formatiert| USING  
|330 Alle Kleinbuchstaben in SR$ in Großbuchstaben wandeln| kein  
|350 Übergabe von SR$ an den Drucker| PRINT#2  
|360 In neue Zeile mit Drucker (CRLF)| kein  
|400 Erzeugung eines Tons gemäß SV,SD und SP| SOUND  
|450 Warten von maximal SD*0.1s auf einen Tastendruck| PAUSE  
|500 Eröffnen eines File mit Namen NF$ gemäß NF| OPEN  
|540 Aus dem File wird ein String an IN$ übergeben| LOAD*  
|560 SR$ wird in das File geschrieben| SAVE*  
|580 man schließe den Bestand mit Code NF ab| CLOSE  
|600 Graphischen Betrieb und Bildschirm löschen| SREEN  
|620 Setzen eines Punktes in die Position HO,VE mit Farbe CN| PSET  
|630 Zeichnen einer Linie zum Punkt HO,VE in Farbe CN| LINE  
|650 SR$ an der Position HO,VE anzeigen(Grafik-Mode)| kein  
|950 Beenden des BASICODE-Mode| END  
  
  
## In BASICODE verbotene Variablen  
- 1. Alle Variablen, die mit dem Buchstaben O beginnen  
- 2. AS,AT,DI,DI$,D$$,EI,EI$,EL,ER,FN,GO,GR,IF,LN,SQ,SQ$,ST,TI,TI$ und TO.  
- 3. PI, enthält aber nicht den Zahlenwert 3.14159.  
  
  
## Im Bascoder verwendete Variablen mit besonderer Bedeutung  
  
- A,CN,CT,FR,HG,HO,IN,IN$,NF,NF$,RV,SD,SP,SR,SR$,SV,VE und VG.  
  
  
  
  
  
  
  
  
  
