---
title: Atari BASIC
---
# Atari BASIC  
### Background  
Atari BASIC is the "standard" BASIC dialect for the 8-bit series. It was originally sold separately as a (relatively expensive) 8k ROM cartridge. Starting with the 600XL/800XL, the ROMs were included inside the machine. There are three versions, the original version, retroactively known as Revision A, and the updated Revision B and C which fixed various bugs.  
  
Atari originally licensed the 6502-assembler code for Microsoft BASIC. This came in two versions, one that was about 7900 bytes that used a 32-bit (6-digit) floating-point number format, and another that was closer to 9000 that included an expanded floating-point format with a 40-bit (9-digit) numbers. The vast majority of 8-bit machines used the larger 9k/40-bit version, and then further expanded it with additional functions for basic input/output. For instance, the BASIC, character set and I/O in the early PET machines was supplied in a total of 16k of ROM.  
  
The Atari machines were originally designed as games consoles that would replace the Atari VCS, and like those machines, software would be supplied on ROM cartridges. ROM was still relatively expensive at the time, so they expanded it from the 4k of the VCS to the luxurious size of 8k. When the project moved to a computer, a BASIC interpreter was required and Atari naturally licensed MS's code. Atari programmers started with the smaller 7900 bytes version and struggled to cut fit it in the pre-selected 8k cartridge format. That was hard enough of its own, but they really wanted to add additional instructions to take advantage of the Atari's graphics and sound. Eventually, sometime in the summer of 1978, they gave up and went looking for a 3rd party to do it for them.  
  
Atari approached Shepardson Microsystems Inc, or SMI for short, who had written a number of 6502-based products and a series of BASICs for other machines. They proposed a simplified syntax and the cutting of a number of rarely-used features, leaving more room for new commands for graphics and sound. Even then, the result required about 10k, so to cross the remaining gap to 8k, some of the core libraries were moved out of the language and into the operating system ROMs. This had the side-effect of allowing any other language on the Atari to use these routines as well.  
  
By the time SMI was hired, Atari was in something of a rush to get a working BASIC. They were planning to show the machines in January 1979, using the working MS version, but then sell the machines later that year with the SMI version instead. The original contract required SMI to make its final delivery in April 1979, but it contained bonus clauses if they finished early. They did: a working version was delivered in October 1978, so Atari to that to CES instead. To SMI's surprise, they learned that Atari had begun burning that version to ROM for sale, even though it had several known bugs. SMI offered an updated version with various fixes, but Atari didn't bother using it, and instead shipped the buggy version for several years.  
  
In order to fit the code into a 8k ROM, two major pieces of code were moved out of the BASIC into the OS ROM. The first was a set of graphics routines to set up the screen, draw lines, and similar tasks. The second was the floating-point math system, based on a new implementation of the 6-byte binary-coded-decimal (BCD) format SMI had designed for the Z80-based Cromemco machines. Both libraries were notoriously slow. Generally, Atari BASIC was among the slowest BASICs of its era, both due to the OS code and two problems involving loops.  
  
The performance issues led to a profusion of 3rd party BASICs, some of which continue to be developed to this day. By replacing the math libraries and fixing these two loop issues, speed improves on the order of 3 to 5 times in most programs, and this is a common feature of 3rd party BASICs like [Turbo-BASIC_XL](../Turbo-BASIC_XL/index.md) and [Altirra_Basic](../Altirra_Basic/index.md). For even higher performance, [FastBasic](../FastBasic/index.md) uses a p-code system that can be quickly interpreted.  
  
![](attachments/Atari_Basic-Box.jpg)  
Atari BASIC - Computing Language box  
  
### Design notes  
Atari BASIC has some key differences with the more common MS-derived BASICs found on most contemporary machines. Generally, one can describe Atari BASIC's design philosophy as "modeless" and "orthogonal".  
  
Most BASICs of the era had the concept of "immediate mode" and "program mode", and some commands could only be used in one mode or the other. A good example in MS BASIC is the {{LIST}} command, which could only be used in immediate mode, at the "command line". Atari BASIC removed this limitation, one could write a program consisting of {{10 LIST}}.  
  
