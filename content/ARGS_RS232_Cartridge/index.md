### Arbeiten mit dem Atari Bus - Teil 4 - RS-232 Modul  
  
von Rohland Büher, ABBUC Regionalgruppe Stuttgart (ARGS), Februar 1994  
  
Disketten:  
  
- [argsrs1.atr](attachments/argsrs1.atr)  
- [argsrs2.atr](attachments/argsrs2.atr)  
- [argsrs3.atr](attachments/argsrs3.atr)  
  
## RS 232-Modul  
  
Diesmal wenden wir uns einem anderen Baustein  
zu. Er trägt die Bezeichnung 6551 und heißt "ACIA"  
  
Er ist ebenfalls ein Peripheriebaustein Für die 65-er CPU und wird zur  
seriellen Datenübertragung eingesetzt. Er hat wie die PIA vier Register  
und übernimmt alle nötigen Funktionen für die, Datenübertragung.  
  
Bauteile  
  
| 1 | ACIA 6551(A) + Quarz 1.8432 |  
| 1 | MAX 232 (oder Ersatz-Typ) |  
| 4 | Elko 22 MikroF |  
  
## Bauplanbeschreibung und Bedienung  
  
![](attachments/ARGSRS232.png)  
Bauplan in voller Größe in den Anhängen!  
  
Die Schaltung lehnt sich teilweise an das RS232-Interface des  
Atari-Magazins an (Atari Magazin 12/88). Dort sind auch weitere  
Informationen über Funktion und Programmierung des Bausteins zu finden.  
Geändert wurde die Steueradresse. Außerdem wurde auf drei  
Hardwarehandshake-Leitungen (DTR, DSR, DCD) verzichtet. Das alles  
vereinfacht die Schaltung ungemein und ermöglicht den Einbau in ein  
Modulgehäuse für den Modulschacht  
  
Die IRQ-Leitung läßt sich am Modulschacht leider nicht abfragen. Aber der  
Baustein hat ein Register, in dem ein ausgelöster Interrupt  
softwaremäßig angezeigt wird. So kann man über einen externen Interrupt  
(VBI, DLI, Pokey) dieses Register abfragen und so auf den  
Hardwareinterrupt verzichten.  
  
Nullmodenbetrieb: Die Standard-Leitungen Für eine serielle  
Datenübertragung  sind  
  
| TxD  | Datensenden |  
| RxD  | Datenempfang  Masse/Ground |  
  
Alle Informationen werden über diese Leitungen ausgetauscht.  
  
Es ist nur ein sogenanntes Softwarehandshake möglich. Dies geschieht  
normalerweise über die Befehle  
  
- XON (17, CTRL-Q) = Datenempfang möglich  
- XOFF (19, CTRL-S) = kein Datenempfang möglich  
  
Achtung: Man muß beim ARGS-RS-232 Modul zusätzlich die Leitungen RTS und  
CTS- miteinander verbinden Beim PC oder anderen Rechnern muß u.U. auch  
noch DSR, DTR, DCD miteinander verbunden werden.  
  
Standard für den Atari XL/XE ist der Befehlssatz des 850er Interfaces  
Eine billige Alternative ist das Datari-Kabel das ein einfaches  
Nullmodemkabel darstellt und für diesen Einsatz kompatibel zum 850er  
ist. Der Handler für das ARGS-Interface ist (bisher nur) teilweise  
kompatibel zum 850er.  
  
Man muß beim Datenaustausch immer bedenken, daß der Atari für Return den  
Wort 155 hat und nicht 13 (=> Wandlung !!!)  
  
## Software Für das RS-232-Modul  
  
Was man dazu braucht ist schlicht ein R:-Handler Nun hat aber das 850-er  
Interface einen Standard vorgegeben, an den man sich halten sollte.  
Deswegen muß der Handler nicht nur mit dem ACIA-Baustein umgehen können,  
sondern muß auch die Befehle des 850-er Interfaces verstehen. Das macht  
die Sache leider etwas komplizierter, aber nicht unmöglich.  
  
Nun zur Software:  
  
- ARGSRS2.** R:-Handler mit hoher Kompatibilität zum 850-er Interface.  
Neue Version, Stand Juli 1994. Steht ab $2000 im Speicher und legt MEMLO  
hoch  
- ARGSRSM** (M=Mini) Auf das Nötigste reduzierter R:-Handler. Nur  
Veränderung der Baud-Festeinstellung von Wortlänge (8 Bit), Parität  
(keine) und Stopbits (1). Nur Hardwarehandshake und keine  
Zeichenwandlung von 155 in 13. Reicht aber z.B. für <nop>BobTerm völlig. Steht  
auch ob $2000 im Speicher.  
- ARGSRSRE.COM (RE=RElocobel) Relocierbarer R:-handler (ARGSRSM s.o.),  
der sich ob MEMLOW in den Speicher legt und dann MEMLOW entsprechend  
erhöht.  
  
Weiche Programme laufen nun mit diesen Handlern? Pur jeden Fall alle die  
das 850-er Interface, voraussetzen und die Handler Sauber abfragen und  
nicht irgendwie direkt einspringen, d.h.	Buffer direkt auslesen. Es  
funktionieren:  
  
