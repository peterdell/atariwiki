  
## Information  
  
### Background  
Action (also Action!) is an Atari-specific programming language written by Clinton Parker and sold by Optimized Systems Software (OSS) in ROM cartridge form starting in August 1983. It is the only language other than [BASIC](../Basic/index.md) and [assembler](../assembler/index.md) that had real popularity on the platform and saw any significant coverage in the Atari press; type-in programs and various technical articles were found in most magazines. In comparison, languages like [Forth](../Forth/index.md) and [Logo](../Logo/index.md) saw much less use and almost no press coverage.  
  
Reviewers at the time gushed about the system. They noted that practically every aspect was superior to anything available at the time; compiling was almost instantaneous, the resulting code ran almost as fast as hand-coded assembler, the full-screen editor was universally loved, and the entire system took up only 8k due to clever memory management. The only complaint, also universal, was the poor quality of the original manual set.  
  
Action uses a greatly cut-down version of the ALGOL syntax, and thus bears strong similarities with [Pascal](../Pascal/index.md) and [C](../C/index.md), which were also derived from ALGOL. Like those languages, Action is procedural, with programs essentially consisting of a large collection of functions that call each other. It lacked encapsulation or data hiding, but that is not a serious concern in the limited program sizes available on an 8-bit machine. Syntactically it looks very similar to Pascal, with the exception that it uses ALGOL 68 DO/OD style bracketing rather than Pascal's BEGIN/END.  
  
Action included a number of features to allow it to run as fast as possible. Notably, it's main data types were BYTE, INT and CARD, 8-bit and 16-bit signed and unsigned values, respectively. These map directly onto the basic 6502-types. The language also included a syntax to directly refer to these objects in memory so they could be mapped into hardware registers. For instance, one could set a variable to {{BYTE RTCLOK=20}} which defined the 8-bit value at memory location 20 to be the value of the real-time clock. The user could then read or write to that register using the name {{RTCLOK}}.  
  
These design details helped increase performance, but the primary reason Action was much faster than other languages of the era was due to its memory management model. In languages like C and Pascal, procedure calls use a stack of records known as "activation records" that record the values of variables when the procedure was called. This allows a procedure to call itself, as each call can have its own values, and it is this feature that allows recursion. This concept requires the manipulation of a stack, which in the 6502 was a non-trivial prospect given the CPU stack was only 256 bytes.  
  
