# ARGS ISA PC Interface  
  
by Roland Buehler  
  
  
## PROGRAMME FUER ATARI-PC-INTERFACE  
  
Es gibt inzwischen 2 Versionen des PC-Interfaces:  
- alte Version mit Steueradressen im Bereich von $D500  
- neue Version mit einem 74LS138 Baustein zusaetzlich mit den Steueradressen im Bereich von $D100. Dies geht aber nur, wenn die ROM-Disk ebenfalls mit einem 74LS138 genauer auscodiert wird.  
  
```
Adressen:

-------------------------
Aufgabe  alt       neu   
-------------------------
ADRL     $D540     $D118
ADRH     $D541     $D119
ADRS     $D520     $D114
DATEN    $D521     $D115
MEMW     $D522     $D116
MEMR     $D523     $D117
IOW      $D542     $D11A
IOR      $D543     $D11B
```
  
- HERCDRV5.COM - H:-Handler fuer Herculeskarte ($D500)  
- EHANDLER.COM - E:-Handler fuer Herculeskarte ($D500). Ueberschreibt den urspruenglichen im Atari und ermoeglicht so 80 Zeichendarstellung bei allen Programmen, die auf den E:-Handler zugreifen (Basic, Turbobasic, DOS).  
- HERCUL.BAS - Beispielprogramm in Basic wie man das Interface programmiert. Es wird die Herculeskarte fuer Text initialisiert.  
- MFM.BAS - Liest die Register eines MFM-Controllers aus.  
- PCINTER.SRC - Alle Routinen zum Betreiben des Interfaces in ATMAS II  
- PCPRINT.COM/SRC - P:-Handler fuer Druckerport der Herculeskarte.  
- PCRESET - Resetroutine fuer Interface. Ist bei manchen PC-Karten notwendig vor Initialisierung.  
- HERC*.SRC/COM ($D100) Einfacher Handler fuer Herculeskarte. Er installiert einen H:-Handler oder ueberschreibt den P:-Handler. Kann auch inverse Zeichen darstellen. Moeglichkeit von Statuszeilen. Ueber HELP und SHIFT+HELP laesst sich Scrollen aus- und einschalten.  
- HERCD114.COM - Verbesserter H:-Handler mit schnelleren Routinen (von Ralf David). Er setzt die neuen Steueradressen voraus.  
- HtoE.SRC/COM Ueberschreibt E:-Handler und ersetzt ihn durch den H:-Handler  
- PCTEST*.TUR - Programm zum Durchtesten der IO-Adressen von PC-Karten. Eine Version fuer $D500 und eine fuer $D100.  
  
RoBue  
