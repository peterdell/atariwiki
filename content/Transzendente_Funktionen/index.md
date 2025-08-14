# Transzendente Funktionen in Atari BASIC:  
  
Die Progrmme sind exklusiv beim PD-Service des WASEO erhältlich, Diskette 1.000):  
  
  
Nach 45 Jahren ist es nun so weit, die transzendenten Funktionen für das Atari BASIC sind umgesetzt. Im Nachhinein fragt man sich natürlich, warum das so lange gedauert hat? Ferner werden viele Nicht-Atarianer davon noch nichts gehört haben. Im Anhang E des Atari Basic Reference Manuals findet man zwar die Beziehungen der jeweiligen Funktionen zu den implementierten Funktionen, wovon 2 jedoch fehlen und 3 nicht korrekt sind, auf der anderen Seite sind in Excel für den Mac 2019 immer noch 4 Funktionen nicht integriert.  
  
Der ABBUC ist immer daran interessiert seinen Mitgliedern vollständige Informationen zur Verfügung zu stellen, was hier an dieser Stelle nun passieren soll. Es reicht nicht die Gleichungen zu haben, man muss auch wissen, wie der Definitions- und Wertebereich aussieht, sonst kommt es zu unerwünschten Komplikationen.  
  
In der Vergangenheit war es sehr schwierig hierzu überhaupt Literatur zu finden, die erschöpfend Auskunft geben kann. Auf den Taschenrechnern der 1970er-Jahre, selbst auf dem Flaggschiff des Jahrzehnts, dem HP-41C, der auch mit dem Space Shuttle flog und es im Notfall landen konnte, fehlen diese Funktionen auf der Tastatur.  
  
Eingestehen muss ich aber auch, dass ich im Studium der Luft- und Raumfahrttechnik nur einmal den SINH brauchte und bei der Dissertation nur einmal COSH und TANH. Die Umkehrfunktionen habe ich nie verwenden müssen. Dennoch sieht die Sache bei den Physikern anders aus. Ferner meine ich auch eine Folge Baywatch gesehen zu haben, wo kurz in einer Bademeisterprüfung darauf eingegangen wurde. ;-)  
  
Der ABBUC hat wieder einmal keine Mühen gescheut und bietet seinen Mitgliedern etwas ganz besonderes anlässlich der eintausensten PD-Diskette an: die kompletten transzendenten Funktionen, lauffähig in Atari BASIC programmiert. Neben den bereits bekannten: SIN, COS und ATN kommen jetzt noch 21 weitere Funktionen hinzu; hier die gesamte Übersicht in die jeweiligen Kategorien eingeordnet:  
  
### Trigonometrische Funktionen:  
Sinus: SIN(X)  
Kosinus: COS(X)  
Tangens: TAN(X) = SIN(X) / COS(X)  
Kosekans: CSC(X) = 1 / SIN(X)  
Sekans: SEC(X) = 1 / COS(X)  
Kotangens: COT(X) = 1 / TAN(X) = COS(X) / SIN(X)  
  
### Arkusfunktionen:  
Arkussinus: ARCSIN(X)  
Arkuskosinus: ARCCOS(X)  
Arkustangens: ARCTAN(X)  
Arkuskosekans: ARCCSC(X) = ARCSIN(1 / X)  
Arkussekans: ARCSEC(X) = ARCCOS(1 / X)  
Arkuskotangens: ARCCOT(X) = ARCTAN(1 / X)  
  
### Hyperbelfunktionen:  
Hyperbolischer Sinus: SINH(X)  
Hyperbolischer Kosinus: COSH(X)  
Hyperbolischer Tangens: TANH(X)  
Hyperbolischer Kosekans: CSCH(X) = 1 / SINHYP(X)  
Hyperbolischer Sekans: SECH(X) = 1 / COSHYP(X)  
Hyperbolischer Kotangens: COTH(X) = 1 / TANHYP(X)  
  
### Areafunktionen:  
Areasinus Hyperbolicus: ARCSINH(X)  
Areakosinus Hyperbolicus: ARCCOSH(X)  
Areatangens Hyperbolicus: ARCTANH(X)  
Areakosekans Hyperbolicus: ARCCSCH(X) = ARCSINHYP(1 / X)  
Areasekans Hyperbolicus: ARCSECH(X) = ARCCOSHYP(1 / X)  
Areakotangens Hyperbolicus: ARCCOTH(X) = ARCTANHYP(1 / X)  
  
Die vorliegende Version 1.0 des Programms macht z. Z. noch die Eingabe im Winkelmaß RAD erforderlich. Eine Umrechnung in Dezimalgrad DEG oder in Neugrad GRAD (wird für Vermessungen häufig verwendet) gestaltet sich aber einfach.  
  
Ich habe das Programm mit großer Sorgfalt geschrieben sowie nach bestem Wissen und Gewissen umgesetzt, dennoch kann ich nicht ausschließen, dass es noch Bugs hat und möchte es daher erst einmal zur Diskussion stellen. Ganz dringend ist darauf zu achten, dass der Definitions- und Wertebereich jeweils eingehalten wird. Dazu habe ich eine [PDF-Datei](attachments/Transzendent.pdf) erstellt, die ziemlich lang ist, jedoch dem Anwender einen guten Überblick verschafft.  
  
![](attachments/Transzendent.png)  
Transzendente Funktionen für Atari BASIC  
  
Für insbesondere negative Kritik hinsichtlich Fehler wäre ich sehr dankbar, um ggf. eine Version 1.1 zu erstellen, sonst bleibt es zunächst bei der Version 1.0. Wie heisst es doch so schön? Wissenschaft ist immer Irrtum auf dem letzten Stand. ;-)  
  
In diesem Sinne wünsche ich euch viel Spaß beim Rechnen mit den neuen Funktionen,  
  
Euer  
  
Luckybuck  