- BOBTERM (vermutlich alle Versionen)  
- OMNICOM  
- Kermit (K65V37NR.COM)  
  
Es funktionieren nicht  
  
- ANSITERM (hat wohl keinen echten R:-Handler)  
  
## Steueraddressen  
  
Steueradressen: (CCTL + A3)  
---
  
|| ACIA  || Aufgabe	||  Atari-Bus (Modulschacht)  
| DATA	  | Ein-/Ausgabe  | $D508/54536  
| STATUS	| IRQ, Fehler, DSR, DCD  | $D509/54537  
| COMMAND  | Parität, Echo, IRQ, RTS | $D50A/54538  
| DATA	  | Baud, Stopbit, Wortlänge | $D5OB/54539  
  
---
  
## Platinen Layout ( Main.GuusAssmann )  
  
für die ARGS RS-232 Cart  
  
## Treiber Quellen  
  
### ARGSRS.SRC  
```
***		 RS 232 HANDLER			 ***
*** Fuer A.R.G.S. RS232 Interface ***
***	Mit Pokey-Timer-Interrupt	***
***		  Version 1.23			  ***
***		von Sven Traenkle		  ***

			ORG $2000,$A800

ACDATA	EQU $D508
ACSTAT	EQU $D509
ACCOMM	EQU $D50A
ACCONT	EQU $D50B


DOSINI	EQU $C
DOSVEC	EQU $A
COLOR1	EQU 709
COLOR2	EQU 710
COLOR4	EQU 712
MEMLO	 EQU 743
ICAX1Z	EQU $2A
ICAX2Z	EQU $2B
ICCOMZ	EQU $22
BRKKEY	EQU 17
POKMSK	EQU 16
DVSTAT	EQU 746

PHENTV	EQU $E486
IRQEN	 EQU $D20E
AUDF1	 EQU $D200
KBCODE	EQU $2FC
VTIMR1	EQU 528
STIMER	EQU 53769


*************************
* Jetzt gehts los !!!	*
*************************

PROT	  DFB 2 *+0
STOP	  DFB 19 *+1
CONT	  DFB 17 *+2
FULLFL	DFB 0 *+3
DATABRK  DFB 0 *+4
ERR		DFB 0 *+5
STAT	  DFB 0 *+6
CHECK	 DFB 0 *+7
OFF		DFB 0 *+8
RWFL	  DFB 0 *+9
NOCHR	 DFB 1 *+A
TRANS	 DFB 1 *+B

IIN		DFB 0 *+C
IOUT	  DFB 0 *+D
OIN		DFB 0 *+E
OOUT	  DFB 0 *+F


INIT	  LDA #END:L
			STA MEMLO
			LDA #END:H
			STA MEMLO+1


*** TREIBER IN TABELLE EINTRAGEN

			LDX #'R 
			LDA #TAB:H
			LDY #TAB:L
			SEC
			JSR PHENTV
			BCC OKA
			RTS ; EINTRAG NICHT ERFOLGREICH
OKA		LDA #5
			STA COLOR4


*** VOREINSTELLUNGEN

			LDA #9
			STA ACCOMM
			LDA #23
			STA ACCONT
			RTS

TAB		DFW OPEN-1
			DFW CLOSE-1
			DFW GET-1
			DFW PUT-1
			DFW STATUS-1
			DFW SPECIAL-1
			JMP OKA


***  HANDLERROUTINEN ***

************
*** OPEN ***
************

OPEN	  LDY #1
			LDA ICAX1Z
			STA RWFL
			LDA #$00
			STA IIN
			STA IOUT
			STA OIN
			STA OOUT


*** POKEY-INT. INIT:

			LDA POKMSK
			ORA #$01
			STA POKMSK
			STA IRQEN
			LDA FREQ
			STA AUDF1
			LDA #INT:L
			STA VTIMR1
			LDA #INT:H
			STA VTIMR1+1
			LDA #1
			STA STIMER
			JSR AN
			RTS


****************
*** CLOSE	 ***
****************

CLOSE	 LDA #0
			STA OFF
			LDA POKMSK
			AND #$FE
			STA POKMSK
			STA IRQEN
			JSR AUS
			LDY #1
			RTS


****************
*** GET ********
****************

GET		LDA BRKKEY
			BEQ BREAK
			LDA #$00
			STA NOCHR
			LDA IIN
			CMP IOUT
			BNE BUFCHK
			LDA ERR
			BNE ERROR
			LDA RWFL
			CMP #12
			BEQ GET
			LDA #$1
			STA NOCHR
			LDA #$00
			JMP NEXT
BUFCHK	LDA FULLFL
			BEQ GETCHR
			LDA IOUT
			SEC
			SBC IIN
			CLC
			CMP #10
			BNE GETCHR
			JSR AN
			LDA #$0
			STA FULLFL

GETCHR	LDY IOUT
			INC IOUT
			LDA IBUF,Y
*		  PHA
*		  LDA TRANS
*		  BNE NOTRL
*		  PLA
*		  AND #127
*		  CMP #13
*		  BNE NOCR
*		  LDA #155
*NOCR	 PHA
*
*NOTRL	PLA
*
NEXT	  LDY #$1
			RTS

ERROR	 LDA ERR
			AND #1
			BNE PARITY
			LDY #169
			JMP ENDERR
			LDA ERR
			AND #2
			BNE STASTO
OVERRUN  LDY #137
			JMP ENDERR
BREAK	 LDY #128
			INC BRKKEY
			RTS
PARITY	LDY #143
			JMP ENDERR
STASTO	LDY #166
ENDERR	LDA #$00
			STA ERR
			RTS		


**************
*** PUT  *****
**************

PUT		PHA
			LDA ACCOMM
			AND #243
			ORA #4
			STA ACCOMM
PUTL	  LDA BRKKEY
			BEQ BREAK
			LDA OIN
			CLC
			ADC #2
			CMP OOUT
			BEQ PUTL
			LDY OIN
			INC OIN

*		  LDA TRANS
*		  BNE NOTRLA
*			PLA
*			CMP #155
*		  BNE NOEOL
*			LDA #13
*
*NOEOL	AND #127
*		  PHA
*
NOTRLA	PLA
			STA OBUF,Y
			LDY #1
			RTS


********************
*** SPECIAL ********
********************

SPECIAL  LDA ICCOMZ
			CMP #36
			BEQ X36
			CMP #38
			BEQ X38
			LDY #1
			RTS

*** XIO 38 (UEBERSETZUNG, PARITAET)

X38		LDA ICAX1Z
			AND #5
			CMP #5
			BEQ UNGER
			LDA ICAX1Z
			AND #10
			CMP #10
			BEQ GERADE
KEINE	 LDA ACCOMM
			AND #$DF
			STA ACCOMM
			LDY #1
			RTS * JMP TL
UNGER	 LDA ACCOMM
			AND #$3F
			ORA #32
			LDY #1
			RTS
GERADE	LDA ACCOMM
			AND #$7F
			ORA #32
			LDY #1
			RTS
*TL		LDA ICAX1Z
*		  AND #32
*		  BNE NTRANS
*		  LDA #$00
*		  STA TRANS
*		  LDY #1
*		  RTS
*NTRANS  LDA #$01
*		  STA TRANS
*		  LDY #1
*		  RTS


*** XIO 36 (BAUDRATE,WORTLAENGE...)

X36		LDA ICAX1Z
			AND #15
			LDX #0
			JSR COMP
			STX WAITS
			STA HELPFL
			LDA ICAX1Z
			AND #48
			ASL
			ADC HELPFL
			ADC #16
			STA HELPFL
			LDA ICAX1Z
			AND #128
			ADC HELPFL
			STA ACCONT
			STY FREQ
			STY AUDF1
			LDY #1
			RTS
*
COMP	  CMP #9
			BEQ B600
			CMP #10
			BEQ B1200
			CMP #11
			BEQ B1800
			CMP #12
			BEQ B2400
			CMP #13
			BEQ B4800
			CMP #14
			BEQ B9600
			CMP #15
			BEQ B19200
			LDA #6
			LDY #$FF
			RTS
B600	  LDA #7
			LDY #$FF
			RTS
B1200	 LDA #8
			LDY #$FF
			RTS
B1800	 LDA #9
			LDY #$FF
			RTS
B2400	 LDA #10
			LDY #160
			RTS
B4800	 LDA #12
			LDY #80
			RTS
B9600	 LDA #14
			LDY #40
			LDX #2
			RTS
B19200	LDA #15
			LDY #20
			LDX #6
			RTS

HELPFL	DFB 00
FREQ	  DFB 255
WAITS	 DFB 0


****************
*** STATUS  ****
****************

STATUS	LDA #$00
			STA DVSTAT+2
			LDA IIN
			SEC
			SBC IOUT
			STA DVSTAT+1
			LDA OIN
			SEC
			SBC OOUT
			STA DVSTAT+3
			CLC
			LDY #$1
			RTS


*************************************
*  INTERRUPT								*
*************************************

INT		TYA
			PHA
			TXA
			PHA
			LDA ACSTAT
			STA STAT
			AND #128
			BNE ACIA
**
*		  LDA KBCODE
*		  CMP #227 * Taste N mit Shift u. Ctrl.
*		  BNE NON
*		  LDA #0
*		  STA PROT
*NON	  CMP #254 * SHFT.-CTRL. S
*		  BNE NOS
*		  LDA #1
*		  STA PROT
*NOS	  CMP #249 *SHFT.-CTRL. H
*		  BNE BACK
*		  LDA #2
*		  STA PROT
BACK	  PLA
			TAX
			PLA
			TAY
			PLA
			RTI
ACIA	  LDA CHECK
			AND STAT
			BEQ OK
			JMP BACK
OK		 LDA STAT
			AND #8
			BEQ NOTFULL
			JSR REC
NOTFULL  LDA STAT
			AND #16
			BEQ NOTEMPT
			JMP TRANSF
NOTEMPT  JMP BACK

***********************
* Byte in Inputbuffer *
***********************

REC		LDA STAT
			AND #1
			BNE ERRO
			LDA PROT
			CMP #1
			BNE NOSO
			LDA ACDATA
			CMP STOP
			BEQ HALT
			CMP CONT
			BEQ WEITER
			JMP INBUF

NOSO	  LDA ACDATA
INBUF	 LDY IIN
			STA IBUF,Y
			INC IIN
			LDA IOUT
			SEC
			SBC IIN
			CMP #8
			BEQ VOLL
			RTS

VOLL	  JSR AUS
			LDA #1
			STA FULLFL
			RTS

ERRO	  LDA STAT
			AND #1
			STA ERR
			RTS

HALT	  LDA #1
			STA DATABRK
			RTS

WEITER	PHA
			LDA DATABRK
			BEQ INBU
			LDA #0
			STA DATABRK
			PLA
			RTS
INBU	  PLA
			JMP INBUF

******************************
* Byte aus Outputbuffer		*
******************************


TRANSF	LDA WAIT
			BEQ ENDWAIT
			DEC WAIT
			JMP BACK
ENDWAIT  LDA WAITS
			STA WAIT
			LDA DATABRK
			BNE NOTRANS
			LDA OOUT
			CMP OIN
			BNE AUSG
NOTRANS  LDA ACCOMM
			AND #243
			ORA #8
			STA ACCOMM
			LDA OFF
			BNE ZU
			JMP BACK
ZU		 JSR AUS
			JMP BACK

AUSG	  TAY
			LDA OBUF,Y
			STA ACDATA
			INC OOUT
			JMP BACK

WAIT	  DFB 03


***************************
* READY AN SENDER MELDEN  *
***************************

AN		 LDA PROT
			BNE HAND
			RTS
HAND	  CMP #2
			BNE AN1
			LDA ACCOMM
			AND #243
			ORA #8
			STA ACCOMM
			RTS
AN1		LDA ACCOMM
			AND #12
			CMP #4
			BEQ AN2
			LDY #1
			LDA ACCOMM
			AND #243
			ORA #4
			STA ACCOMM
AN2		LDA ACSTAT
			AND #16
			BEQ AN2
			LDA CONT
			STA ACDATA
			CPY #1
			BEQ END2
			LDA ACCOMM
			AND #243
			ORA #8
			STA ACCOMM
END2	  RTS


**************************
* NICHT READY MELDEN	  *
**************************

AUS		LDA PROT
			BNE HAND1
			RTS
HAND1	 CMP #2
			BNE AUS1
			LDA ACCOMM
			AND #243
			STA ACCOMM
			RTS
AUS1	  LDA ACCOMM
			AND #12
			CMP #4
			BEQ AUS2
			LDY #1
			LDA ACCOMM
			AND #243
			ORA #4
			STA ACCOMM
AUS2	  LDA ACSTAT
			AND #16
			BEQ AUS2
			LDA STOP
			STA ACDATA
			CPY #1
			BEQ ENDE
			LDA ACCOMM
			AND #243
			ORA #8
			STA ACCOMM
ENDE	  RTS


*******************
*** BUFFER		 **
*******************

IBUF	  ASC '********************************'
			ASC '  A.R.G.S. (Atari Regionalgruppe'
			ASC ' Stuttgart) is the best !!!	  '
			ASC '********************************'
			ASC '										  '
			ASC 'ARGS-RS 232 Handler (p)1992/93  '
			ASC 'Sven Traenkle (mit mehr oder wen'
			ASC 'iger grosser Unterstuetzung von '
			DFB 255
OBUF	  ASC 'Roland Buehler, Holger Pfeil, Pe'
			ASC 'ter Straif, Star Trek - The next'
			ASC ' Generation, Al Bundy und seiner'
			ASC ' schrecklich netten Familie, der'
			ASC 'Lindenstrasse, 21st Century Digi'
			ASC 'tal Boy, Ramones, Coca Cola, Stu'
			ASC 'ttgarter Hofbraeu, Bofrost,Wing '
			ASC 'Com.II und meinem genialen Hirn.'
END		DFB 255
```
  
