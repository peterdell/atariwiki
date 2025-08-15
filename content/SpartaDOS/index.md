---
title: SpartaDOS
---
# SpartaDOS  
  
  
  
SpartaDOS is a completely different command-line DOS modelled after MS-DOS, though it is perfectly capable of reading all Atari DOS and MyDOS disks. There are many versions available. Hopefully this list will help keep them all straight. SpartaDOS X is further developed via the [SpartaDOS X Upgrade Project](http://sdx.atari8.info/index.php)  
  
__Hint: In emulators please choose: 'No PBI Expansion', otherwise SpartaDOS may not work correct.__  
  
DOS 2 Equivalents:  
The following is a list of the commands from the AtariDOS 2.0S menu and their equivalents in SpartaDOS X:  
A-DISK DIRECTORY __DIR and DIRS__  
B-RUN CARTRIDGE __BASIC for internal BASIC in XL/XE computers, CAR for an external cartridge__  
C-COPY FILE __COPY__  
D-DELETE FILE __ERASE, DELETE or DEL__  
E-RENAME FILE __RENAME or REN__  
F-LOCK FILE __ATR +P__  
G-UNLOCK FILE __ATR -P__  
H-WRITE DOS __not needed - SDX boots from cartridge__  
I-FORMAT DISK __FORMAT__  
J-DUPLICATE DISK __COPY or MENU__  
K-BINARY SAVE __SAVE__  
L-BINARY LOAD __program name, LOAD__  
M-RUN AT ADDRESS __External command RUN from SDXTK__  
N-CREATE MEM.SAV __SET CAR and SET BASIC__  
O-DUPLICATE FILE __MENU__  
  
## CAR Images  
- [SpartaDOS_X_4.22.car](attachments/SpartaDOS_X_4.22.car) ; size: 64 KB  
- [SpartaDOS_X_4.48.car](attachments/SpartaDOS_X_4.48.car) ; size: 128 KB  
  
## ROM Images  
- [SpartaDOS_X_4.21.rom](attachments/SpartaDOS_X_4.21.rom) ; size: 64 KB  
- [SpartaDOS_X_4.22.rom](attachments/SpartaDOS_X_4.22.rom) ; size: 64 KB  
  
## ATR Images  
- [SpartaDOS_3.2g_with_DOS.atr](attachments/SpartaDOS_3.2g_with_DOS.atr) ; SpartaDOS 3.2g formatted SSSD disk with just SpartaDOS (bootable); size: 92 KB  
- [SpartaDOS_3.2g.atr](attachments/Spartados_3.2g.atr) ; SpartaDOS 3.2g Master Disk; size: 92 KB  
- [SpartaDOS_3.2g_720K.atr](attachments/SpartaDOS_3.2g_720K.atr) ; SpartaDOS 3.2g Master Disk; size: 720 KB  
- [SpartaDOS_3.2g_720K_empty.atr](attachments/SpartaDOS_3.2g_720K_empty.atr) ; SpartaDOS 3.2g formatted, no DOS; size: 720 KB  
- [SpartaDOS_X_4.48_92K_empty.atr](attachments/SpartaDOS_X_4.48_92K_empty.atr) ; SpartaDOS X 4.48 formatted, SSSD, no DOS; size: 92 KB  
- [SpartaDOS_X_4.48_720K_empty.atr](attachments/SpartaDOS_X_4.48_720K_empty.atr) ; SpartaDOS X 4.48 formatted, no DOS; size: 720 KB  
- [720K_SpartaDOS.atr](attachments/720K_SpartaDOS.atr) ; blank formatted disk ; size: 720 KB  
  
## Manual  
- [SpartaDOS_X_4.48_User_Guide.pdf](attachments/SpartaDOS_X_4.48_User_Guide.pdf) ; size: 4.5 MB ; OCR ; thanks to: [SpartaDOS X Upgrade Project](http://sdx.atari8.info/index.php), highly appreciated! :-)  
  
## SpartaDOS 3.2g and 3.2gx - Dated 6/4/94.  
  
Last official disk-based versions, released as shareware by Fine Tooned  
Engineering (FTe), who had purchased the rights from ICD.  3.2g is the primary  
version; 3.2gx differs only in that it locates the disk buffers under the OS  
to save RAM.  3.2gx is intended for use in systems that include a PBI device  
(MIO, Black Box); it is not compatible with BASIC XE or any other programs  
using RAM under the OS.  
  
First shareware release from FTe: 3.2f.  
  
Earlier major releases from the original developer, ICD: 3.2d, 3.2c, 2.3, 1.1  
  
Only the SDX cartridges and the original version 1.1 are compatible with the  
400/800 computer models; SpartaDOS 2.x, and 3.x require an XL/XE.  
  
Many disk-based SpartaDOS versions are available for download here,  
Thunderdome, kept by SysOp Fox-1:  
[http://www7.brinkster.com/atari/ataridl/sdsys.htm](http://www7.brinkster.com/atari/ataridl/sdsys.htm)  
  
One source of SpartaDOS documentation is Russ Gilbert's page at:  
[http://my.en.com/~russg/](http://my.en.com/~russg/)  
  
## SpartaDOS Pro 3.3a, 3.3b, and 3.3c - 1994-  
  
The SpartaDOS Pro 3.3 versions were developed by Stephen J. Carden, based upon  
a dissembled copy of the older (more stable?) 3.2c release from ICD.  
- SpartaDOS Pro Ver 3.3a  3-Nov-94 -- Added MUX support and MS-DOS Commands. Highspeed SIO routines NOT included.  Recommended for use in emulators (especially Xformer) only.  
- SpartaDOS Pro Ver 3.3b 25-Dec-95 -- Has two different SIOV handlers, one for the MUX and one for the MIO.  
- SpartaDOS Pro Ver 3.3c  1995 -- Looks at your system and by checking it determines what CIO handler to load, and has MS-DOS command set.  Black Box, MUX, and MIO are fully supported, though none of these are required.  
- SpartaDOS Pro Ver 3.3c 19-Dec-97 -- the same 3.3c produced on a 16K ROM cartridge by Video 61.  
- SpartaDOS Pro Ver 3.3d -- exists, but is not in general release  
  
According to Lance Ringquist:  
K-Products contracted FTe to develop SpartaDOS Pro 3.3 for exclusive use and  
distribution with K-Products' BBS Express! Pro, to provide this BBS system  
with the most stable platform possible.  As Video 61 now owns the rights to  
BBS Express! Pro, SpartaDOS Pro 3.3 is therefore now a product of Video 61.  
  
According to Stephen Carden:  
The SpartaDOS Pro 3.3 versions were never owned by K-Products, and are  
technically shareware owned by FTe, although FTe had no connection with the  
specific development of the 3.3 versions.  
  
## SpartaDOS X (SDX) cartridge  
  
Greatly enhanced/expanded compared to disk- based SpartaDOS; completely  
different source code. Several versions produced:  
  
||Version||Datei||vendor||  
|  4.22  | 11-05-95  | released by Fine Tooned Engineering (FTe) |  
|  4.21  | 7-10-89   | released by ICD |  
|  4.20  | 2-06-89   | released by ICD |  
|  4.19  | 1-16-89   | released by ICD |  
|  4.18  | 10-29-88  | released by ICD |  
|  4.17  |  ?-?-88   | released by ICD |  
  
## References  
- [SpartaDOS X @ Wikipedia](https://en.wikipedia.org/wiki/SpartaDOS_X)  
- [Sparta DOS X Review](../SpartaDosXReview/index.md)  
  
# Deutsch  
  
## Sparta-DOS 3.2x  
- Hersteller: ursprünglich ICD, später hat FTE die Rechte davon erworben und sich dann leider "aus dem Staub gemacht".  
- Umfang: Das DOS besteht aus einem File X32x.DOS und ist DOS 2.x inkompatibel. Atari-DOS 2.x Formate können aber intern gelesen und angezeigt werden. Ein Programm kann via Batchfile-Verarbeitung (ein einfach selbst zu erstellendes Textfile mit dem Namen STARTUP.BAT) automatisch geladen werden. Eine XE-Ramdisk wird via externem Treiber bis zu einer Größe von 1024k unterstützt (der Treiber muss aber entweder manuell oder via Batchfile geladen werden). Wurde u.a. im ABBUC-Magazin released und upgedatet.  
- DOS-Menü: Nein! Das DOS ist Kommando-orientiert! Es gibt keine eingebaute Befehlsübersicht, d.h. die Kommandos muss man kennen oder im Manual nachschlagen;  
- Formate: alle möglichen und unmöglichen Formate, Single, Enhanced und Double; single-sided und double-sided; 35 Tracks, 40 Tracks, 77 Tracks und 80 Tracks; High Density...  
- Sub-Directories: Ja!  
- Harddisk-Partitionen: Ja, bis 16MB!  
- Aux.: /N /A  
- max. Anzahl von Drives: 9 (als D1: bis D9:);  
- Dir.-Einträge: max. 1024? ;  
- RAM unter dem OS: wird vollständig genutzt, ergo lassen sich damit keine Programme (z.B. TB XL ) oder Treiber (z.B. XL-RD) laden, die ebenfalls diesen Speicherplatz verwenden...  
- DOS 2.0 kompatibel: SD = nein, DD = nein, da eigenes "Sparta-Format"  
- DOS 2.5 kompatibel: ED = nein, da eigenes "Sparta-Format" (via MENU.COM können SD/ED/DD Files aber ins Atari DOS 2.x oder ins Sparta-Format konvertiert werden)  
- Speeder-Treiber: es ist ein ultraspeed treiber vorhanden, der Happy, Speedy und US Doubler (und kompatible Laufwerke) unterstützt; für XF551 und Turbo existieren keine Speeder;  
Anmerkung: die letzte offizielle Version war 3.2g; Sparta-DOS bietet eine Datums- und Zeit- Funktion; für den Betrieb mit einer XF551 muss das DOS und/oder der Formatter (XINIT.COM) gepatcht werden, da man sonst beim Booten immer die Nachricht "Error - no DOS!" erhält. Dazu sind mehrere Patch-Programme erhältlich...  
  
## Sparta DOS 3.3x  
- Hersteller bzw. Autor war Stephen J. Carden  
Es existieren die Varianten 3.3a, 3.3b und 3.3c. Diese Versionen von Sparta-DOS wurden speziell für den Betrieb von Mailboxen mit dem Programm BBS-Express-Pro hergestellt. Es gibt nach wie vor Diskussionen darüber, wer der offizielle Rechte-Inhaber von 3.3x ist. Das DOS besteht aus einem File X33x.DOS und ist zu Atari DOS 2.x inkompatibel; Atari-DOS 2.x Formate können aber intern gelesen und angezeigt werden. Ein Programm kann via Batchfile-Verarbeitung (ein einfach selbst zu erstellendes Textfile mit dem Namen STARTUP.BAT) automatisch geladen werden. Eine XE-Ramdisk wird via externem Treiber bis zu einer Größe von 1024k unterstützt (der Treiber muss aber entweder manuell oder via Batchfile geladen werden).  
- DOS-Menü: Nein! Das DOS ist Kommando-orientiert! Es gibt keine eingebaute Befehlsübersicht, d.h. die Kommandos muss man kennen oder im Manual nachschlagen;  
- Formate: alle möglichen und unmöglichen Formate, Single, Enhanced und Double; single-sided und double-sided; 35 Tracks, 40 Tracks, 77 Tracks und 80 Tracks; High Density...  
- Sub-Directories: Ja!  
- Harddisk-Partitionen: Ja, bis 16MB!  
- Aux.: /N /A  
- max. Anzahl von Drives: 9 (als D1: bis D9:);  
- Dir.-Einträge: max. 1024? ;  
- RAM unter dem OS: wird vollständig genutzt, ergo lassen sich damit keine Programme (z.B. TB XL ) oder Treiber (z.B. XL-RD) laden, die ebenfalls diesen Speicherplatz verwenden...  
- DOS 2.0 kompatibel: SD = nein, DD = nein, da eigenes "Sparta-Format"  
- DOS 2.5 kompatibel: ED = nein, da eigenes "Sparta-Format" (via MENU.COM können SD/ED/DD Files aber ins Atari DOS 2.x oder ins Sparta-Format konvertiert werden)  
- Speeder-Treiber: es ist ein ultraspeed treiber vorhanden, der Happy, Speedy und US Doubler (und kompatible Laufwerke) unterstützt; für XF551 und Turbo existieren keine Speeder;  
- Anmerkung: die letzte offizielle Version war 3.3c; Sparta-DOS bietet eine Datums- und Zeit- Funktion; für den Betrieb mit einer XF551 muss das DOS und/oder der Formatter (XINIT.COM) gepatcht werden, da man sonst beim Booten immer die Nachricht "Error - no DOS!" erhält. Dazu sind mehrere Patch-Programme erhältlich. Leider laufen div. Sparta-DOS only Programme nur unter Sparta-DOS 3.2x, deshalb wurden für 3.3x sog. Versionsnummer-Faker geschrieben (Faker.Com und Setvers.Com)...  
  
## Sparta DOS X-Cartridge (4.x):  
- Die Sparta-DOS X cartridge wurde von ICD hergestellt und später an FTE weiterverkauft. Da FTE heute nicht mehr aktiv ist, kann man SDX kaum noch erhalten. Es handelt sich bei SDX um eine sog. Super- oder Mega- cartridge, in der neben dem DOS auch noch zahlreiche utilities vorhanden sind; das Modul ist abschaltbar, erlaubt das aufstecken weiterer Module (die dann ebenfalls abschaltbar werden) und kann Programme die das RAM unter dem OS benötigen via banked RAM (XRAM) problemlos starten. Das DOS ist weiterhin DOS 2.x inkompatibel, Atari-DOS 2.x Formate können aber intern gelesen und angezeigt werden. Ein Programm kann via Batchfile-Verarbeitung (ein einfach selbst zu erstellendes Textfile mit dem Namen STARTUP.BAT) automatisch geladen werden. Eine XE-Ramdisk wird via externem Treiber bis zu einer Größe von 1024k unterstützt (der Treiber muss aber entweder manuell oder via Batchfile geladen werden).  
- DOS-Menü: Nein! Das DOS ist Kommando-orientiert! Es gibt keine eingebaute Befehlsübersicht, d.h. die Kommandos muss man kennen oder im Manual nachschlagen;  
- Formate: alle möglichen und unmöglichen Formate, Single, Enhanced und Double; single-sided und double-sided; 35 Tracks, 40 Tracks, 77 Tracks und 80 Tracks; High Density...  
- Sub-Directories: Ja!  
- Harddisk-Partitionen: Ja, bis 16MB!  
- Aux.: /N /A  
- max. Anzahl von Drives: 9 (als D1: bis D9:);  
- Dir.-Einträge: max. 1024? ;  
- RAM unter dem OS: ??? Programme die diesen Speicherplatz benötigen können via banked RAM (XRAM, also 128k RAM minimum) problemlos geladen werden;  
- DOS 2.0 kompatibel: SD = nein, DD = nein, da eigenes "Sparta-Format"  
- DOS 2.5 kompatibel: ED = nein, da eigenes "Sparta-Format" (via MENU.COM können SD/ED/DD Files aber ins Atari DOS 2.x oder ins Sparta-Format konvertiert werden)  
- Speeder-Treiber: es ist ein ultraspeed treiber vorhanden, der Happy, Speedy und US Doubler (und kompatible Laufwerke) unterstützt;  
- Anmerkung: Die letzte offizielle SDX Version war 4.22; Sparta-DOS bietet eine Datums- und Zeit- Funktion; der lästige XF551-Bug ist hier nicht vorhanden. Leider laufen div. Sparta-DOS only Programme nur unter Sparta-DOS 3.2x, deshalb kann man für Version 4.x sog. Versionsnummer-Faker benutzen (Faker.Com und Setvers.Com)...  
Infos von Andreas Magenheimer.  
