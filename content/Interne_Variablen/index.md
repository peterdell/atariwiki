General Information  
Author: Peter Finzel  
Language: ACTION!  
Compiler/Interpreter: ACTION!  
Published: ATARI Magazin #3 (05/06-87), ACTION! Center 3  
---
# Interne Variablen  
## Teil 3 des Action!-Centers führt in die Verwendung der compilerspeziﬁschen Variablen ein.  
  
Wer schon einmal mit Action! gearbeitet hat, wird sich nur schwer der Faszination dieser Sprache entziehen können. Action! ist angenehm, in der Bedienung, schnell im Kompilieren und erzeugt nicht zuletzt Programme, die mit reinen Assembler-Programmen in Laufzeit und Länge konkurrieren können.  
  
In der heutigen Folge werden Sie sehen, wie die Möglichkeiten des Compilers noch besser zu nutzen sind. Ebenso wie Basic verfügt Action! über eine Reihe von internen Variablen, mit denen man z.B. die Code Erzeugung hervorragend steuern kann. Es ist sogar möglich, Programme so zu schreiben, dass sich Speicherbereiche nutzen lassen, die während der Kompilierung nicht zur Verfügung stehen.  
  
Was in Basic der POKE-Befehl, ist in Action! die SET-Direktive. Mit ihr kann man gezielt einzelne Speicherzellen oder 2-Byte-Werte in den Speicher eintragen. Da dies gelegentlich zu Verwirrungen führen kann. wollen wir zunächst zwei Beispiele betrachten:  
```
trägt nur den Wert $80 in die Speicherzelle $491 ein. Dagegen beschreibt
{{{SET $491 = $5140}}}
Adresse $491 mit $40 und Adresse $492 mit $51. Beachten Sie bitte, dass im ersten Beispiel die Speicherzelle $492 nicht verändert, also auch nicht mit Null beschrieben wurde! Man sollte sich demnach immer bewusst sein, ob man Bytes oder Cards eintragen will. Nur wenige wissen wahrscheinlich, dass die SET-Direktive auch mit dem Pointer-Symbol angewendet werden kann:

SET S491=$5000^ schreibt den Inhalt der Speicherzelle $5000 nach $491. Falls der Inhalt von $5001 ungleich Null ist, so wird dieser nach S492 transferiert. Auch hier sollte man ein bisschen vorsichtig sein.

!Interne Variablen

Die SET-Direktive wird während des Kompilierens und nicht während der Laufzeit des erzeugten Programms ausgeführt. Dies ist von einiger Bedeutung. Sehen wir uns nun die wichtigsten internen Variablen des Action!-Compilers an, die zur Steuerung der Code-Erzeugung eingesetzt werden:

!APPMHI (Adresse $0E, 2 Bytes)
Dieses seltsame Kürzel, das für Application Memory High steht, ist eigentlich mehr eine Variable des Atari-Betriebssystems, die bei Action! aber sehr häuﬁg verwendet wird. Hier findet sich immer ein Zeiger auf die nächste freie Speicherzelle, die Action! nutzen kann. Das hat nun mehrere Konsequenzen.

Wenn Sie APPMHI mit ?$0E im Monitor nach einem Kompiliervorgang abfragen, so wird die Endadresse des kompilierten Programms angezeigt. Fragen Sie diese Speicherzelle vor dem Kompilieren ab, erhalten Sie die Anfangsadresse, die im normalen Betrieb mit der Endadresse des Textspeichers übereinstimmt. Auf diese Weise lässt sich z.B. die Länge der erzeugten Programme herausfinden. Wenn Sie APPMHl mit SET verändern, wird der Objectcode ab der SET-Direktive an die gewünschte Speicherstelle eingetragen. lm Prinzip ist SET $0E=<Adresse> nichts anderes als der .ORG- oder *=-Befehl eines Assemblers.

!CODEBASE (Adresse $491, 2 Bytes)
Wenn Sie das Handbuch des Compilers Studiert haben, dann wissen Sie, dass $0E und $491 immer gemeinsam auf die gleiche Adresse geändert werden sollten. Das muss allerdings nicht in jedem Fall sinnvoll sein, denn CODEBASE hat nur die Funktion, sich die Anfangsadresse des kompilierten  Programms für eine eventuelle Aufzeichnung mit dem Monitorbefehl W auf Disk zu merken. Wenn Sie CODEBASE mit SET verändern, können Sie somit auch größere oder kleinere Segmente auf Disk speichern.

!CODESIZE (Adresse $493, 2 Bytes)
Hier merkt sich Action! wie viele Bytes erzeugt wurden, damit der entsprechende Speicherblock auf Disk geschrieben werden kann. Wenn Sie also diese Variable modifizieren, so empﬁehlt es sich auch, sie auf den neuesten Stand zu bringen.

!STSP (Adresse $495‚ 1 Byte)
Diese 1-Byte-Variable hat zwar nur mittelbaren Einﬂuss auf die Code Erzeugung, ist aber in vielen Fällen sehr wichtig. Sie gibt an, wie viele Pages für die Symboltabelle verwendet werden sollen. Die Voreinstellung dafür ist 8 (d.h. 2 KByte); bei langen Programmen mit vielen INCLUDES ist diese Grenze schnell erreicht.

Wenn der Compiler einen Error 61 (Out of Symbol Space) meldet, dann wird es Zeit, die Symboltabelle auf z.B. 12 Pages zu vergrößern. Der Befehl dazu lautet SET $495=12. Diese Anweisung ist direkt im Monitor zu geben, da die Symboltabelle vor dem Kompiliervorgang eingerichtet wird, so dass ein SET-Befehl im Programm keine Wirkung mehr hat. Hartgesottene Naturen können das natürlich trotzdem tun, müssen aber dann einen Error 61 bei der ersten Kompilierung in Kauf nehmen.

!CODEOFF (Adresse $B5, 2 Bytes)
Mit Hilfe dieser Variablen können Sie Programme für Speicherbereiche schreiben, die während der Kompilierung belegt sind. Dies ist eine wirklich trickreiche und leistungsfähige Einrichtung des Action!-Compilers. Man trägt hierzu einen Offset in die Speicherzellen $B5 und $B6 ein, also einen Wert für den Unterschied zwischen der Adresse, bei der das Programm während des Kompilierens im Speicher abgelegt wird, und der Adresse, ab der es später laufen soll.

Dazu gleich ein Beispiel. Ein Programm für den Speicherbereich ab $A000 soll geschrieben werden. Während des Kompiliervorgangs ist dieser Bereich durch die Action!-Cartridge belegt. Mit den bereits besprochenen SET-Anweisungen legt man das Programm zunächst an die Adresse $8000 und setzt CODEOFF auf $2000. Es wird nun so kompiliert, dass es an der Adresse $A000 (=$8000 + $2000) lauffähig ist.

Wie das in der Praxis aussieht, zeigt Ihnen Listing 1. Wenn Sie dieses Programm mit W auf Diskette schreiben, wird es unter DOS übrigens genau an die Stelle geladen, an der es lauffähig ist.

Bei solchen Programmen darf man natürlich nicht auf die ROM-Bibliothek des Action!-Moduls zurückgreifen (kein PRINT, POKE usw., keine Funktionen mit mehr als 3 Byte Parameter), oder es ist das Runtime-Modul zu verwenden.

Damit wollen wir das Action!-Center für heute beschließen. Ich hoffe, Sie haben etwas interessantes gefunden, und würde mich freuen, wenn Sie das nächste Mal wieder dabei sind.
----
!Listing in Action!
Dieses Listing demonstriert, wie Speicherbereiche genutzt werden können,
die bei der Kompilierung gar nicht zur Verfügung stehen.
{{{
;************************************
;Beispiel zur Steuerung der
;Codeerzeugung bei ACTION!
;
;Programm kompilieren und im Monitor
;abspeichern, dann Steckmodul
;entfernen und mit DOS laden. Das
;Pgm wird dann an die Adresse $A000
;geladen (wo sich vorher das 
;ACTION!-Steckmodul befand).
;************************************

BYTE WSYNC =$D40A,
     VCOUNT=$D40B,
     COLBK =$D01A‚
     RTCLK =$14‚
     SDMCTL=$022F
;
; Programm ab $8000 ablegen
;
SET $0E =$8000
SET $491=$8000
;
; Offset zur Adresse $A000
;
SET $B5 =$2000
;
PROC TEST()

SDHCTL=0
  DO
    WSYNC=0
    COLBK=RTCLK-VCOUNT
  OD
RETURN
```
---
PDF: [act3.pdf](attachments/act3.pdf)  
  
  