### ARGSRS2.SRC  
```
***		 RS 232 HANDLER			 ***
*** Fuer A.R.G.S. RS232 Interface ***
***	Mit Pokey-Timer-Interrupt	***
***		  Version 1.23			  ***
***		von Sven Traenkle		  ***
*** modifiziert v. RoBue 23.08.94 ***

			ORG $2000,$A800

ACDATA	EQU $D508
ACSTAT	EQU $D509
ACCOMM	EQU $D50A
ACCONT	EQU $D50B


DOSINI	EQU $C
DOSVEC	EQU $A
COLOR1	EQU 709
COLOR2	EQU 710
COLOR4	EQU 712
MEMLO	 EQU 743
ICAX1Z	EQU $2A
ICAX2Z	EQU $2B
ICCOMZ	EQU $22
BRKKEY	EQU 17
POKMSK	EQU 16
DVSTAT	EQU 746

PHENTV	EQU $E486
IRQEN	 EQU $D20E
AUDF1	 EQU $D200
KBCODE	EQU $2FC
VTIMR1	EQU 528
STIMER	EQU 53769


*************************
* Jetzt gehts los !!!	*
*************************

PROT	  DFB 2 *+0
STOP	  DFB 19 *+1
CONT	  DFB 17 *+2
FULLFL	DFB 0 *+3
DATABRK  DFB 0 *+4
ERR		DFB 0 *+5
STAT	  DFB 0 *+6
CHECK	 DFB 0 *+7
OFF		DFB 0 *+8
RWFL	  DFB 0 *+9
NOCHR	 DFB 1 *+A
TRANS	 DFB 1 *+B

IIN		DFB 0 *+C
IOUT	  DFB 0 *+D
OIN		DFB 0 *+E
OOUT	  DFB 0 *+F


INIT	  LDA #END:L
			STA MEMLO
			LDA #END:H
			STA MEMLO+1


*** TREIBER IN TABELLE EINTRAGEN

			LDX #'R 
			LDA #TAB:H
			LDY #TAB:L
			SEC
			JSR PHENTV
			BCC OKA
			RTS ; EINTRAG NICHT ERFOLGREICH
OKA		LDA #5
			STA COLOR4


*** VOREINSTELLUNGEN

			LDA #9
			STA ACCOMM
			LDA #23
			STA ACCONT
			RTS

TAB		DFW OPEN-1
			DFW CLOSE-1
			DFW GET-1
			DFW PUT-1
			DFW STATUS-1
			DFW SPECIAL-1
			JMP OKA


***  HANDLERROUTINEN ***

************
*** OPEN ***
************

OPEN	  LDY #1
			LDA ICAX1Z
			STA RWFL
			LDA #$00
			STA IIN
			STA IOUT
			STA OIN
			STA OOUT


*** POKEY-INT. INIT:

			LDA POKMSK
			ORA #$01
			STA POKMSK
			STA IRQEN
			LDA FREQ
			STA AUDF1
			LDA #INT:L
			STA VTIMR1
			LDA #INT:H
			STA VTIMR1+1
			LDA #1
			STA STIMER
			JSR AN
			RTS


****************
*** CLOSE	 ***
****************

CLOSE	 LDA #0
			STA OFF
			LDA POKMSK
			AND #$FE
			STA POKMSK
			STA IRQEN
			JSR AUS
			LDY #1
			RTS


****************
*** GET ********
****************

GET		LDA BRKKEY
			BEQ BREAK
			LDA #$00
			STA NOCHR
			LDA IIN
			CMP IOUT
			BNE BUFCHK
			LDA ERR
			BNE ERROR
			LDA RWFL
			CMP #12
			BEQ GET
			LDA #$1
			STA NOCHR
			LDA #$00
			JMP NEXT
BUFCHK	LDA FULLFL
			BEQ GETCHR
			LDA IOUT
			SEC
			SBC IIN
			CLC
			CMP #10
			BNE GETCHR
			JSR AN
			LDA #$0
			STA FULLFL
*
GETCHR	LDY IOUT
			INC IOUT
			LDA IBUF,Y
			PHA
			LDA TRANS
			BNE NOTRL
			PLA
			AND #127
			CMP #13
			BNE NOCR
			LDA #155
NOCR	  PHA
*
NOTRL	 PLA
*
NEXT	  LDY #$1
			RTS

BREAK	 LDY #128
			INC BRKKEY
			RTS
ERROR	 LDA #$00
			STA ERR
			LDY #163
			RTS		


**************
*** PUT  *****
**************

PUT		PHA
			LDA ACCOMM
			AND #243
			ORA #4
			STA ACCOMM
PUTL	  LDA BRKKEY
			BNE PUTLL
			PLA
			JMP BREAK
PUTLL	 LDA OIN
			CLC
			ADC #2
			CMP OOUT
			BEQ PUTL
			LDY OIN
			INC OIN
*
			LDA TRANS
			BNE NOTRLA
			PLA
			CMP #155
			BNE NOEOL
			LDA #13
*
NOEOL	 AND #127
			PHA
*
NOTRLA	PLA
			STA OBUF,Y
			LDY #1
			RTS


********************
*** SPECIAL ********
********************

SPECIAL  LDA ICCOMZ
			CMP #36
			BEQ X36
			CMP #38
			BEQ X38
			LDY #1
			RTS

*** XIO 38 (UEBERSETZUNG, PARITAET)

X38		LDA ICAX1Z
			AND #5
			CMP #5
			BEQ UNGER
			LDA ICAX1Z
			AND #10
			CMP #10
			BEQ GERADE
KEINE	 LDA ACCOMM
			AND #$DF
			STA ACCOMM
			LDY #1
			JMP TL
UNGER	 LDA ACCOMM
			AND #$3F
			ORA #32
			LDY #1
			RTS
GERADE	LDA ACCOMM
			AND #$7F
			ORA #32
			LDY #1
			RTS
TL		 LDA ICAX1Z
			AND #32
			BNE NTRANS
			LDA #$00
			STA TRANS
			LDY #1
			RTS
NTRANS	LDA #$01
			STA TRANS
			LDY #1
			RTS


*** XIO 36 (BAUDRATE,WORTLAENGE...)

X36		LDA ICAX1Z
			AND #15
			LDX #0
			JSR COMP
			STX WAITS
			STA HELPFL
			LDA ICAX1Z
			AND #48
			ASL
			ADC HELPFL
			ADC #16
			STA HELPFL
			LDA ICAX1Z
			AND #128
			ADC HELPFL
			STA ACCONT
			STY FREQ
			STY AUDF1
			LDY #1
			RTS
*
COMP	  CMP #9
			BEQ B600
			CMP #10
			BEQ B1200
			CMP #11
			BEQ B1800
			CMP #12
			BEQ B2400
			CMP #13
			BEQ B4800
			CMP #14
			BEQ B9600
			CMP #15
			BEQ B19200
			LDA #6
			LDY #$FF
			RTS
B600	  LDA #7
			LDY #$FF
			RTS
B1200	 LDA #8
			LDY #$FF
			RTS
B1800	 LDA #9
			LDY #$FF
			RTS
B2400	 LDA #10
			LDY #160
			RTS
B4800	 LDA #12
			LDY #80
			RTS
B9600	 LDA #14
			LDY #40
			LDX #2
			RTS
B19200	LDA #15
			LDY #20
			LDX #6
			RTS

HELPFL	DFB 00
FREQ	  DFB 255
WAITS	 DFB 0


****************
*** STATUS  ****
****************

STATUS	LDA #$00
			STA DVSTAT+2
			LDA IIN
			SEC
			SBC IOUT
			STA DVSTAT+1
			LDA OIN
			SEC
			SBC OOUT
			STA DVSTAT+3
			CLC
			LDA ERR
			STA DVSTAT
			LDY #$1
			RTS


*************************************
*  INTERRUPT								*
*************************************

INT		LDA ACSTAT
			BPL BACK1
			STA STAT
			TYA
			PHA

**
*		  LDA KBCODE
*		  CMP #227 * Taste N mit Shift u. Ctrl.
*		  BNE NON
*		  LDA #0
*		  STA PROT
*NON	  CMP #254 * SHFT.-CTRL. S
*		  BNE NOS
*		  LDA #1
*		  STA PROT
*NOS	  CMP #249 *SHFT.-CTRL. H
*		  BNE BACK
*		  LDA #2
*		  STA PROT

ACIA	  LDA CHECK
			AND STAT
			BEQ OK
			JMP BACK
OK		 LDA STAT
			AND #8
			BEQ NOTFULL
			JSR REC
NOTFULL  LDA STAT
			AND #16
			BEQ BACK
			JMP TRANSF

BACK	  PLA
			TAY
BACK1	 PLA
			RTI

***********************
* Byte in Inputbuffer *
***********************

REC		LDA STAT
			AND #7
			BNE ERRO
			LDA PROT
			CMP #1
			BNE NOSO
			LDA ACDATA
			CMP STOP
			BEQ HALT
			CMP CONT
			BEQ WEITER
			JMP INBUF

NOSO	  LDA ACDATA
INBUF	 LDY IIN
			STA IBUF,Y
			INC IIN
			LDA IOUT
			SEC
			SBC IIN
			CMP #8
			BEQ VOLL
			RTS

VOLL	  JSR AUS
			LDA #1
			STA FULLFL
			RTS

ERRO	  STA ERR
			RTS

HALT	  LDA #1
			STA DATABRK
			RTS

WEITER	PHA
			LDA DATABRK
			BEQ INBU
			LDA #0
			STA DATABRK
			PLA
			RTS
INBU	  PLA
			JMP INBUF

******************************
* Byte aus Outputbuffer		*
******************************


TRANSF	LDA WAIT
			BEQ ENDWAIT
			DEC WAIT
			JMP BACK
ENDWAIT  LDA WAITS
			STA WAIT
			LDA DATABRK
			BNE NOTRANS
			LDA OOUT
			CMP OIN
			BNE AUSG
NOTRANS  LDA ACCOMM
			AND #243
			ORA #8
			STA ACCOMM
			LDA OFF
			BNE ZU
			JMP BACK
ZU		 JSR AUS
			JMP BACK

AUSG	  TAY
			LDA OBUF,Y
			STA ACDATA
			INC OOUT
			JMP BACK

WAIT	  DFB 03


***************************
* READY AN SENDER MELDEN  *
***************************

AN		 LDA PROT
			BNE HAND
			RTS
HAND	  CMP #2
			BNE AN1
			LDA ACCOMM
			AND #243
			ORA #8
			STA ACCOMM
			RTS
AN1		LDA ACCOMM
			AND #12
			CMP #4
			BEQ AN2
			LDY #1
			LDA ACCOMM
			AND #243
			ORA #4
			STA ACCOMM
AN2		LDA ACSTAT
			AND #16
			BEQ AN2
			LDA CONT
			STA ACDATA
			CPY #1
			BEQ END2
			LDA ACCOMM
			AND #243
			ORA #8
			STA ACCOMM
END2	  RTS


**************************
* NICHT READY MELDEN	  *
**************************

AUS		LDA PROT
			BNE HAND1
			RTS
HAND1	 CMP #2
			BNE AUS1
			LDA ACCOMM
			AND #243
			STA ACCOMM
			RTS
AUS1	  LDA ACCOMM
			AND #12
			CMP #4
			BEQ AUS2
			LDY #1
			LDA ACCOMM
			AND #243
			ORA #4
			STA ACCOMM
AUS2	  LDA ACSTAT
			AND #16
			BEQ AUS2
			LDA STOP
			STA ACDATA
			CPY #1
			BEQ ENDE
			LDA ACCOMM
			AND #243
			ORA #8
			STA ACCOMM
ENDE	  RTS


*******************
*** BUFFER		 **
*******************

IBUF	  ASC '********************************'
			ASC '  A.R.G.S. (Atari Regionalgruppe'
			ASC ' Stuttgart) is the best !!!	  '
			ASC '********************************'
			ASC '										  '
			ASC 'ARGS-RS 232 Handler (p)1992/93  '
			ASC 'Sven Traenkle (mit mehr oder wen'
			ASC 'iger grosser Unterstuetzung von '
			DFB 255
OBUF	  ASC 'Roland Buehler, Holger Pfeil, Pe'
			ASC 'ter Straif, Star Trek - The next'
			ASC ' Generation, Al Bundy und seiner'
			ASC ' schrecklich netten Familie, der'
			ASC 'Lindenstrasse, 21st Century Digi'
			ASC 'tal Boy, Ramones, Coca Cola, Stu'
			ASC 'ttgarter Hofbraeu, Bofrost,Wing '
			ASC 'Com.II und meinem genialen Hirn.'
END		DFB 255
```
  