Additionally, most BASICs had commands that read input or produced output, for example, the {{INPUT}} can be thought of as the opposite of {{PRINT}}. Atari BASIC was orthogonal in that every such command had a partner. For instance, {{LIST}} produces output, so the new command {{ENTER}} reversed this, reading a program listing from a device. This opened up a number of possible overlay techniques that other BASICs lacked.  
  
The most noticeable difference between Atari BASIC and MS-derived versions is the string handling. Atari BASIC used a greatly simplified system of character-arrays instead of the dynamic strings in MS. This meant that all strings had to be predefined using {{DIM}}, and their length could not be changed during run-time. There are a number of advantages to this approach, notably speed and lower memory usage, but this means conversion of standard programs from MS listings may be difficult.  
  
### What's missing  
In addition to differences like string handling, Atari BASIC also lacked some of the less-used features found in MS BASIC. Among these are...  
  
- {{TAB}} and {{SPC}}, for formatting output  
- {{PRINT USING}}, which formatted output (rarely supported on small machines)  
- {{INPUT "prompt", A$}}, which printed the prompt and placed the cursor at the end  
- {{INKEY$}}, which read the keyboard without pausing (unlike {{INPUT}})  
- {{DEF FN}}, which defines mathematical functions  
  
Most 3rd party BASICs for the Atari added many of these features, and more.  
  
### What's new  
To allow BASIC programmers access to the advanced features of the system, Atari BASIC added commands for defining the GRAPHICS, changing COLORs, MOVEing and drawing a DRAWTO, playing SOUND, and others.  
  
## Source Code  
![](attachments/The_Atari_BASIC_Source_Book-Bill_Wilkinson-Kathleen_O_Brien-Paul_Laughton.jpg)  
[The Atari BASIC Source Book - Bill Wilkinson, Kathleen O'Brien and Paul Laughton](https://data.atariwiki.org/DOC/The_Atari_BASIC_Source_Book-Bill_Wilkinson-Kathleen_O'Brien-Paul_Laughton.pdf) ; size: 76.8 MB ; 316 pages  
  
## ROM-Images  
![](attachments/Cart_800er.jpg)  
Atari Basic Cartridge - brown - Revison A  
  
![](attachments/Cart_XE.jpg)  
Atari Basic Cartridge - silver - Revison C ; Revision B was soldered in the machines only and therefore not available as a stand-alone cartridge  
  
