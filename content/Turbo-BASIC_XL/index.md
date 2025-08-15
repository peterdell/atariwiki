---
title: Turbo-BASIC XL
---
# Turbo-BASIC XL by Frank Ostrowski 1985  
  
  
## Background  
Turbo-BASIC XL 1.5 is a fast [BASIC](../Basic/index.md) interpreter for the Atari XL and XE. Frank Ostrowski wrote it and first published it in the German Happy Computer magazine in 1985. TURBO is fully compatible with [Atari_BASIC](../Atari_BASIC/index.md) but fixes some well-known bugs and replaces its notoriously slow loops and math functions. The result is that Turbo-BASIC XL will run any Atari BASIC program but do so around three to five times as fast!  
  
If that is not enough, Turbo-BASIC XL also includes a suite of new keywords and functions to improve on the original. These include structured programming concepts like {{WHILE}} loops and similar, DOS commands that allow you to manipulate files without exiting to the DOS menu, {{DPOKE}} and {{DPEEK}} for working with 16-bit memory values, editing commands like {{RENUM}}, and debugging commands like {{TRACE}}. Yet, due to clever memory management, Turbo-BASIC XL leaves 1,700 more bytes of RAM free, allowing you to write larger programs than Atari BASIC.  
  
And if ''that'' wasn't enough, Ostrowski also released the Turbo-BASIC Compiler, which lets you take your completed programs and compile them so they run 15 to 20 times faster than Atari BASIC. The compiler has an associated runtime library, so the resulting programs run on machines without loading Turbo-BASIC XL.  
  
The original Turbo-BASIC XL ran only on the XL/XE machines, but Ostrowski later back-ported it to the original 400/800's as Frost BASIC 1.4, which was later named Turbo-BASIC 1.4. Other programmers have added their own extensions to the TURBO code, resulting in a profusion of minor versions.  
  
Turbo-BASIC XL is compatible with Atari BASIC, but it runs three to four times faster when interpreted and has advanced program control and I/O commands. Using the Turbo-BASIC XL compiler makes programs run 15-20 times faster than Atari BASIC, and it will compile Atari BASIC programs too!  
  
Turbo-BASIC XL will only work on XL and XE computers with at least 64K. Ostrowski is also the author of GFA BASIC for the Atari ST, which is being distributed in the U.S. by MichTron.  
  
TUREX.COM is the enhancement for Turbo-BASIC XL you are looking for. So, load Turbo-BASIC XL, then BLOAD or BRUN the TUREX.COM file. You now have an extended version of Turbo-BASIC XL with various new commands. Take a look at the TUREX.TXT file in the German documentation that shows all available extra commands...  
  
As mentioned before, all *.XTB files are only examples of the Turbo-BASIC XL enhancements. (The "Extended Turbo-BASIC XL" was originally released as an *.ARC file. I also put this file on the disk together with UNARC.COM; but you already find all unarced files on the disk, so the ARC file is redundant and just there for archiving purposes.)  
  
Afair, XTB had been created by Thorsten Karwoth. He is also the author of Atari Macro Assembler 4.32, Atari Macro Assembler XE 2.1, Power Packer, Packer and Linker, Megablast, MyDOS Batchfile Enhancement, Laser Duell, Soundmonitor Professional, and a few other programs. Thank you so much Thorsten, for giving your work into PD. We owe you very much. The community is deep in your debt!  
  