### ARGSRSM.SRC  
```
***		 RS 232 HANDLER			 ***
*** Fuer A.R.G.S. RS232 Interface ***
***	Mit Pokey-Timer-Interrupt	***
***		von Sven Traenkle		  ***
***		  neue Version			  ***
***			 by RoBue				 ***
***			20.08.1994				***


			ORG $2000,$A800

ACDATA	EQU $D508			ACIA-
ACSTAT	EQU $D509			REGISTER
ACCOMM	EQU $D50A
ACCONT	EQU $D50B

DOSINI	EQU $C
DOSVEC	EQU $A
COLOR1	EQU 709
COLOR2	EQU 710
COLOR4	EQU 712
MEMLO	 EQU 743
ICAX1Z	EQU $2A
ICAX2Z	EQU $2B
ICCOMZ	EQU $22
BRKKEY	EQU 17
POKMSK	EQU 16
DVSTAT	EQU 746

PHENTV	EQU $E486
IRQEN	 EQU $D20E
AUDF1	 EQU $D200
KBCODE	EQU $2FC
VTIMR1	EQU 528
STIMER	EQU 53769


*************************
* Jetzt gehts los !!!	*
*************************


INIT	  LDA #END:L		  NEUES
			STA MEMLO			MEMLO
			LDA #END:H		  FESTLEGEN
			STA MEMLO+1


*** TREIBER IN TABELLE EINTRAGEN

			LDX #'R 
			LDA #TAB:H
			LDY #TAB:L
			SEC
			JSR PHENTV
			BCC OKA
			RTS					EINTRAG NICHT ERFOLGREICH
OKA		LDA #5
			STA COLOR4


*** VOREINSTELLUNGEN

			LDA #9				300/8/N/1
			STA ACCOMM
			LDA #23
			STA ACCONT
			RTS

TAB		DFW OPEN-1
			DFW CLOSE-1
			DFW GET-1
			DFW PUT-1
			DFW STATUS-1
			DFW SPECIAL-1
			JMP OKA


***  HANDLERROUTINEN ***

************
*** OPEN ***
************

OPEN	  LDY #0
			STY IIN			  BUFFER
			STY IOUT			 ZURUECK-
			STY OIN			  SETZEN
			STY OOUT
			INY

			LDA POKMSK		  POKEY-
			ORA #$01			 IRQ
			STA POKMSK		  EIN
			STA IRQEN
			LDA FREQ
			STA AUDF1
			LDA #INT:L
			STA VTIMR1
			LDA #INT:H
			STA VTIMR1+1
			LDA #1
			STA STIMER
			JMP AN

****************
*** CLOSE	 ***
****************

CLOSE	 LDA POKMSK		  POKEY-
			AND #$FE			 IRQ
			STA POKMSK		  AUS
			STA IRQEN
			JSR AUS
			LDY #1
			RTS


****************
*** GET ********
****************

GET		LDA BRKKEY		  BREAK?
			BEQ BREAK
			LDA IIN
			CMP IOUT
			BEQ GET
BUFCHK	LDA FULLFL
			BEQ GETCHR
			LDA IOUT
			SEC
			SBC IIN
			CLC
			CMP #10
			BNE GETCHR
			JSR AN
			LDA #$0
			STA FULLFL
GETCHR	LDY IOUT
			INC IOUT
			LDA IBUF,Y
NEXT	  LDY #$1
			RTS

BREAK	 LDY #128
			INC BRKKEY
			RTS


**************
*** PUT  *****
**************

PUT		PHA
			LDA ACCOMM
			AND #243
			ORA #4
			STA ACCOMM
PUT0	  LDA BRKKEY		  BREAK?
			BNE PUT1
			PLA
			JMP BREAK
PUT1	  LDA OIN
			CLC
			ADC #2
			CMP OOUT
			BEQ PUT0
			LDY OIN
			PLA
			STA OBUF,Y
			INC OIN
			LDY #1
			RTS


********************
*** SPECIAL ********
********************

SPECIAL  LDA ICCOMZ
			CMP #36
			BEQ X36
			LDY #1
			RTS


*** XIO 36 (BAUDRATE,WORTLAENGE...)

X36		LDA ICAX1Z
			AND #15
			JSR COMP			 Baudrate u. Pokey-Freq.
			SEI
			PHA
			LDA ACCONT
			AND #%11110000
			STA ICAX1Z
			PLA
			ORA ICAX1Z
			STA ACCONT
			STY FREQ
			STY AUDF1
			CLI
			LDY #1
			RTS
*
*		  AKKU: Baudrate
*		  YREG: IRQ-Frequenz
COMP	  CMP #10
			BEQ B1200
			CMP #12
			BEQ B2400
			CMP #13
			BEQ B4800
			CMP #14
			BEQ B9600
			CMP #15
			BEQ B19200
			LDA #6				300/8/N/1 
			LDY #$FF
			RTS
B1200	 LDA #8
			LDY #$FF
			RTS
B2400	 LDA #10
			LDY #160
			RTS
B4800	 LDA #12
			LDY #80
			RTS
B9600	 LDA #14
			LDY #40
			RTS
B19200	LDA #15
			LDY #20
			RTS


****************
*** STATUS  ****
****************

STATUS	LDA #$00
			STA DVSTAT+2
			LDA IIN
			SEC
			SBC IOUT
			STA DVSTAT+1
			LDA OIN
			SEC
			SBC OOUT
			STA DVSTAT+3
			CLC
			LDY #$1
			RTS


*************************************
*  INTERRUPT								*
*************************************

INT		LDA ACSTAT
			BPL BACK1
			STA STAT
			TYA
			PHA

ACIA	  LDA STAT
			AND #8
			BEQ NOTFULL
			JSR REC
NOTFULL  LDA STAT
			AND #16
			BEQ BACK
			JSR TRANSF

BACK	  PLA
			TAY
BACK1	 PLA
			RTI

***********************
* Byte in Inputbuffer *
***********************

REC		LDA STAT
			AND #%00000111
			BEQ NOSO
			LDA ACDATA
			RTS
NOSO	  LDA ACDATA
INBUF	 LDY IIN
			STA IBUF,Y
			INC IIN
			LDA IOUT
			SEC
			SBC IIN
			CMP #8
			BEQ VOLL
			RTS

VOLL	  JSR AUS
			LDA #1
			STA FULLFL
			RTS

******************************
* Byte aus Outputbuffer		*
******************************


TRANSF	LDA DATABRK
			BNE NOTRANS
			LDA OOUT
			CMP OIN
			BNE AUSG
NOTRANS  JMP AUS

AUSG	  TAY
			LDA OBUF,Y
			STA ACDATA
			INC OOUT
			RTS

***************************
* READY AN SENDER MELDEN  *
***************************

AN		 LDA ACCOMM
			AND #243
			ORA #8
			STA ACCOMM
			RTS


**************************
* NICHT READY MELDEN	  *
**************************

AUS		LDA ACCOMM
			AND #243
			STA ACCOMM
			RTS


*************************
* VARIABLE ETC.			*
*************************


FULLFL	DFB 0
DATABRK  DFB 0
STAT	  DFB 0 
FREQ	  DFB 255

IIN		DFB 0
IOUT	  DFB 0
OIN		DFB 0
OOUT	  DFB 0


*******************
*** BUFFER		 **
*******************

IBUF	  ASC '********************************'
			ASC '  A.R.G.S. (Atari Regionalgruppe'
			ASC ' Stuttgart) is the best !!!	  '
			ASC '********************************'
			ASC '										  '
			ASC 'ARGS-RS 232 Handler (p)1992/93  '
			ASC 'Sven Traenkle (mit mehr oder wen'
			ASC 'iger grosser Unterstuetzung von '
			DFB 255
OBUF	  ASC 'Roland Buehler, Holger Pfeil, Pe'
			ASC 'ter Straif, Star Trek - The next'
			ASC ' Generation, Al Bundy und seiner'
			ASC ' schrecklich netten Familie, der'
			ASC 'Lindenstrasse, 21st Century Digi'
			ASC 'tal Boy, Ramones, Coca Cola, Stu'
			ASC 'ttgarter Hofbraeu, Bofrost,Wing '
			ASC 'Com.II und meinem genialen Hirn.'
END		DFB 255
```
  