- [Atari_Basic_Rev._A.rom](attachments/Atari_Basic_Rev._A.rom) ; ? PEEK(43234) should return: 162  
- [Atari_Basic_Rev._B.rom](attachments/Atari_Basic_Rev._B.rom) ; ? PEEK(43234) should return: 96  
- [Atari_Basic_Rev._C.rom](attachments/Atari_Basic_Rev._C.rom) ; ? PEEK(43234) should return: 234  
- [Monkey_Wrench_with_BASIC_Rev._C.rom](attachments/Monkey_Wrench_with_BASIC_Rev._C.rom) ; both roms in just one 16 KiB file  
- [Monkey_Wrench_II_OS-B_right_v1.rom](attachments/Monkey_Wrench_II_OS-B_right_v1.rom) ; thanks to [serious computerist](http://seriouscomputerist.altervista.org/pages/utility/utility.atari.htm), we really appreciate! :-)  
- [Monkey_Wrench_II_OS-B_right_v2.rom](attachments/Monkey_Wrench_II_OS-B_right_v2.rom) ; thanks to [serious computerist](http://seriouscomputerist.altervista.org/pages/utility/utility.atari.htm), we really appreciate! :-)  
- [Monkey_Wrench_II_OS-B_right_v1_with_BASIC_Rev._C.rom](attachments/Monkey_Wrench_II_OS-B_right_v1_with_BASIC_Rev._C.rom) ; both roms in just one 16 KiB file  
- [Monkey_Wrench_II_OS-B_right_v2_with_BASIC_Rev._C.rom](attachments/Monkey_Wrench_II_OS-B_right_v2_with_BASIC_Rev._C.rom) ; both roms in just one 16 KiB file  
- [Monkey_Wrench_II_XL_with_BASIC_Rev._C.rom](attachments/Monkey_Wrench_II_XL_with_BASIC_Rev._C.rom) ; both roms in just one 16 KiB file  
  
To create one 16 KiB-ROM out of 2 8 KiB ROMs, use the following method:  
  
__Windows:__  
Go to the CMD shell and there to the directory, where the 2 files are, which should be combined, then type:  
  
copy /b monkey.rom+basic.rom allinone16k.rom  
  
and the resulting rom file can be found in the same directory.  
  
__Unix/Mac:__  
Start application shell/Terminal and then type cd and a blank. Drag the folder, in which the 2 files are, directly behind the blank. Check with typing ls -a, whether the 2 files can be seen. Then type:  
  
cat monkey.rom basic.rom > allinone16k.rom  
  
and the resulting rom file can be found in the same directory.  
  
## CAR-Images  
- [Atari_Basic_Rev._A.car](attachments/Atari_Basic_Rev._A.car) ; ? PEEK(43234) should return: 162  
- [Atari_Basic_Rev._B.car](attachments/Atari_Basic_Rev._B.car) ; ? PEEK(43234) should return: 96  
- [Atari_Basic_Rev._C.car](attachments/Atari_Basic_Rev._C.car) ; ? PEEK(43234) should return: 234  
- [The_Monkey_Wrench.car](attachments/The_Monkey_Wrench.car) Tool for better editing Basic programs, version I  
- [The_Monkey_Wrench_II.car](attachments/The_Monkey_Wrench_II.car) Tool for better editing Basic programs, version II v2  
- [Monkey_Wrench_with_BASIC_Rev._C.car](attachments/Monkey_Wrench_with_BASIC_Rev._C.car) ; both cartridges in just one 16 KiB file  
- [Monkey_Wrench_II_OS-B_right_v1.car](attachments/Monkey_Wrench_II_OS-B_right_v1.car) ; thanks to [serious computerist](http://seriouscomputerist.altervista.org/pages/utility/utility.atari.htm), we really appreciate! :-)  
- [Monkey_Wrench_II_OS-B_right_v2.car](attachments/Monkey_Wrench_II_OS-B_right_v2.car) ; thanks to [serious computerist](http://seriouscomputerist.altervista.org/pages/utility/utility.atari.htm), we really appreciate! :-)  
- [Monkey_Wrench_II_XL_with_BASIC_Rev._C.car](attachments/Monkey_Wrench_II_XL_with_BASIC_Rev._C.car) ; both cartridges in just one 16 KiB file. This is a patched BASIC, when initialized jumps to $8002 (right cartridge). Only this way it is runnig on a XL machine.  
  
## Manuals  
- [Atari Basic Reference Manual Rev. A (1980)](https://data.atariwiki.org/DOC/ATARI_BASIC_Reference_Manual.pdf) ; size: 77.7 MB ; 122 pages  
- [Atari Basic Reference Manual-Product Update-C061038 Rev. A, Errata for the above manual (1982)](attachments/Atari_Basic_Reference_Manual-Product_Update-C061038_Rev._A-c_1982_Atari_Inc.pdf) ; size: 4.2 MB ; 6 pages  
- [Atari Basic Reference Manual Rev. C (1983)](https://data.atariwiki.org/DOC/Atari_Basic_Reference_Manual_Rev._C.pdf) ; size: 47.9 MB ; 134 pages  
- [Atari BASIC - Bob_Albrecht, LeRoy Finkel and Jerald R. Brown (1979)](https://data.atariwiki.org/DOC/Atari_Basic_1979.pdf) ; size: 80.9 MB ; OCR ; 348 pages  
- [Atari_Basic-Richard_Haskell (1983)](https://data.atariwiki.org/DOC/Atari_Basic_1983.pdf) ; size: 74.7 MB ; OCR ; 196 pages  
- [Atari BASIC-XL Edition - Bob_Albrecht, LeRoy Finkel and Jerald R. Brown (1985)](https://data.atariwiki.org/DOC/Atari_BASIC_XL_Edition-Bob_Albrecht,_LeRoy_Finkel_and_Jerald_R._Brown_1985.pdf) ; size: 86.5 MB ; OCR ; 404 pages  
- [ATARI BASIC-Handbuch für Selbststudium und Praxis-BOB ALBRECHT, Le Roy Finkel, JERALD BROWN](https://data.atariwiki.org/DOC/ATARI_BASIC-Handbuch_fuer_Selbststudium_und_Praxis-BOB_ALBRECHT,_Le_Roy_Finkel,_JERALD_BROWN.pdf) ; Größe: 44,8 MB ; OCR ; 214 Doppelseiten  
- [ATARI Basic Leitfaden](attachments/ATARI_Basic_Leitfaden.pdf) ; Größe: 5,2 MB ; 11 Seiten  
- [Atari BASIC - Quick Reference Guide - Gilbert Held](attachments/Atari_BASIC_Quick_Reference_Guide-Gilbert_Held.pdf) ; size: 10.4 MB ; 8 pages  
- [OSS Quick reference card for Atari Basic](attachments/oss-quick-reference-card-basic-a-plus.pdf) ; size: 3.4 MB ; 8 pages ; thank you so much Bill Lange for finding this very rare cards. :-)  
- [Atari Basic Referenz-Karten](attachments/Atari_Basic_Referenz-Karten.pdf) ; Größe: 3,1 MB ; OCR ; 271 Seiten  
- [Atari BASIC Source Book (2006)](attachments/Atari_BASIC_Source_Book_2006.pdf) ; size: 10.4 MB ; OCR ; 80 pages ; converted 2006 by Andreas Bertelmann for ABBUC ; thank you Andreas  
- [Monkey_Wrench_-_Manual.pdf](http://data.atariwiki.org/DOC/Monkey_Wrench_-_Manual.pdf) ; size: 67.5 MB ; thanks to [serious computerist](http://seriouscomputerist.altervista.org/pages/utility/utility.atari.htm), we really appreciate! :-)  
- [Monkey_Wrench_II_-_Manual.pdf](attachments/Monkey_Wrench_II_-_Manual.pdf) ; size: 2.5 MB ; thanks to [serious computerist](http://seriouscomputerist.altervista.org/pages/utility/utility.atari.htm), we really appreciate! :-)  
- [The major differences between the Monkey Wrench II and Monkey Wrench II-XL cartridges](attachments/Monkey_Wrench_II_XL_-_Notes.rtf) ; thanks to [serious computerist](http://seriouscomputerist.altervista.org/pages/utility/utility.atari.htm), we really appreciate! :-)  
  
## Atari Basic Keywords  
An incredible good site for all [Atari BASIC keywords](http://www.abbuc.de/software/133-software/softwarereferenz/309-atari-basic-referenz) ; thank you ABBUC, greatly appreciated! :-)  
![](attachments/Atari_Basic_Keywords.jpg)  
Atari Basic Keywords  
  
## Abbreviations  
|| Command || Abbreviation  
  
|| BYE || B.   
|| CLOAD || CLOA.   
|| CLOSE || CL.   
|| COLOR || C.   
|| CONT || CON.   
|| CSAVE || CS.   
|| DATA || D.   
|| DEG || DE.   
|| DIM || DI.   
|| DOS || DO.   
|| DRAWTO || DR.   
|| ENTER || E.   
|| FOR || F.   
|| GET || GE.   
|| GOTO || G.   
|| GOSUB || GOS.   
|| GRAPHICS || GR.   
|| INPUT || I.   
|| LET || LE.   
|| LIST || L.   
|| LOAD || LO.   
|| LOCATE || LOC.   
|| LPRINT || LP.   
|| NEXT || N.   
|| NOTE || NO.   
|| OPEN || O.   
|| PLOT || PL.   
|| POINT || P.   
|| POKE || POK.   
|| POSITION || POS.   
|| PRINT || PR.   
|| PUT || PU.   
|| RAD || RA.   
|| READ || REA.   
|| REM || .   
|| RESTORE || RES.   
|| RETURN || RET.   
|| RUN || RU.   
|| SAVE || S.   
|| SETCOLOR || SE.   
|| SOUND || SO.   
|| STATUS || ST.   
|| STOP || STO.   
|| TRAP || T.   
|| XIO || X.   
  
## Atari Basic Error Codes  
2 - INSUFFICIENT MEMORY  
3 - BAD VALUE  
4 - TOO MANY VARIABLES  
5 - STRING LENGHT ERROR  
6 - OUT OF DATA  
7 - BAD LINE NUMBER  
8 - INPUT ERROR  
9 - DIMENSION ERROR  
10 - STACK OVERFLOW  
11 - OVERFLOW/UNDERFLOW  
12 - LINE NOT FOUND  
13 - NO MATCHING FOR  
14 - LINE TOO LONG  
15 - GOSUB/FOR DELETED  
16 - RETURN ERROR  
17 - SYNTAX ERROR  
18 - INVALID CHARACTER  
19 - PROGRAM TOO LONG  
20 - BAD DEVICE NUMBER  
21 - LOAD FILE ERROR  
  
## Atari Basic Course: An Invitation to Programming 1-3  
- [Course 1: An Invitation to Programming 1 - Fundamentals of Basic Programming CX4101](../An_Invitation_to_Programming_1_CX4101/index.md)  
- [Course 2: An Invitation to Programming 2 - Writing Programs one and two CX4106](../An_Invitation_to_Programming_2_CX4106/index.md)  
- [Course 3: An Invitation to Programming 3 - Introduction to Sound and Graphics CX4117](../An_Invitation_to_Programming_3_CX4117/index.md)  
  
## Atari Basic Kurs (deutsch): Teil 1 und 2 sind vorhanden, Teil 3 wurde leider nie fertig  
- [Kurs 1: Programmieren leicht gemacht-Lernen Sie BASIC mit Dagmar Berghoff-TXG4110](../Programmieren_leicht_gemacht_TXG4110/index.md)  
- [Kurs 2: Noch mehr BASIC-Lernen Sie BASIC mit Dagmar Berghoff-TXG 55007](../Noch_mehr_BASIC_TXG_55007/index.md)  
- [Kurs 3: BASIC für Fortgeschrittene-Lernen Sie BASIC mit Dagmar Berghoff](../BASIC_fuer_Fortgeschrittene/index.md)  
  
## BASIC 1x1 des Programmierens - ein Basic-Lehrgang, einstmals gesendet auf Radio DDR II in der Computersendung REM, Begleitmaterial veröffentlicht als Kassettenbox. Mit einer Programm-Kassette für ATARI 800XL.  
- [Programm_Kassette.atr](attachments/Programm_Kassette.atr)  
- [BASIC 1x1 des Programmierens (Radio DDR II)/Kassetten 1 bis 6 (mp3)](https://k1.spdns.de/Vintage/Sinclair/82/Books/BASIC%201x1%20des%20Programmierens%20%5BRadio%20DDR%20II%5D/Kassetten%201%20bis%206%20(mp3)/)  
- [REM und DT64-Computerclub](http://www.kc85emu.de/scans/fa0589/REM.htm)  
  
## Source and Tools  
- [Extended_Atari_Basic](../Extended_Atari_Basic/index.md)  
- [RPM810](../RPM810/index.md) Program to measure 810 disk speed  
- [Infoline](../Infoline/index.md) Infoline for BASIC and ACTION!  
- [ST_Mouse_Driver_for_Basic](../ST_Mouse_Driver_for_Basic/index.md)  
- [Boolean_Logic_in_BASIC](../Boolean_Logic_in_BASIC/index.md)  
- [Atari_Basic_Special_Clear_Screen](../Atari_Basic_Special_Clear_Screen/index.md) (german)  
- [How_to_find_the_revision_number_of_Atari_Basic](../How_to_find_the_revision_number_of_Atari_Basic/index.md)  
- [Basic_Fast_Stack_and_Fast_Jump](../Basic_Fast_Stack_and_Fast_Jump/index.md)  
- [BASIC_on-off_from_DOS_XL_commandline](../BASIC_on-off_from_DOS_XL_commandline/index.md)  
- [Page_Flip_Routine_for_Basic](../Page_Flip_Routine_for_Basic/index.md)  
- [RAM_Move_Routine_for_Basic](../RAM_Move_Routine_for_Basic/index.md)  
- [Basic_Program_Lister](../Basic_Program_Lister/index.md)  
- [UUDecoder](../UUDecoder/index.md)  
- [Create_Data-Statements_from_binary_load_files](../Create_Data-Statements_from_binary_load_files/index.md)  
- [Schnelle_Player_Bewegung_in_Basic](../Schnelle_Player_Bewegung_in_Basic/index.md) (german)  
- [REV.B_TO_REV.C_CONVERTER.txt](attachments/REV.B_TO_REV.C_CONVERTER.txt) Atari Basic Rev. B to Rev. C Converter as TXT file  
- [RevB2C.atr](attachments/RevB2C.atr) Atari Basic Rev. B to Rev. C Converter as ATR-image  
  
## References  
- [Atari BASIC Article in Wikipedia](http://en.wikipedia.org/wiki/ATARI_BASIC)  
- [Atari_Basic_vs._Commodore_C64_Basic_vs._Apple_II_Basic](../Atari_Basic_vs._Commodore_C64_Basic_vs._Apple_II_Basic/index.md)  
- [Atari BASIC: the good, the bad and the ugly](https://web.archive.org/web/20070524044410/http://www3.sympatico.ca/maury/other_stuff/atari_basic.html)  
  
## Pictures  
![](attachments/Atari_Basic_Reference_Manual_800_.jpg)  
[Atari Basic Reference Manual Rev. A](https://data.atariwiki.org/DOC/ATARI_BASIC_Reference_Manual.pdf) ; size: 77.7 MB ; 122 pages  
  
![](attachments/Atari_Basic_Reference_Manual_XE.jpg)  
[Atari Basic Reference Manual Rev. C](https://data.atariwiki.org/DOC/Atari_Basic_Reference_Manual_Rev._C.pdf) ; size: 47.9 MB ; 134 pages  
  
![](attachments/Atari_Basic_1979.jpg)  
[Atari BASIC - Bob_Albrecht, LeRoy Finkel and Jerald R. Brown (1979)](https://data.atariwiki.org/DOC/Atari_Basic_1979.pdf) ; size: 80.9 MB ; OCR ; 348 pages  
  
![](attachments/Atari_Basic-Richard_Haskell.jpg)  
[Atari_Basic-Richard_Haskell.jpg (1983)](https://data.atariwiki.org/DOC/Atari_Basic_1983.pdf) ; size: 74.7 MB ; OCR ; 196 pages  
  
![](attachments/Atari_Basic-XL-Edition.jpg)  
[Atari BASIC-XL Edition - Bob_Albrecht, LeRoy Finkel and Jerald R. Brown (1985)](https://data.atariwiki.org/DOC/Atari_BASIC_XL_Edition-Bob_Albrecht,_LeRoy_Finkel_and_Jerald_R._Brown_1985.pdf) ; size: 86.5 MB ; OCR ; 404 pages  
  
![](attachments/ATARI_BASIC-Handbuch_fuer_Selbststudium_und_Praxis-BOB_ALBRECHT%2C_Le_Roy_Finkel%2C_JERALD_BROWN-2.jpg)  
[ATARI BASIC-Handbuch für Selbststudium und Praxis-BOB ALBRECHT, Le Roy Finkel, JERALD BROWN](https://data.atariwiki.org/DOC/ATARI_BASIC-Handbuch_fuer_Selbststudium_und_Praxis-BOB_ALBRECHT,_Le_Roy_Finkel,_JERALD_BROWN.pdf) ; Größe: 44,8 MB ; OCR ; 214 Doppelseiten  
  
![](attachments/Atari_Basic_Reference_Guide_XL.jpg)  
[ATARI Basic Leitfaden](attachments/ATARI_Basic_Leitfaden.pdf) ; Größe: 5,2 MB ; 11 Seiten  
  
![](attachments/Atari+BASIC+Quick+Reference+Guide-Gilbert+Held.jpg)  
[Atari BASIC - Quick Reference Guide - Gilbert Held](attachments/Atari_BASIC_Quick_Reference_Guide-Gilbert_Held.pdf) ; size: 10.4 MB ; 8 pages  
  
![](attachments/Atari_Basic_Referenz-Karten3.jpg)  
[Atari Basic Referenz-Karten](attachments/Atari_Basic_Referenz-Karten.pdf) ; Größe: 3,1 MB ; OCR ; 271 Seiten  