## References  
- [Wikipedia: Turbo-BASIC XL (English)](https://en.wikipedia.org/wiki/Turbo-BASIC_XL)  
- [Wikipedia: Turbo-BASIC XL (Deutsch)](https://de.wikipedia.org/wiki/Turbo-BASIC_XL)  
- [Multi_Zoom_Master](../Multi_Zoom_Master/index.md) Graphics Program by Carsten Strotmann  
- [Player_Missile_in_Turbo_Basic](../Player_Missile_in_Turbo_Basic/index.md)  
- [Simple_Blitter](../Simple_Blitter/index.md)  
- [http://seriouscomputerist.altervista.org/pages/language/language.basic.htm](http://seriouscomputerist.altervista.org/pages/language/language.basic.htm) ; highly recommended!  
- [http://atariki.krap.pl/index.php/Turbo_BASIC_XL](http://atariki.krap.pl/index.php/Turbo_BASIC_XL) ; Turbo-BASIC XL description in Polish ; highly recommended!  
- [http://atariki.krap.pl/index.php/Tokeny_Turbo_BASIC_XL](http://atariki.krap.pl/index.php/Tokeny_Turbo_BASIC_XL); Turbo-BASIC XL tokens in Polish ; highly recommended!  
- [http://www.stcarchiv.de/hc1985/12/turbo-basic](http://www.stcarchiv.de/hc1985/12/turbo-basic) ; Listing des Monats für den 800XL: Turbo-Basic  
- [http://www.stcarchiv.de/hc1986/05/frank-ostrowski](http://www.stcarchiv.de/hc1986/05/frank-ostrowski) ; Frank Ostrowski: Der Interpreter als Sprungbrett zum Erfolg  
- [http://www.stcarchiv.de/hc1988/05/turbo-basics-autostart](http://www.stcarchiv.de/hc1988/05/turbo-basics-autostart) ; Atari XL/XE: Turbo-Basics Autostart  
- [http://www.stcarchiv.de/hc1988/07/karriere-als-programmierer](http://www.stcarchiv.de/hc1988/07/karriere-als-programmierer) ; Karriere als Programmierer: Porsche, Prunk und blaue Scheine  
  
## Pictures form Frank Ostrowski  
![](attachments/Frank_Ostrowski_1.jpg)  
Frank Ostrowski around 1985  
  
![](attachments/Frank_Ostrowski_2.jpg)  
Article of Frank Ostrowski's Turbo-Basic XL from 12/1985  
  
![](attachments/Frank_Ostrowski_3.jpg)  
Frank Ostrowski and his boss in the mid 80's  
  
![](attachments/Frank_Ostrowski_4.jpg)  
Frank Ostrowski in the late 80's taken from ST World Magazine - Jan 1990 - Issue 47 scanned by Lonny Pursell  
  
## Source Code  
After years of investigation and paying government fees in 3-digit amounts, AtariWiki can disclose that the author of Turbo-BASIC XL, Frank Ostrowski, left us in 2011 at age 50 due to a severe disease. Deep investigations regarding his brother, sisters, colleagues, and so on conclude that the source code is lost. Even the enhanced version from Thorsten Karwoth is lost because of water damage in Thorsten's home, which destroyed all listings and diskettes. That is a very sad status, but there is still hope. If someone in the galaxy can build a source code out of this marvelous program from the original object code, as Lorenz did with Star Raiders [Star_Raiders_source_code_by_Lorenz_Wiest](../Star_Raiders_source_code_by_Lorenz_Wiest/index.md), we can rebuild it. We can build the best Basic for the Atari, faster, stronger, and better. We call the six million dollar Basic just simple Ultimate Basic. With all the source codes now in PD: [Source Codes](https://atariwiki.org/wiki/Wiki.jsp?page=Articles#section-Articles-ProgrammingLanguages), it should be possible. Stay tuned.  
  
Frank, wherever you are, you did a man's job - outstanding and far ahead of your time. Germany is deep in your debt, and so is the worldwide Atari community. We will never forget your work and your contribution to the world. You belong to those who are not replaceable and will never be forgotten. May god bless you wherever you are now.  
  
Well, sometimes miracles happen, so today: 5/22/17 ; Somewhere out there in the galaxy, a very good soul (who prefers to stay in the dark) with a great heart at the right place had the source code and we can offer it now with the permission of the Ostrowski family. Here we go:  
- [TBXL_DSDD_DOS_XE.atr](attachments/TBXL_DSDD_DOS_XE.atr) ; size: 368 KB ; complete source on one disk image (DSDD) with DOS XE ; the ACTION! cartridge can read in the source code and the Bibo Assembler  
- [TBXL_SSDD_DOS_2.0D-1.atr](attachments/TBXL_SSDD_DOS_2.0D-1.atr) ; size: 184 KB ; complete source on two disk images (SSDD) with DOS 2.0D part 1/2 ; the ACTION! cartridge can read in the source code  
- [TBXL_SSDD_DOS_2.0D-2.atr](attachments/TBXL_SSDD_DOS_2.0D-2.atr) ; size: 184 KB ; complete source on two disk images (SSDD) with DOS 2.0D part 2/2 ; the ACTION! cartridge can read in the source code  
- [TEXT.zip](attachments/TEXT.zip) ; size: 683 KB ; complete source code in one folder as text files. Please consider that the tokens in file #11 have special characters. Therefore, we made some screenshots of these letters on an original Atari.  
- [Atari_Ampel_Decoder_0.09.zip](attachments/Atari_Ampel_Decoder_0.09.zip) ; typed-in object codes from the Happy Computer magazines as text files regarding the interpreter, compiler, runtime etc., including an Ampel decoder. Ampel is a Basic program for typing in object code with checksums to verify the typed-in listing.  
- [TurboBasic XL v1.5 MADS source (disassembly)](http://atariage.com/forums/topic/266070-turbobasic-xl-v15-mads-source-disassembly/) ; [TurboBasic XL v1.5 MADS source (disassembly)](attachments/tb1_5-mads.asm) from dmsc from AtariAge. dmsc, that is an incredible outstanding work! The community is deep in your debt for sharing your work with us. Thank you sooo much! :-)  
- [Turbo-Basic XL 2.0 with DOS command restored to 1.5](http://atariage.com/forums/topic/265869-turbo-basic-xl-source-code-now-in-pd-and-online/page-3#entry3770028) ; [Turbo-Basic XL 2.0 with DOS command restored to 1.5](attachments/tb20-mads.asm) ; thank you so much peteym5 from AtariAge, that is so outstanding. Thank you so much! :-)))  
- [Turbo-Basic XL 2.0 Source Code Disk](attachments/Turbo-BASIC-20-Source-Code.zip) to build the executable on the Atari itself as shown in the [Building Turbo BASIC XL for the Atari XL/XE From Source Code](https://www.youtube.com/watch?v=WFNRZ_49un8) video  
  
## CAR-Images  
- [TURBO-BASIC_XL-Cartridge.car](attachments/TURBO-BASIC_XL-Cartridge.car)  
- [TURBO-BASIC_XL-built_in_XE.car](attachments/TURBO-BASIC_XL-built_in_XE.car)  
- [Turbo-BASIC_XL_1.5_Switchable_XEGS.car](attachments/Turbo-BASIC_XL_1.5_Switchable_XEGS.car) ; thank you MrFish from AtariAge for your help! :-)  
- [TURBO-BASIC_XL_1.5_Compiler_1.1_Runtime_and_Linker.car](attachments/TURBO-BASIC_XL_1.5_Compiler_1.1_Runtime_and_Linker.car) ; TURBO-BASIC XL 1.5, Compiler 1.1, Runtime and Linker in just one single cartridge; thank you MrFish from AtariAge for your help! :-)  
  
## ROM-Images  
- [Turbo-BASIC_XL_1.5_Switchable_XEGS.rom](attachments/Turbo-BASIC_XL_1.5_Switchable_XEGS.rom) ; thank you MrFish from AtariAge for your help! :-)  
- [TURBO-BASIC_XL_1.5_Compiler_1.1_Runtime_and_Linker.rom](attachments/TURBO-BASIC_XL_1.5_Compiler_1.1_Runtime_and_Linker.rom) ; for use with Atari800MacX emulator ; thank you MrFish from AtariAge for your help! :-)  
- [TURBO-BASIC_XL_1.5_Compiler_1.1_Runtime_and_Linker_Altirra.rom](attachments/TURBO-BASIC_XL_1.5_Compiler_1.1_Runtime_and_Linker_Altirra.rom) ; for use with Altirra emulator ; thank you MrFish from AtariAge for your help! :-)  
  
TODO: (The following is not correct!) There is only a one-byte difference between the headers in the two files above, which is in the cartridge type definition section of the header. The Altirra CAR has the correct byte of "55" for a SIC cart, whereas the Atari800MacX CAR has "30", which is the type defined for a MegaCart 256 KB. Thank you MrFish from AtariAge for your help! :-)  
  
## ATR-Images  
- [TURBO-BASIC_XL_1.5_full.atr](attachments/TURBO-BASIC_XL_1.5_full.atr) ; complete Turbo-BASIC XL with Compiler and Runtime on one single disk with manuals in text files on the disk  
- [TurboBASIC_XL-1A.atr](attachments/TurboBASIC_XL-1A.atr) ; Happy Computer Sonderheft 2-1986-TurboBASIC (XL)-Original Diskette (1-A)-Vorderseite  
- [TurboBASIC_XL-1B.atr](attachments/TurboBASIC_XL-1B.atr) ; Happy Computer Sonderheft 2-1986-TurboBASIC (XL)-Original Diskette (1-B)-Rückseite  
- [TurboBASIC_XL-2A.atr](attachments/TurboBASIC_XL-2A.atr) ; Happy Computer Sonderheft 2-1986-TurboBASIC (XL)-Original Diskette (2-A)-Vorderseite  
- [TurboBasic_XL_with_DOS_2.5_SD.atr](attachments/TurboBasic_XL_with_DOS_2.5_SD.atr) ; Turbo-BASIC XL with Compiler and Runtime on one single disk  
- [Happy_Computer_1985b.atr](attachments/Happy_Computer_1985b.atr); Turbo-BASIC XL with helper program AMPEL for typing in from the original listing in the Happy Computer magazine  
- [Frost_Basic_1.4_cryptic.atr](attachments/Frost_Basic_1.4_cryptic.atr) ; Frost Basic 1.4 for the Atari 400/800 with 'cryptic info', which was released after the Turbo-BASIC XL 1.5 for the XL machines ; Copyright (C) 1985 Markt & Technik Software  
- [Turbo_Basic_1.4.atr](attachments/Turbo_Basic_1.4.atr) ; Turbo-BASIC 1.4 for the Atari 400/800 ; altered Frost Basic, which seems to be the first version for just the 400/800 machines  
- [Turbo_Basic_1.4_HC.atr](attachments/Turbo_Basic_1.4_HC.atr) ; Turbo-BASIC 1.4 for the Atari 400/800 with Happy Computer startup screen  
- [TURBO-BASIC_XL_1.5_Editor_Compiler_Runtime_and_AMPEL.atr](attachments/TURBO-BASIC_XL_1.5_Editor_Compiler_Runtime_and_AMPEL.atr)  
- [Extended_TURBO-BASIC_XL.atr](attachments/Extended_TURBO-BASIC_XL.atr)  
- [Extended_TURBO-BASIC_XL-Manuals.atr](attachments/Extended_TURBO-BASIC_XL-Manuals.atr)  
- [Extended_TurboBASIC_XL_with_DOS_2.5_SD.atr](attachments/Extended_TurboBASIC_XL_with_DOS_2.5_SD.atr)  
- [Turbo-BASIC_XL-Extension.atr](attachments/Turbo-BASIC_XL-Extension.atr) ; thank you MrFish from AtariAge, for your help! :-)  
- [TURBO-BASIC_XL_1.6.atr](attachments/TURBO-BASIC_XL_1.6.atr)  
- [Turbo-Basic_XL_3.2q-SpartaDOS_3.2g.atr](attachments/Turbo-Basic_XL_3.2q-SpartaDOS_3.2g.atr) ; Turbo-Basic XL 3.2q on a SpartaDOS 3.2g formatted SSSD disk  
- [Turbo-Basic_XL_3.2q-SpartaDOS_3.2g_720K.atr](attachments/Turbo-Basic_XL_3.2q-SpartaDOS_3.2g_720K.atr) ; Turbo-Basic XL 3.2q on a SpartaDOS 3.2g formatted 720 KiB disk  
- [TURBO-BASIC_XL-3.2q-SpartaDOS.atr](attachments/TURBO-BASIC_XL-3.2q-SpartaDOS.atr) ; file version of Turbo-BASIC XL 3.2q for SpartaDOS, but on a TURBO-DOS XE formatted diskette; Thank you sooo much Tom Hunt for giving the community the [SpartaDOS suite for TURBO-BASIC XL](attachments/Turbo_Basic_XL_for_Sparta_DOS_3.2d.zip)! We really appreciate your help so much. Please go ahead! :-)))  
- [TURBO-BASIC_XL_for_SpartaDOS_3.2d.atr](attachments/TURBO-BASIC_XL_for_SpartaDOS_3.2d.atr) ; file version of Turbo-BASIC XL 3.2q for SpartaDOS, but on a DOS 2.5 formatted diskette  
- [TURBO-BASIC_XL-NTSC_with_DOS_2.5.atr](attachments/TURBO-BASIC_XL-NTSC_with_DOS_2.5.atr) ; slightly adapted version for NTSC, see [Turbo-Basic_XL_1.5-NTSC.txt](attachments/Turbo-Basic_XL_1.5-NTSC.txt) for the differences  
- [TURBO-BASIC_XL_suite.atr](attachments/TURBO-BASIC_XL_suite.atr)  
- [All Turbo-Basic versions](attachments/TBXL_Versions.zip) ; size: 290 KB ; all 7 versions of Turbo-Basic in one zipped folder ; incredible work from CharlieChaplin from AtariAge. Thank you so much, Charlie Chaplin, for preserving this part of culture. :-)))  
- [Turbo-Basic_XL_Versionen-komplett.zip](attachments/Turbo-Basic_XL_Versionen-komplett.zip) ; size: 576 KB ; same as above, but with version 1.6 from Thor  
- [Turbo_Basic_ATD2.atr](attachments/Turbo_Basic_ATD2.atr); Turbo-Basic XL for Datasette-Turbo-Format(Schleife88,CHAOS etc.). Please use LOAD "T:" to load data from turbo-tape, or SAVE "T:" to save data to tape. The Disk is bootable (MyPicoDOS from HiassofT)  
  