Action solved this problem by simply not implementing activation records. Instead, the storage space for variables was allocated at compile time (not dissimilar to Atari BASIC's model). This meant Action could not support recursion, but also eliminated the necessity to build and manipulate a complex stack. This dramatically lowers the overhead of procedure calls, and in a language that organizes a program as a series of procedure calls, this represents a significant amount of time.  
  
Action had a number of limitations, none of them very serious. Curiously, Action did not include support for floating-point types, although such support is built into the machine's OS ROM (see [Atari_BASIC](../Atari_BASIC/index.md) for details) and available to any programming language. This is a significant limitation in some roles, although perhaps not for its target market. It also lacked most string handling routines, but made up for this somewhat with a series of PRINT commands that made formatted output easy.  
  
Generally, Action programs had performance on-par with reasonable-quality [assembler](../assembler/index.md), while being much easier to program. In one review, it ran Byte's Sieve of Eratosthenes 219 times faster than Atari BASIC, while its source was only a few lines longer. In comparison, the assembler version's source ran on for several pages. Such performance, combined with terse code and library functions to access much of the platform's hardware, made it suitable for action games while still having a simple source format suitable for type-in programs. It deserved to be much more popular, and may have been had it been released earlier, or by Atari itself.  
  
Action inspired several similar languages that differ largely in syntax and various features that they do or do not support. Examples include [PL65](../PL65/index.md) and [Quick](../Quick/index.md).  
  
  
### Hello World  
  
```
; Hello world in Action programming language for the Atari 8-Bit computers
PROC Hello()
   PrintE("Hello World!")
RETURN
```
  
The {{;}} is a comment marker, which was a commonly used as the comment marker in assembler as well. The {{PROC}} is the start of a PROCedure, which ends (perhaps oddly) with {{RETURN}}. In Action, the last {{PROC}} in the program is the one that runs first, in this case "Hello". This is something of a mix between Pascal where the "global code" defines the program entry point, and C, where the function called "Main" is the entry point. The only line of code in this example is {{PrintE}}, which simply prints a string, while the more common {{PrintF}} is a formatted print similar to {{printf}} in C.  
  
Like assembler, it was common for variables to be specified at a particular address that mapped onto one of the Atari's "shadow registers" that were used to communicate between the hardware and user programs. Here is a simple variation on Hello World that demonstrates this concept, as well as a basic loop:  
```
; Hello world in a loop
PROC Hello()
BYTE RTCLOK=20,       ; decimal address of system timer
     CONSOL=$D01F     ; hex address of the key-pressed register
CARD TIME
     
    RTCLOK=0 ; reset the clock
    WHILE CONSOL>6 ; did the user press a key?
    DO
        PRINTE("Hello World!")
    OD
    TIME = RTCLOK
    PRINTF("Ran for %E %U jiffies",TIME)
RETURN
```
Note that the definitions of {{RTCLOK}} and {{CONSOL}} are not setting the values, but stating that they are at those memory locations. The syntax changes when those variables are accessed; the {{RTCLOK=0}} ''does'' set the value of that location. Also notice the syntax of loops, which work similarly to Pascal's {{BEGIN/END}} but use {{DO/OD}}.  
  
There is a clever trick in this code. Note that {{RTCLOK}} is defined as a {{BYTE}} but {{TIME}} is defined as a {{CARD}}, a 16-bit value. This is because the clock value is stored in three bytes, 18, 19 and 20. By defining {{TIME}} as a {{CARD}}, when that value is read it automatically reads two bytes, thereby getting a value from both 20 and 19. This solution ignores the third byte, but since the value is from 0 to 65535 jiffies, about 36 minutes, this can safely be ignored for a program that is likely to run for a few seconds. This solution avoids the need to read two bytes and manipulate them into a 16-bit value, something that is commonly found in BASIC programs.  
  
### Manuals and Docs  
- [Action Manual](https://sourceforge.net/p/atari-action/code/ci/master/tree/JAC/doc/action-manual.pdf?format=raw) - The complete latest version of the manual in English. Created and updated by GoodByteXL. There is no better version worldwide! Thank you so much GoodByteXL. We are deep in your debt! :-)))  
- [Action Handbuch](https://sourceforge.net/p/atari-action/code/ci/master/tree/JAC/doc/action-manual-de.pdf?format=raw) - Das komplette, vollständige, restaurierte und überarbeitete Action Handbuch in Deutsch! Der totale Hammer, inkl. Editor, Monitor, Language, Compiler, Library, Run Time, Toolkit. Vollständig überarbeitete Version von GoodByteXL. So müssen PDF-Dateien aussehen, es gibt weltweit nichts vergleichbares. AtariWiki empfiehlt die PDF-Datei auf das Wärmste! Wer diese nicht lädt, ist selber schuld. Wir bedanken uns an dieser Stelle sehr, sehr herzlich bei GoodByteXL für seine lange andauernde und intensive Arbeit an diesem Werk, dass er hiermit der Atari-Gemeinschaft zur Verfügung stellt. GoodByteXL mega-Danke für Deine Arbeit, die Gemeinschaft steht tief in Deiner Schuld. :-)))  
- [The_ACTION!_Toolkit](../The_ACTION!_Toolkit/index.md)  
- [The_ACTION!_Run_Time_Package](../The_ACTION!_Run_Time_Package/index.md)  
- [ACTION!_Reference_Card](../ACTION!_Reference_Card/index.md)  
- [ACTION!_error_codes](../ACTION!_error_codes/index.md)  
- [Aktion_mit_ACTION](../Aktion_mit_ACTION/index.md) - Report about the ACTION! Programming Language from the German Magazin "Happy Computer"  
- [Action!_Bugsheet_3](../Action!_Bugsheet_3/index.md)  
- [Fix_for_the_Bugs_in_divide_in_ACTION!](../Fix_for_the_Bugs_in_divide_in_ACTION!/index.md)  
- [Fix_for_Bug_in_PrintF](../Fix_for_Bug_in_PrintF/index.md)  
- [Optimized Systems Software, Inc. - SOFTWARE LICENSE AGREEMENT](attachments/Optimized_Systems_Software_Software_License_Agreement.pdf) ; thanks to Atarimania  
  
### Tutorials  
- [Step-by-Step_Tutorial_-_How_to_create_a_stand-alone_ACTION!_Program](../Step-by-Step_Tutorial_-_How_to_create_a_stand-alone_ACTION!_Program/index.md)  
- [Action!_and_BBS_Express!_PRO_Tutorial](../Action!_and_BBS_Express!_PRO_Tutorial/index.md)  
- [Larry's Action! Tutorial](../Larrys_Action_Tutorial/index.md)  
- [How_to_setup_an_ACTION!_Development_Disk](../How_to_setup_an_ACTION!_Development_Disk/index.md)  
- [Action! Programming for Atari 8-bit Computers](https://www.youtube.com/watch?v=yQ8ABW8rY40&list=PL5FYYzC9Hpgog9GPsJRtshMP0wpHrxb2J) video tutorial series  
- [Learning Atari Action!](http://atariaction.tumblr.com/) blog  
  
### Workshops  
  
- [Action!_Workshop_1](../Action!_Workshop_1/index.md) - 24. October 2010 "Unperfekthaus" in Essen  
- [Action!_Workshop_2](../Action!_Workshop_2/index.md) - 02. October 2011 "Unperfekthaus" in Essen  
- [Action!_Workshop_3](../Action!_Workshop_3/index.md) - 28. October 2012 "Unperfekthaus" in Essen  
  
## Versions  
  
### Latest Versions  
- [Action! Programming Language](https://sourceforge.net/projects/atari-action/) - The latest [sources](https://sourceforge.net/p/atari-action/code/ci/master/tree/) and [binaries](https://sourceforge.net/projects/atari-action/files/action.zip/download) for Action  
- Includes CAR-Images for OSS cartridges and for standard 16K cartridges  
- Includes executable language and editor "ACTION.COM" on ATR-Images for different DOS versions  
- Includes executable standalone editor "ACTIONED.COM" on ATR-Images for different DOS versions  
You can use it under SpartaDOS and DosXL with "D1:ACTIONED MYSRC.ACT" to direct load the "MYSRC.ACT" file into the editor. Further, this editor can even be used for BASIC, PASCAL, FORTH etc.  
  
### Cross Compiler  
- [https://gury.atari8.info/effectus/](https://gury.atari8.info/effectus/) - Thank you soooo much Gury! That is totally incredible, we now can use high end editors, eclipse and have the results in a flash! We are deep in your debt! Thank you so much, really. :-)  
  
### Original CAR-Images  
- [ACTION_Version_3.6_C_1983_ACS_034M.car](attachments/ACTION_Version_3.6_C_1983_ACS_034M.car)  
- [ACTION_Version_3.6_C_1983_ACS_M091.car](attachments/ACTION_Version_3.6_C_1983_ACS_M091.car)  
  
### Original ROM-Images  
- [ACTION_Version_3.6_C_1983_ACS_034M.rom](attachments/ACTION_Version_3.6_C_1983_ACS_034M.rom)  
- [ACTION_Version_3.6_C_1983_ACS_M091.rom](attachments/ACTION_Version_3.6_C_1983_ACS_M091.rom)  
  
### Original ATR-Images  
- [OSS_ACTION_Programmers_Aid_Disk_100.atr](attachments/OSS_ACTION_Programmers_Aid_Disk_100.atr) - Rebuild from damaged discs and files around the world  
- [The_ACTION!_Toolkit.atr](attachments/The_ACTION!_Toolkit.atr)  
- [The_Action_RunTime_Disk-Original.atr](attachments/The_Action_RunTime_Disk-Original.atr) - Protected image copy of the original disk from a good soul from AtariAge  
- [The_ACTION!_RunTime_Disk.atr](attachments/The_ACTION!_RunTime_Disk.atr) - Unprotected copy of the original disk from a good soul from AtariAge  
- [Original_Action!_System_Runtime_Source](../Original_Action!_System_Runtime_Source/index.md)  
- [Alternative_Action!_Runtime_Source](../Alternative_Action!_Runtime_Source/index.md)  
- [ACTION!_Runtime_von_Jeff_Reister](../ACTION!_Runtime_von_Jeff_Reister/index.md)  
- [OSS_ACTION_3.6_and_REAL_files_with_DOS_XL_2.30p_Color.atr](attachments/OSS_ACTION_3.6_and_REAL_files_with_DOS_XL_2.30p_Color.atr)  
- [TURBO-DOS_XE_with_ACTION_Disk_1.atr](attachments/TURBO-DOS_XE_with_ACTION_Disk_1.atr)  
- [TURBO-DOS_XE_with_ACTION_Disk_2.atr](attachments/TURBO-DOS_XE_with_ACTION_Disk_2.atr)  
  
## Source Code  
  
### Action Language and Editor  
  
at this point AtariWiki must give the highest award possible:  
  
- [Action!_Source_Code](../Action!_Source_Code/index.md)  
Thank you so much Mr. Parker, we can't thank you enough for what you have done for us.  
  
![](attachments/Thank+you+Mr.+Parker.jpg)  
Thank you so much Mr. Parker  
  
- [Action! Editor Source Code](https://sourceforge.net/p/atari-action/code/ci/master/tree/ALFRED/EDITOR/)  
Thank you Alfred from AtariAge for extracting the editor source code for generations to come. We are deep in your debt.  
  
![](attachments/Thank+you+Alfred.jpg)  
Thank you Alfred  
  
### Functions  
- [Misc_useful_ACTION!_Functions](../Misc_useful_ACTION!_Functions/index.md) - (DIVERS.ACT)  
- [Chartest](../Chartest/index.md) - a group of routines which perform various functions and tests on characters.  
- [Fast_Screen_IO](../Fast_Screen_IO/index.md)  
- [Player_Missile](../Player_Missile/index.md)  
- [String_Library_PSC](../String_Library_PSC/index.md) - (STRING.ACT)  
  
### Mini-Runtime LIBs  
- [_Intro](../_Intro/index.md) (Eine kleine Einführung zu den Mini-LIBs)  
- [Simple_PRINT_Runtime](../Simple_PRINT_Runtime/index.md) (Mini-LIB)  
- [ZERO_and_SETBLOCK](../ZERO_and_SETBLOCK/index.md) (RT Part)  
  
  
### Examples  
  
- [A_pseudo_Assembler_in_Action!](../A_pseudo_Assembler_in_Action!/index.md)  
- [ACTION!_Logo](../ACTION!_Logo/index.md) ACS  
- [ATARI_Rainbow_effect](../ATARI_Rainbow_effect/index.md)  
- [Access_SpartaDOS_commandline_parameters](../Access_SpartaDOS_commandline_parameters/index.md)  
- [Atari_Fuji_Logo_in_ACTION!](../Atari_Fuji_Logo_in_ACTION!/index.md)  
- [Atari_Picture_Mirror_Tool](../Atari_Picture_Mirror_Tool/index.md)  
- [Atari_ST_Mouse_Driver_for_ACTION!](../Atari_ST_Mouse_Driver_for_ACTION!/index.md)  
- [BASIC_USR_Machine_Language_Call_Simulation_for_ACTION!](../BASIC_USR_Machine_Language_Call_Simulation_for_ACTION!/index.md)  
- [Backtrack_in_ACTION!](../Backtrack_in_ACTION!/index.md)  
- [Big_Symbol_Table_for_ACTION!](../Big_Symbol_Table_for_ACTION!/index.md) ACS  
- [Binary_File_Load_in_ACTION!](../Binary_File_Load_in_ACTION!/index.md)  
- [Butterfly_Demo](../Butterfly_Demo/index.md)  
- [C_Style_Strings](../C_Style_Strings/index.md)  
- [COM_File_Segment_Dump](../COM_File_Segment_Dump/index.md)  
- [Catch_and_Throw_Error_Handling](../Catch_and_Throw_Error_Handling/index.md) ACS  
- [Catepill](../Catepill/index.md) unfinished Game with Level editor in ACTION!  
- [Compile_to_Disk](../Compile_to_Disk/index.md) ACS  
- [DLI_in_ACTION!](../DLI_in_ACTION!/index.md)  
- [DOS_Setup](../DOS_Setup/index.md) - A small tool to copy some files from disk to ramdisk. can be configured by a textfile.  
- [Data_Entry_Routines](../Data_Entry_Routines/index.md)  
- [Date_Routines](../Date_Routines/index.md) - Library of routines supporting the input, storage and manipulation of dates.  
- [Delete_EOL_Char_in_Textfiles](../Delete_EOL_Char_in_Textfiles/index.md)  
- [Displaylist_in_ACTION!](../Displaylist_in_ACTION!/index.md)  
- [END_Procedure](../END_Procedure/index.md) - Call procedure to leave an Action Program  
- [ERROR](../ERROR/index.md) (Converts SpartaDOS, BeWeDOS and RealDOS error # to readable text)  
- [Fast_Graphics_15_Routines](../Fast_Graphics_15_Routines/index.md)  
- [Fast_Graphics_8_Routines](../Fast_Graphics_8_Routines/index.md)  
- [File_Compare](../File_Compare/index.md)  
- [File_IO_Routines](../File_IO_Routines/index.md)  
- [File_Select_Box](../File_Select_Box/index.md)  
- [File_Select_Shell](../File_Select_Shell/index.md)  
- [Game_AMAZING_in_ACTION!](../Game_AMAZING_in_ACTION!/index.md)  
- [Grep_for_Sparta_DOS](../Grep_for_Sparta_DOS/index.md)  
- [HexDump](../HexDump/index.md) - Dump - Print the contents of binary files in hexadecimal and ATASCII  
- [Jump_to_DOS_DUP](../Jump_to_DOS_DUP/index.md)  
- [Kermit_in_ACTION!](../Kermit_in_ACTION!/index.md)  
- [Load_APL_Display-List_Files](../Load_APL_Display-List_Files/index.md)  
- [Load_Font_Files_in_ACTION!](../Load_Font_Files_in_ACTION!/index.md)  
- [Load_Koala_Pictures](../Load_Koala_Pictures/index.md)  
- [MiniDOS](../MiniDOS/index.md)  
- [Multi_Player_Animation](../Multi_Player_Animation/index.md)  
- [OS_Vectors](../OS_Vectors/index.md)  
- [PERCOM_Block_Manipulation](../PERCOM_Block_Manipulation/index.md)  
- [PERCOM_Service](../PERCOM_Service/index.md) -- Disk Format Configuration  
- [Printing_Routine_for_Epson_Printer](../Printing_Routine_for_Epson_Printer/index.md)  
- [Query_Console_Keys](../Query_Console_Keys/index.md)  
- [SIO_CIO_Routine](../SIO_CIO_Routine/index.md)  
- [SourceCodeDisk1](../SourceCodeDisk1/index.md) ; SpartaDOS X disk image with Action source code  
- [Starburst](../Starburst/index.md)  
- [Symbol_table_lister](../Symbol_table_lister/index.md) ACS  
- [Timer_Programming](../Timer_Programming/index.md)  
- [Trackball](../Trackball/index.md)  
- [Using_the_RAM_Under_the_OS_ROM_on_XL_and_XE_Computers](../Using_the_RAM_Under_the_OS_ROM_on_XL_and_XE_Computers/index.md)  
- [VT52_Terminal_Emulator](../VT52_Terminal_Emulator/index.md)  
- [VTEmulator](../VTEmulator/index.md)  
- [Windowing_Routines](../Windowing_Routines/index.md)  
- [XFD_Disk_Transfer_tool](../XFD_Disk_Transfer_tool/index.md) XFormer Filetransfere  
- [XModem_Filetransfer](../XModem_Filetransfer/index.md)  
  
### Tools  
  
- [Action_Source_Code_Formatter](../Action_Source_Code_Formatter/index.md)  
- [Infoline](../Infoline/index.md) for ACTION! and BASIC  
- [ACTION_OBJECT_CODE_RELOCATION_PROGRAM](../ACTION_OBJECT_CODE_RELOCATION_PROGRAM/index.md) ; Thank you so much Alfred from AtariAge, we all really appreciate your help here again.  
- [Relocator](../Relocator/index.md) for Action; relocates Action code to run independent from the code location  
- [acsterm.txt](attachments/acsterm.txt) ; ACSTERM is a terminal emulator for the Atari 800, 800XL, 1200XL and 130XE  
- [How_to_find_the_revision_number_of_ACTION](../How_to_find_the_revision_number_of_ACTION/index.md)  
  
### Missing Tools: Graphics Utilities Library and Shape Editor  
  
__As of 2020, just these two programs are still missing. They were published via OSS-BBS only! The number was: +1 (408) 438 - 6775. Any hint, any help is welcome at any time. We would really appreciate your help in that case.__  
  
![](attachments/Graphics+Utilities+Library+1.jpg)  
Graphics Utilities Library for ACTION! screen 1  
  
![](attachments/Graphics+Utilities+Library+2.jpg)  
Graphics Utilities Library for ACTION! screen 2  
  
![](attachments/Shape+Editor+and+Animator.jpg)  
Shape Editor and Animator for ACTION!  
  
![](attachments/OSS-BBS_.jpg)  
OSS-BBS with the number: +1 (408) 438 - 6775 where the two missing programs were published only!  
  
## Articles in Magazines  
  
### Advertisements  
![](attachments/00_first_ad_in_compute_Jul1983.jpg)  
First Action ad in Compute July, 1983 ; please take into account: 128-column screen and for Apple II & Commodore 64. Thanks to GoodByteXL!  
  
### Analog  
||Title||Issue||Language||Comment  
|[Review_Action!](../Review_Action!/index.md)|#16 (02/ 84)|en|Review  
|[An_Introduction_to_ACTION!](../An_Introduction_to_ACTION!/index.md) |#17 + #18 (03+ 04/ 84)|en|Tutorial  
|[Stars_in_3D](../Stars_in_3D/index.md)|#20 (07/ 84)|en|Demo  
|[Bounce_in_ACTION!](../Bounce_in_ACTION!/index.md)|#20 (07/ 84)|en|Game  
|[Pulse_in_ACTION!](../Pulse_in_ACTION!/index.md)|#26 (01/ 85)|en|Demo  
|[More_Fun_with_Bounce!](../More_Fun_with_Bounce!/index.md)|#27 (02/ 85)|en|Game  
|[Demon_Birds](../Demon_Birds/index.md)|#28 (03/ 85)|en|Game  
|[Roto](../Roto/index.md)|#31 (06/ 85)|en|Game  
|[Color_the_shapes](../Color_the_shapes/index.md)|#32 (07/ 85)|en|game  
|[Getting_in_on_the_Action!_1](../Getting_in_on_the_Action!_1/index.md)|#32 (07/ 85)|en|Tutorial  
|[Getting_in_on_the_Action!_2](../Getting_in_on_the_Action!_2/index.md)|#35 (10/ 85)|en|Tutorial  
|[Sneak_attack](../Sneak_attack/index.md)|#36 (11/ 85)|en|Game  
|[Air_hockey](../Air_hockey/index.md)|#38 (01/ 86)|en|Game  
|[D-Check](../D-Check/index.md)|#44 (07/ 86)|en|Tool  
|[Trails](../Trails/index.md)|#50 (01/ 87)|en|Tool for using the KoalaPad in ACTION!  
|[ACTION!_Zero_Free](../ACTION!_Zero_Free/index.md)|#54 (05/ 87) |en|Tool  
  
### Antic  
||Title||Issue||Language||Comment  
|[Interrupts_in_ACTION!](../Interrupts_in_ACTION!/index.md)|Vol. 3 #3 (07/ 84)|en|  
|[Demo_Pretty](../Demo_Pretty/index.md)|Vol. 3 #7 (11/ 84)|en|Demo from Antic I/O-Board  
|[SPLASH_in_ACTION!](../SPLASH_in_ACTION!/index.md)|Vol. 3 #12 (04/ 85)|en|Demo  
|[Game_AMAZING_in_ACTION!](../Game_AMAZING_in_ACTION!/index.md)|Vol. 4 #1  (05/ 85)|en|Game  
|[View_3D](../View_3D/index.md)|Vol. 4 #2 (06/ 85)|en|Tool  
|[Dark_Star](../Dark_Star/index.md)|Vol. 4 #3 (07/ 85)|en|Game: Zapping Aliens With Radioactive Waste  
|[Display_Master](../Display_Master/index.md)|Vol. 4 #4 (08/ 85)|en|  
|[Eight_Queens](../Eight_Queens/index.md)|Vol. 4 #5 (09/ 85)|en|92 chess solutions in 40 seconds  
|[Video_Stretch](../Video_Stretch/index.md)|Vol. 5 #6 (10/ 86)|en|Tool  
|[Killer_Chess](../Killer_Chess/index.md)|Vol. 6 #10 (02/ 88)|en|Game  
|[Reardoor](../Reardoor/index.md)|Vol. 6 #10 (02/ 88)|en|Game  
|[Frog](../Frog/index.md)|Vol. 6 #10 (02/ 88)|en|Game  
|[ACTION!_Toolbox](../ACTION!_Toolbox/index.md)|Vol. 7 #6 (10/ 88)|en|Lightning-fast command finder (Wordfind and Matchup)  
  
### ATARI''magazin''  
||Title||Issue||Language||Comment  
|[Schnelle_Vektoren_in_ACTION!](../Schnelle_Vektoren_in_ACTION!/index.md)|#1 (1-2/ 87)|de|Tutorial: Action!-Center Teil 1  
|[Schnelle_Umwege_in_ACTION!](../Schnelle_Umwege_in_ACTION!/index.md)|#2 (3-4/ 87)|de|Tutorial: Action!-Center Teil 2  
|[Interne_Variablen](../Interne_Variablen/index.md)|#3 (5-6/ 87)|de|Tutorial: Action!-Center Teil 3  
|[Was_ist_dran_an_Action!?](../Was_ist_dran_an_Action!?/index.md)|#4 (7-8/ 87)|de| Tutorial: Action!-Center Teil 4  
  
### Atari Magazine  
||Title||Issue||Language||Comment  
|[ACTION!_Deel](../ACTION!_Deel/index.md)| |nl|A collection of Action Articles  
  
### CK Computer Kontakt  
||Title||Issue||Language||Comment  
|[Musik_in_ACTION](../Musik_in_ACTION/index.md) |#10/85|ge| Tutorial  
|[ACTION!_noch_schneller](../ACTION!_noch_schneller/index.md) |#6-7/86|ge| Tutorial  
