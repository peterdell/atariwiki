# XIO Command Codes DOS Handler (D:)  
  
  
|| code  || ATARIDos 2.5       || MyDOS              || BeweDOS            || TurboDOS           || XDOS               || BiboDos            || SpartaDOS 2.3/3.2, Real.DOS[3](../3/index.md)  || SpartaDOS X[4](../4/index.md)     || SuperDOS  
|  3     | OPEN                | OPEN                | OPEN                | OPEN                | OPEN                | OPEN                | OPEN                | OPEN                | OPEN  
|  5     | GET RECORD          | GET RECORD          | GET RECORD          | GET RECORD          | GET RECORD          | GET RECORD          | GET RECORD          | GET RECORD          | GET RECORD  
|  7     | GET CHARACTERS      | GET CHARACTERS      | GET CHARACTERS      | GET CHARACTERS      | GET CHARACTERS      | GET CHARACTERS      | GET CHARACTERS      | GET CHARACTERS      | GET CHARACTERS  
|  9     | PUT RECORD          | PUT RECORD          | PUT RECORD          | PUT RECORD          | PUT RECORD          | PUT RECORD          | PUT RECORD          | PUT RECORD          | PUT RECORD  
| 11     | PUT CHARACTERS      | PUT CHARACTERS      | PUT CHARACTERS      | PUT CHARACTERS      | PUT CHARACTERS      | PUT CHARACTERS      | PUT CHARACTERS      | PUT CHARACTERS      | PUT CHARACTERS  
| 12     | CLOSE               | CLOSE               | CLOSE               | CLOSE               | CLOSE               | CLOSE               | CLOSE               | CLOSE               | CLOSE  
| 13     | STATUS REQUEST      | STATUS REQUEST      | STATUS REQUEST      | STATUS REQUEST      | STATUS REQUEST      | STATUS REQUEST      | STATUS REQUEST      | STATUS REQUEST      | STATUS REQUEST  
| 32     | RENAME              | RENAME              | RENAME              | RENAME              | RENAME              | RENAME              | RENAME              | RENAME              | RENAME  
| 33     | DELETE              | DELETE              | DELETE              | DELETE              | DELETE              | DELETE              | DELETE              | DELETE              | DELETE  
| 34     |                     | CREATE DIRECTORY    |                     | CLEAR DISK          | GET DENSITY         |                     | LOCK DISK           |                     | RESTORE  
| 35     | LOCK FILE           | LOCK FILE           | LOCK FILE           | LOCK FILE           | LOCK FILE           | LOCK FILE           | LOCK FILE           | LOCK FILE           | LOCK FILE  
| 36     | UNLOCK FILE         | UNLOCK FILE         | UNLOCK FILE         | UNLOCK FILE         | UNLOCK FILE         | UNLOCK FILE         | UNLOCK FILE         | UNLOCK FILE         | UNLOCK FILE  
| 37     | POINT[1](../1/index.md)            | POINT[1](../1/index.md)            | POINT[2](../2/index.md)            | POINT               | POINT[1](../1/index.md)            | POINT               | SEEK                | SEEK                | POINT  
| 38     | NOTE[1](../1/index.md)             | NOTE[1](../1/index.md)             | NOTE[2](../2/index.md)             | NOTE                | NOTE[1](../1/index.md)             | NOTE                | TELL                | TELL                | NOTE  
| 39     |                     | LOAD BINARY FILE&RUN| GET FILE LENGTH     |                     | EXEC COMMAND        |                     | GET FILE LENGTH     | GET FILE LENGTH     |  
| 40     |                     | LOAD BINARY FILE&RUN| (0)LOAD (128)L&RUN  |                     | LOAD BINARY FILE    |                     |                     | LOAD BINARY FILE    |  
| 41     |                     | CHANGE DIRECTORY    |                     |                     |                     |                     | SAVE BINARY FILE    |                     |  
| 42     |                     | CREATE DIRECTORY    | CREATE DIRECTORY    |                     |                     |                     | CREATE DIRECTORY    | CREATE DIRECTORY    |  
| 43     |                     |                     | DELETE DIRECTORY    |                     |                     |                     | DELETE DIRECTORY    | DELETE DIRECTORY    |  
| 44     |                     |                     | CHANGE DIRECTORY    |                     |                     |                     | CHANGE DIRECTORY    | CHANGE DIRECTORY    |  
| 45     |                     |                     |                     |                     |                     |                     | SET BOOT FILE       | SET BOOT FILE       |  
| 46     |                     |                     |                     |                     |                     |                     | UNLOCK DISK         |                     |  
| 47     |                     |                     | GET DISK INFO       |                     |                     |                     | GET DISK INFO       | GET DISK INFO       |  
| 48     |                     |                     |                     |                     |                     |                     | GET CURRENT DIR     | GET CURRENT DIR     |  
| 49     |                     |                     |                     |                     |                     |                     |                     | SET FILE ATTRIBUTES |  
| 80     |                     |                     |                     |                     | EXEC DUP COMMAND    |                     |                     |                     |  
| 251    |                     |                     |                     |                     | FORMAT QUAD   DENS. |                     |                     |                     |  
| 252    |                     |                     |                     | FORMAT QUAD   DENS. | FORMAT DOUBLE DENS. |                     |                     |                     |  
| 253    | FORMAT SINGLE DENS. |                     |                     | FORMAT DOUBLE DENS. | FORMAT SINGLE DENS. |                     |                     |                        | FORMAT  
| 254    | FORMAT DISK (MD/SD) | FORMAT DISK         |                     | FORMAT MEDIUM DENS. | FORMAT MEDIUM DENS. | FORMAT MEDIUM       |                     |                     |  
| 255    |                     |                     |                     | FORMAT SINGLE DENS. | CLEAR DISK          |                     |                     |                     |  
  
  
- XIO 254 under DOS 2.5 tries to format MD and if the drive doesn't support MD, it formats in SD, other DOS versions try only to format MD.  
- XIO 254 under MyDos works as following: If AUX1, Bit 7 is set, the disk is only cleared (empty directory written to disk). If AUX1 Bit 6-0 and AUX 2 are zero, the formatted disk will have the current density setting of the drive, if not, AUX1&AUX2 define the number of available sectors.  
- BeweDOS has no format commands in the FMS. The note and point commands deliver a relative file position rather than an absolute sector/byte position as the other DOS versions do.  
- You can use XIO 33 to delete (empty) MyDOS directories.  
- MyDOS allows to ignore INIT- and RUN-addresses (in XIO39/40) by setting an appropriate AUX1-value (4=do Run & Init, 5=Run only, 6=Init only, 7=ignore Run and Init).  
- In XDOS this is possible via XIO 39, e.g. XIO 39,#1,0,0,"D1:LOA file"  
- XDOS allows the execution of every DUP command (DIR, LOA, SAV, COP,...) via XIO 39 and the density of a disk can be checked via XIO 34.  
  
We need an update on this list for  
  
- MyDOS (Versions)  
- Turbo-DOS  
- Bibo-Dos  
- Bewe-DOS  
- other DOS Versions you use  
  
### Credits  
- [Stefan Dorndorf](http://www.abbuc.de/~bernd/friends/stefan-dietrich-dorndorf.html)  
- Mathy van Nisselroy  
- Freddy Offenga  
- Ron Hamilton for finding the Error in Command "PUT RECORD"  
- Konrad M. Kokoszkiewicz  
  
  
[1](../1/index.md) Note und Point - der absolute Sector und das Byte innerhalb des Sectors müssen angegeben werden/ werden zurück gegeben.  
[2](../2/index.md) Note und Point - das Byteoffset innerhalb der geöffneten Datei müssen angegeben werden/ werden zurück gegeben.  
[3](../3/index.md) Real.DOS is based on SpartaDOS 3.3  
[4](../4/index.md) See Atariki [Lista funkcji specjalnych CIO według urządzeń](http://atariki.krap.pl/index.php/Lista_funkcji_specjalnych_CIO_według_urządzeń)  