## XEX-File  
- [TURBO-BASIC_XL_3.2q.zip](attachments/TURBO-BASIC_XL_3.2q.zip) ; thank you Tom Hunt from CTH Enterprises  
  
## CAS-File  
- [Turbo-BASIC_XL_1.5.cas](attachments/Turbo-BASIC_XL_1.5.cas) ; thank you MrFish from AtariAge, for your help! :-)  
  
## Manuals  
- [TURBO-BASIC_XL-Interpreter.pdf](attachments/TURBO-BASIC_XL-Interpreter.pdf) ; size: 2 MB  
- [TURBO-BASIC_XL-Turbo_Compiler.pdf](attachments/TURBO-BASIC_XL-Turbo_Compiler.pdf) ; size: 1.7 MB  
- [TURBO-BASIC_XL-Expanded_Documentation.pdf](attachments/TURBO-BASIC_XL-Expanded_Documentation.pdf) ; size: 4.9 MB  
- [TURBO-BASIC_XL_Manual.pdf](attachments/TURBO-BASIC_XL_Manual.pdf) ; size: 1.7 MB  
- [TURBO-BASIC_XL-Compiler.pdf](attachments/TURBO-BASIC_XL-Compiler.pdf) ; size: 1.8 MB  
- [TURBO-BASIC_XL-Compiler_Info.pdf](attachments/TURBO-BASIC_XL-Compiler_Info.pdf) ; size: 431 KB  
- [Expanded-TURBO-BASIC_XL-Documentation-Ron_Fetzer.pdf](attachments/Expanded-TURBO-BASIC_XL-Documentation-Ron_Fetzer.pdf) ; size: 1 MB  
- [Expanded_TURBO-BASIC_XL_Documentation-Ron_Fetzer_1.pdf](attachments/Expanded_TURBO-BASIC_XL_Documentation-Ron_Fetzer_1.pdf)  
- [Expanded_TURBO-BASIC_XL_Documentation-Ron_Fetzer_2.pdf](attachments/Expanded_TURBO-BASIC_XL_Documentation-Ron_Fetzer_2.pdf)  
- [TURBO-BASIC_XL-Expanded_Documentation.pdf](attachments/TURBO-BASIC_XL-Expanded_Documentation.pdf) ; size: 4.9 MB ; thank you MrFish from AtariAge for your help! :-)  
- [HC_AMPEL_Version_1.1.pdf](attachments/HC_AMPEL_Version_1.1.pdf)  
- [Quick Summary of TURBO-BASIC XL Commands and Functions](attachments/Quck_Summery_of_TURBO-BASIC_XL_command_and_functions.pdf)  
- [TURBO-BASIC_XL_1.5_Handbuch_1.pdf](attachments/TURBO-BASIC_XL_1.5_Handbuch_1.pdf)  
- [TURBO-BASIC_XL_1.5_Handbuch_2.pdf](attachments/TURBO-BASIC_XL_1.5_Handbuch_2.pdf)  
- [TURBO-BASIC_XL-Referenz.pdf](attachments/TURBO-BASIC_XL-Referenz.pdf)  
- [EXPANDED_TURBO-BASIC_XL-DOCUMENTATION.txt](attachments/EXPANDED_TURBO-BASIC_XL-DOCUMENTATION.txt)  
- [Kurzreferenz_zur_TURBO-BASIC_XL-Erweiterung.txt](attachments/Kurzreferenz_zur_TURBO-BASIC_XL-Erweiterung.txt)  
![](attachments/Turbo-Basic_XL_1.5-Handbuch_.jpg)  
Turbo-Basic XL 1.5-Handbuch ; original first edition created by Wil Braakman, translated from Rolf A. Specht into German and completely re-edited and revised by Marc 'Sleepπ' Brings ; highly recommended by AtariWiki! :-)))  
  
