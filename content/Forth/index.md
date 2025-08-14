# Forth  
  
  
### Background  
Forth is a cancatenative stack-based programming language.  
  
Stack-based languages simplify the language's parser considerably because the data for an instruction always appears in the source code before the instructions that will use it. To see why this helps, consider this typical line of [Basic](../Basic/index.md):  
  
{{A = 10 + 20 * B}}  
  
To perform this line, the interpreter has to read the entire line, look up the value of B (let's say 3), realize that the * has to be performed before + and order the instructions correctly, and then finally convert those into instructions something like:  
  
{{get(B,temp1)}} - get the value in B and store it in temp1  
{{multiply(20,temp1,temp2)}} - multiply that value by 20 and store the result in temp2  
{{add(10,temp2,temp3)}} - add 10 to temp2 and store the result in temp3   
{{put(temp3,A)}} - store the value of temp3 into the variable A  
  
In contrast, in a stack-based system, the programmer organizes the code in the fashion it will ultimately be performed. The equivalent would be something like:  
  
{{B 20 mul}}  
{{10 add}}  
  
When this code is performed, the interpreter pushes the value of B on the stack, then 20. It then encounters the mul, which removes the last two items, the 3 and 20, multiplies them, and puts the result back on the stack. Next, it pushes 10 on the stack, leaving the top two locations containing 60 and 10. It then encounters add, taking the two values, adding them, and putting the result back on the stack. The top of the stack now contains the result, 70.  
  
Notice that the stack-based version ''has no temporary values'', and only reads a single instruction at a time, not an entire line of code. As a result, the parser is much simpler, smaller and requires less memory to run. This, in turn, generally makes it much faster, comparable to compiled programs.  
  
Another key aspect of the language is Forth's inherently multitasking design. The program could set up separate stacks and feed different code into each one. The Forth kernel would run each of these stacks in turn, so all Forth programs had access to these features. This made writing multithreaded code very easy, so one could, for instance, have a thread reading the joystick as it moved, and then read that value in a game loop in another stack.  
  
## Forth Standards  
- [Forth79](../Forth79/index.md) (1979)  
- [Forth83](http://forth.sourceforge.net/standard/fst83/) (1983)  
- [ANSI Forth](http://www.taygeta.com/forth/dpans.html) (1994)  
- [Forth 200x](http://www.forth200x.org/forth200x.html) (2009)  
([Family tree](http://www.complang.tuwien.ac.at/forth/family-tree/))  
  
## Forth Systems for the Atari  
  
- [FOCO65](https://github.com/piotr-wiszowaty/foco65) a Forth Cross-Compiler written in Python that translates into XASM assembly language  
- [SPL](../SPL/index.md) (Simple Programming Language) a Forth-ish compiler written in Python that translates into Assembly language  
- [X-FORTH](../X-FORTH/index.md) - a FIG Forth variant, currently maintained  
- [VolksForth](../VolksForth/index.md) - a powerful Forth83 standards Forth for Atari 8bit, Atari ST, MS-DOS, CP/M, C=64, C=16/116/Plus4, still maintained  
- [ANTIC_Forth](../ANTIC_Forth/index.md)  
- [valFORTH](../valFORTH/index.md)  
- [English_Software_Company_FORTH](../English_Software_Company_FORTH/index.md)  
** [Page 6 Review of ES Forth](http://page6.org/archive/issue_14/page_34.htm)  
- [Extended_Atari_FIG-Forth_APX20029](../Extended_Atari_FIG-Forth_APX20029/index.md)  
- [Mesa_Forth](../Mesa_Forth/index.md)  
- [QS_Forth](../QS_Forth/index.md)  
- [Graphic_Forth](../Graphic_Forth/index.md) - A ANTIC / Fig-FORTH 1.4s Version with special Graphics Extensions.  
- [FIG_Forth_1.1](../FIG_Forth_1.1/index.md)  
- [FIG_Forth_1.0D](../FIG_Forth_1.0D/index.md)  
- [fig-FORTH1.4S-1.atr](attachments/fig-FORTH1.4S-1.atr)  
- [fig-FORTH1.4S-2.atr](attachments/fig-FORTH1.4S-2.atr)  
- [ProForth](../ProForth/index.md) Apple II (6502 Source)  
- [SNAUT](../SNAUT/index.md)  
- [Forth_Compiler_from_Frank_Ostrowski](../Forth_Compiler_from_Frank_Ostrowski/index.md)  
- [CoinOp_FORTH](../CoinOp_FORTH/index.md)  
- [Elcomp_Forth_DOS_25.atr](attachments/Elcomp_Forth_DOS_25.atr); Atari Version of Elcomp-Forth by E.Floegel & H.C.Wagner, 1982  
- [Grafs Atari-Forth DOS 2.5.atr](attachments/Grafs_Atari-Forth_DOS_2.5.atr); from Andreas Graf ca. 1990  
- ATAFORTH; advertised as compatible with Atari-DOS; lost; from Dan Bloomquist, Nova Technology, 1982  
- pns-Forth (the author was probably Robert Gonsalves; by Pink Noise Studios, 1981) - at least versions 1.4 and 1.5 were available (''files to be amended'')  
- Colleen Forth; from Atari - Steve Calfee, Michael Albaugh and others, 1980 (''files to be amended'')  
** later ported to Fig standard and evolved into multiple Forths: 1.4S/Team Atari/ANTIC/1.4V/Coin-Op/Turbo4TH  
- Nautilus Compiler - used at least to release game "Alien Garden" on Atari; the compiler was probably not available on the Atari itself; lost; by Nautilus Systems (Jerry Boutelle), 1981  
- Go-Forth (pForth?); released but lost; from Lawrence Rust - Bignose Software / SECS, ca. 1985  
- Fig Forth by Pulsar Software; lost or never released; 1988  
- Marx Forth; never released or lost compiler; advertised by Perkel Software Systems in 1983  
- MVP-FORTH Programmer's Kit; never released or lost; advertised for Atari by ECS / Mountain View Press ca. 1983 as somehow related to (non-Atari) MVP-FORTH  
- Micromotion FORTH-79 - used for Apple II and Atari educational games; the compiler was probably not available on the Atari itself; Micromotion, 1980  
  
## Forth Books  
  
- [Using Fig FORTH On The Atari 800 By Stephen A. Cohen](https://archive.org/details/UsingFigFORTHOnTheAtari800ByStephenACohen)  
- [APX 20157 FORTH Turtle Graphics Plus Manual by William D. Volk](https://archive.org/details/APX20157FORTHTurtleGraphicsPlusManual)  
  
## Forth Articles  
  
- [What_is_Forth](../What_is_Forth/index.md)?  
- [Converting_FIG-Forth_Programs_to_Forth-83](../Converting_FIG-Forth_Programs_to_Forth-83/index.md)  
- [Forth_Code_Size](../Forth_Code_Size/index.md)  
- [6502_Assembler_in_Forth](../6502_Assembler_in_Forth/index.md)  
- [A_FORTH_ASSEMBLER_FOR_THE_6502](../A_FORTH_ASSEMBLER_FOR_THE_6502/index.md) by William F. Ragdale, FOURTH DIMENSIONS Vol 3, 5p, 143ff  
- [FigForth_Source_Listing](../FigForth_Source_Listing/index.md) - FIG Forth for the BBC Micro in 6502 Assembler  
- [Some_Debugging_Sourcecode_found_on_a_BBC_Micro_Fig-Forth_Disk](../Some_Debugging_Sourcecode_found_on_a_BBC_Micro_Fig-Forth_Disk/index.md)  
- [6502_DISASSEMBLER](../6502_DISASSEMBLER/index.md) in Forth  
- [Kermit_Protocol_in_Forth](../Kermit_Protocol_in_Forth/index.md)  
- [6502_Forth_like_tiny_Operating_System](../6502_Forth_like_tiny_Operating_System/index.md)  
- [APPLE_II_QForth](../APPLE_II_QForth/index.md)  
- [GNU_Forth_EC_for_6502](../GNU_Forth_EC_for_6502/index.md)  
- [Henry_Laxen_on_Slashdot_2002](../Henry_Laxen_on_Slashdot_2002/index.md)  
- [Yet_another_target_compiler](../Yet_another_target_compiler/index.md)  
- [Forth_Macros](../Forth_Macros/index.md)  
- [Local_Variables](../Local_Variables/index.md)  
- [Freedom_of_Assembly](../Freedom_of_Assembly/index.md) by Julian V. Noble  
- [Forth_sorting_routines](../Forth_sorting_routines/index.md)  
- [Forth_memory_allocator](../Forth_memory_allocator/index.md)  
- [Forth_Database_design](../Forth_Database_design/index.md) "ELEMENTS OF DATA BASE DESIGN" by Glen B. Haydon  
- [Signed_Integer_Division](../Signed_Integer_Division/index.md) by Robert L. Smith  
- [From_PASCAL_to_FORTH](../From_PASCAL_to_FORTH/index.md) by Leonard Morgenstern  
- [Implementations_of_NEXT_on_6502](../Implementations_of_NEXT_on_6502/index.md)  
- [Ultimate_CASE_Statement](../Ultimate_CASE_Statement/index.md) by Wil Baden, VD 2 1987  
  
## Tutorials  
- [Einfuehrung_in_Forth_83](../Einfuehrung_in_Forth_83/index.md)  
  
## Videos and Screencasts  
  
- [Introducing FIG-Forth on the Atari 8-bit](http://youtu.be/JaNn1cnvBAI)  
- [Atari fig-FORTH: Showing the Stack](http://youtu.be/XFWGteNE0Gg)  
- [Atari FIG-FORTH: About Screens](http://youtu.be/nZKYONc7sYs)  
- [Atari FIG-FORTH - Editing Screens](http://youtu.be/-E5zQZApJRQ)  
- [Atari fig-FORTH: Manipulating the Display List - Part 1](http://youtu.be/t-oeSRC1fdo)  
- [Atari fig-FORTH: Manipulating the Display List - Part 2](http://youtu.be/-eNt-zjmFV0)  
- [Atari Fig-Forth - Full Screen Editor progress](http://youtu.be/8FH2P-z2VVY)  
- [Making Atari fig-FORTH Tools - ANTIC Disassembler 1 of 4](http://youtu.be/qnbN8fEOp4g)  
- [Making Atari fig-FORTH Tools - ANTIC Disassembler 1 of 4](http://youtu.be/-QF97z-aC1M)  
- [Making Atari fig-FORTH Tools - ANTIC Disassembler 1 of 4](http://youtu.be/up2AHDdK8jM)  
- [Making Atari fig-FORTH Tools - ANTIC Disassembler 1 of 4](http://youtu.be/C1Hbjwxp6LI)  