The above-mentioned printed book includes everything you ever want to know about Turbo-Basic! It is in German. Only a few are available. Orders can be made via the [ABBUC shop](http://www.abbuc.de/mitgliedschaft/shop/literatur).  
  
Das neue Turbo-Basic XL 1.5 Handbuch. Das Buch wurde langjährigen Mitgliedern als Jahresgabe 2015 überreicht. Für alle, die dieses Buch nicht bekommen haben, gibt es jetzt die Möglichkeit eines der wenigen Restexemplare käuflich vom [ABBUC shop](http://www.abbuc.de/mitgliedschaft/shop/literatur) zu erwerben.  
  
## Abbreviations  
|| Command || Abbreviation   
| # | #   
| %GET | %G.   
| %PUT | %.   
| *B | *B   
| *F | *.   
| *L | *L   
| -- | --   
| -MOVE | -.   
| ? | ?   
| BGET | BG.   
| BLOAD | BL.   
| BPUT | BP.   
| BRUN | BR.   
| BYE | B.   
| CIRCLE | CI.   
| CLOAD | CLOA.   
| CLOSE | CL.   
| CLR | CLR   
| CLS | CLS   
| COLOR | C.   
| COM | COM   
| CONT | CON.   
| CSAVE | CS.   
| DATA | D.   
| DEG | DE.   
| DEL | DEL   
| DELETE | DEL.   
| DIM | DI.   
| DIR | DIR   
| DO | DO   
| DOS | DO.   
| DPOKE | DP.   
| DRAWTO | DR.   
| DSOUND | DS.   
| DUMP | DU.   
| ELSE | EL.   
| END | END   
| ENDIF | END.   
| ENDPROC | ENDP.   
| ENTER | E.   
| EXEC | EXE.   
| EXIT | EX.   
| FCOLOR | FC.   
| FILLTO | FI.   
| FOR | F.   
| GET | GE.   
| GOTO | G.   
| GO# | GO#   
| GOSUB | GOS.   
| GOTO | G.   
| GRAPHICS | GR.   
| IF | IF   
| INPUT | I.   
| LET | LE.   
| LIST | L.   
| LOAD | LO.   
| LOCATE | LOC.   
| LOCK | LOCK   
| LOOP | LOO.   
| LPRINT | LP.   
| MOVE | M.   
| NEW | NEW   
| NEXT | N.   
| NOTE | NO.   
| ON | ON   
| OPEN | O.   
| PAINT | PAI.   
| PAUSE | PA.   
| PLOT | PL.   
| POINT | P.   
| POKE | POK.   
| POP | POP   
| POSITION | POS.   
| PRINT | PR.   
| PROC | PRO.   
| PUT | PU.   
| RAD | RA.   
| READ | REA.   
| REM | .   
| RENAME | REN.   
| RENUM | RENU.   
| REPEAT | REP.   
| RESTORE | RES.   
| RETURN | RET.   
| RUN | RU.   
| SAVE | S.   
| SETCOLOR | SE.   
| SOUND | SO.   
| STATUS | ST.   
| STOP | STO.   
| TEXT | TE.   
| TIME$= | TI.   
| TRACE | TRAC.   
| TRAP | T.   
| UNLOCK | UNL.   
| UNTIL | U.   
| WEND | WE.   
| WHILE | W.   
| XIO | X.   
  
## Images  
![](attachments/Happy+Computer+2-1986-TurboBASIC+%28XL%29-Original+Disketten+%281-2%29-Diskette.png)  
Happy Computer 2-1986-TurboBASIC (XL)-Original Diskette (1-2)-Diskette  
  
![](attachments/Happy+Computer+2-1986-TurboBASIC+%28XL%29-Original+Disketten+%282-2%29-Diskette.png)  
Happy Computer 2-1986-TurboBASIC (XL)-Original Diskette (2-2)-Diskette  
  
![](attachments/Frost_Basic-MuT_Software.jpg)  
Frost BASIC 1.4 - start screen ; this was the predecessor of Turbo-BASIC XL 1.5 for the 400/800 machines, but was later published than Turbo-BASIC XL 1.5 itself. The characters after 1985 are, by all means, no mistake. Indeed, they match perfectly with: 'M&T SOFTWARE', which means: 'Markt und Technik Software'. Please look for yourself in the [Atari_ATASCII_Table](../Atari_ATASCII_Table/index.md). :-)  
  
![](attachments/Startscreen-2.jpg)  
Turbo-BASIC XL - startscreen  
  
![](attachments/TURBO-BASIC_XL_1.5%2C_Compiler_1.1%2C_Runtime_and_Linker_.jpg)  
Turbo-BASIC XL - Turbo-BASIC XL 1.5, Compiler 1.1, Runtime and Linker in just one single cartridge  
  
![](attachments/TURBO-BASIC_XL_1.6.jpg)  
Turbo-BASIC XL - Turbo-BASIC XL 1.6 ; thank you so much THOR! We appreciate your help, especially with Basic++  
  
![](attachments/TURBO-BASIC+XL+2.0.jpg)  
Turbo-BASIC XL - Turbo-BASIC XL 2.0 ; (C) 1990 LASER software  
  
![](attachments/TURBO-BASIC+XL+2.1.jpg)  
Turbo-BASIC XL - TT-BASIC XL 2.11 ; with TURBO 2000 SYSTEM; (C) 1988 J. Richter  
  
![](attachments/Turbo+Basic+Version+3.2q.jpg)  
Turbo-BASIC XL 3.2q for SpartaDOS, Startscreen ; (C) 1992 Tom Hunt  
  
![](attachments/TURBO-BASIC_XL-Compiler_Version_1.1_Intro.jpg)  
Turbo-BASIC XL - Turbo-BASIC XL Compiler Version 1.1 - intro  
  
![](attachments/TURBO-BASIC_XL-Compiler_Version_1.1_main.jpg)  
Turbo-BASIC XL - Turbo-BASIC XL Compiler Version 1.1 - main  
  
![](attachments/Ron_Fetzer.jpg)  
Ron Fetzer  
