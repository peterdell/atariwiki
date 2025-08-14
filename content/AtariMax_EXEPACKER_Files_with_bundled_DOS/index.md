### AtariMax EXEPACKER Files with bundled DOS  
  
## About  
The current (Januar 2004) AtariMax Flashcart Software is very well suited for Games, either Disk-Bootable Games or File-Games. But if you try to use Applications from the Flash-Cart, there are some shortcomings:  
- if you make a diskimage, you can boot a DOS for the Application, but the Flash-Boot-Software installs a SIO patch. It is not trivial to access a real Floppy drive 1 afer booring from the Flash Cart  
- if you use the EXEPACKER Function (which works like a Gamedos), you don't have a DOS System to load and save data.  
  
So if you like to create a cart with a collection of programming languages, you have to hack the thing :)  
I had the challenge that a friend send me an Atari Artist Cart and asked me if I could put the Atari Artist Program into another cartridge. My idea was to put the software into an AtariMax Flashcart, together with another fine graphics programm, Design Master. But both Programs should work with DOS and should be able to load and save pictures.  
  
The Atari Cartridge Specification defines that with Bit 1 and Bit 2 of the Option Register $BFFD/$9FFD CARTFG the Cart can choose whether a Diskboot should happend or not. Unforuntaly the AtariMax Software don't allow to set this behavior.  
  
So I decided to bundle a DOS with with each Application.  
  
## Preparing a DOS  
After some testing, I found that OS/A+ 2.0 from OSS is an easy to handle DOS for this task. It is a commandline DOS, so it is not neccessary to work with a DUP .SYS. OS/A+ is very Atari DOS 2.0 compatible (same DOSINI Vector) and can also handle Double Density Disks.  
  
With a Memory Monitor (a 16K BiboMon) a examined where this DOS loaded into memory. OS/A+ 2.0 occupies the memory between $0700 and $1C9F. I dumed this memory portion as a COM-File to disk. Next, a small machine program was appended to the dumped DOS file, taking care of all neccesary initialisation:  
  
1. Setting the BOOTFLG to 1 to indicate a successful disk boot  
1. Setting the DOS Vector $0A  
1. Set the D: Device Driver entry in the Hander-table HATABS  
1. Initialize the DOS through HDOSINI  
1. Setting the DOS Initialistion Vector $0C. This DOSINI Vector is set to the Loader Routine itself so that the loader is resident and survies as reset.  
1. Call the command line through HDOSVEC  
  
A good Linker or Packer (I used Thorsten Karwoths PowerPacker) will help to assemble the DOS File and the Loader into one file. The resulting file is for a plain OS/A+ DOS loadable from AtariMax Cart.  
  
### OS/A+ Loader (Bibo Assembler)  
```
01000	 .LI OFF
01010 *************************
01020 ** DOS OSS/A+ LOADER   **
01030 ** (C) 2004 PSC	     **
01040 ** OSS/A+ 2.00	     **
01050 *************************
01060 ;
01070			 .OR $2000
01080			 .OF D:OSLOAD.COM
01090 ;
01100 ;
01110 BOOTFLG  =	$09
01120 DOSVEC	=	$0A
01130 DOSINI	=	$0C
01140 ;
01170 HDOSVEC  =	$15B7
01180 HDOSINI  =	$1540
01190 HDOSTAB  =	$07CB ; HTABS D:
01200 ;
01210 HATABS	=	$031A
01220 ;
01230 START
01240 ;
01250			 LDA #$01	 ; BOOT
01260			 STA BOOTFLG ; SUCCESS
01270 ; SET DOS ADDRESS
01280			 LDA #HDOSVEC
01290			 STA DOSVEC
01300			 LDA /HDOSVEC
01310			 STA DOSVEC+1
01320 ; SET D: ENTRY
01330			 LDX #$F  ; OFFSET D:
01340			 LDA #$44 ; D
01350			 STA HATABS,X
01360			 LDA #HDOSTAB
01370			 STA HATABS+1,X
01380			 LDA /HDOSTAB
01390			 STA HATABS+2,X
01400 ; INIT DOS
01410			 JSR HDOSINI
01420			 LDA #START
01430			 STA DOSINI
01440			 LDA /START
01450			 STA DOSINI+1
01460 ; START DOS SHELL
01470			 JSR HDOSVEC
01480 ;
01490			 RTS
01500 ------------------------------
```
  
## Preparing Design Master  
Design Master is already a COM-File that loads from $2800-$7B67 with a start/init address of $79D# Design Master expects to find a already loaded Font (1024 Byte) at $2400.  
The Design Master loader is almost identical with the OS/A+ loader, except that as the last step Design Master is called instead of the DOS command line.  
  
The resulting compound file (COM-File) includes:  
1. OS/A+ DOS COM File $0700-$1C9F  
1. Design Master Loader $2000-$20xx  
1. Design Master Font $2400-$27FF  
1. Design Master COM-File, $2800-$7B67, Init $2000  
  
### Design Master Loader (Bibo Assembler)  
```
01000	 .LI OFF
01010 *************************
01020 ** DESIGN MASTER LOADER**
01030 ** (C) 2004 PSC		  **
01040 ** OSS/A+ 2.00			**
01050 *************************
01060 ;
01070			 .OR $2000
01080			 .OF D:DMLOAD.COM
01090 ;
01100 ;
01110 BOOTFLG  =	$09
01120 DOSVEC	=	$0A
01130 DOSINI	=	$0C
01140 ;
01150 DMSTART  =	$79D1
01160 ;
01170 HDOSVEC  =	$15B7
01180 HDOSINI  =	$1540
01190 HDOSTAB  =	$07CB ; HTABS D:
01200 ;
01210 HATABS	=	$031A
01220 ;
01230 START
01240 ;
01250			 LDA #$01	 ; BOOT
01260			 STA BOOTFLG ; SUCCESS
01270 ; SET DOS ADDRESS
01280			 LDA #HDOSVEC
01290			 STA DOSVEC
01300			 LDA /HDOSVEC
01310			 STA DOSVEC+1
01320 ; SET D: ENTRY
01330			 LDX #$F  ; OFFSET D:
01340			 LDA #$44 ; D
01350			 STA HATABS,X
01360			 LDA #HDOSTAB
01370			 STA HATABS+1,X
01380			 LDA /HDOSTAB
01390			 STA HATABS+2,X
01400 ; INIT DOS
01410			 JSR HDOSINI
01420			 LDA #START
01430			 STA DOSINI
01440			 LDA /START
01450			 STA DOSINI+1
01460 ; START DESIGNMASTER
01470			 JSR DMSTART
01480 ;
01490			 RTS
01500 ------------------------------
```
  
## Preparing Atari Artist  
Bringing Atari Artist into this was a little bit more work. Atari Artist is a 16 K Cartridge. It occupies the space from $8000 to $BFFF. I plugged in the cart, enabled the BiboMon and moved this area to $3000-$6FFF. The Init- and Start-Adresses can be read at $BFFA (Start) and $BFFE (Init).  
  
The loader for Atari Artist has some more work to do:  
1. set RAMTOP (106, $6a) to $80 (=$8000), and initialize a graphics 0 screen. This is neccessary to move the screen memory and the display list below $8000, else it would be in the same memory area where the program sits.  
1. Test if this is the initial run, if yes, move the memory from $3000-$6FFF to $8000-$BFFF  
1. Set the BOOTFLG to 1 to indicate a successful disk boot  
1. Set the DOS Vector $0A  
1. Set the D: Device Driver entry in the Hander-table HTABS  
1. Initialize the DOS through HDOSINI  
1. Initialize the Atari Artist Program  
1. Call the Atari Artist Program  
The resulting compound file (COM-File) includes:  
1. OS/A+ DOS COM File $0700-$1C9F  
1. Atari Artist Program loading to $3000-$6FFF  
1. Atari artist Loader, $7000-$7096, Init $7000  
  
### Atari Artist Loader (Bibo Assembler)  
```
01000	 .LI OFF
01010 *************************
01020 ** ATARI ARTIST LOADER **
01030 ** (C) 2003 PSC	     **
01040 ** OSS/A+ 2.00	     **
01050 *************************
01060 ;
01070			 .OR $7000
01080			 .OF D:AARTIS3.COM
01090 ;
01100 ;
01110 RAMTOP	=	$6A
01120 CIOV	  =	$E456
01130 ICCOM	 =	$342
01140 ICBADR	=	$344
01150 ICAUX1	=	$34A
01160 ICAUX2	=	$34B
01170 ;
01180 COPN	  =	$03
01190 CCLOSE	=	$0C
01200 ;
01210 FROM	  =	$D2
01220 TO		 =	$D4
01230 NUM		=	$D6
01240 ;
01250 BOOTFLG  =	$09
01260 DOSVEC	=	$0A
01270 DOSINI	=	$0C
01280 ;
01290 CARTINIT =	$8F48
01300 CARTRUN  =	$8F5D
01310 ;
01320 HDOSVEC  =	$15B7
01330 HDOSINI  =	$1540
01340 HDOSTAB  =	$07CB ; HTABS D:
01350 ;
01360 HATABS	=	$031A
01370 ;
01380 START
01390			 LDA #$80	 ; SAVE MEM
01400			 STA RAMTOP  ; FOR CART
01410 ;
01420			 LDA #0		; GR.0
01430			 JSR GRAFIX
01440 ;
01450 ; TEST IF INITAL RUN
01460 ;
01470			 LDA $BFFF
01480			 BNE .3
01490 ;
01500			 LDA #$30	 ; $3000
01510			 STA FROM+1
01520			 LDA #$80	 ; $8000
01530			 STA TO+1
01540			 LDA #$40	 ; $4000
01550			 STA NUM
01560			 LDA #0
01570			 STA FROM
01580			 STA TO
01590 ;
01600			 TAY
01610			 TAX
01620 .1
01630			 LDA (FROM),Y
01640			 STA (TO),Y
01650			 INY
01660			 BNE .2
01670			 INC FROM+1
01680			 INC TO+1
01690 .2
01700			 DEX
01710			 BNE .1
01720			 DEC NUM
01730			 BPL .1
01740 ;
01750			 LDA #$01	 ; BOOT
01760			 STA BOOTFLG ; SUCCESS
01770 ; SET DOS ADDRESS
01780 .3		 LDA #HDOSVEC
01790			 STA DOSVEC
01800			 LDA /HDOSVEC
01810			 STA DOSVEC+1
01820			 LDA #START
01830			 STA DOSINI
01840			 LDA /START
01850			 STA DOSINI+1
01860 ; SET D: ENTRY
01870			 LDX #$F  ; OFFSET D:
01880			 LDA #$44 ; D
01890			 STA HATABS,X
01900			 LDA #HDOSTAB
01910			 STA HATABS+1,X
01920			 LDA /HDOSTAB
01930			 STA HATABS+2,X
01940 ; INIT DOS
01950			 JSR HDOSINI
01960 ; RUN CART
01970			 JSR CARTINIT
01980			 JSR CARTRUN
01990 ;
02000			 RTS
02010 ;
02020 GRAFIX
02030			 PHA
02040			 LDX #6*$10  ; #6
02050			 LDA #CCLOSE
02060			 STA ICCOM,X
02070			 JSR CIOV	 ; CLOSE#6
02080 ;
02090			 LDX #6*$10
02100			 LDA #COPN
02110			 STA ICCOM,X
02120			 LDA #SNAME
02130			 STA ICBADR,X
02140			 LDA /SNAME
02150			 STA ICBADR+1,X
02160 ;
02170			 PLA ; SAVED GR.MODE
02180			 STA ICAUX2,X
02190			 AND #$F0
02200			 EOR #$10
02210			 ORA #$0C
02220			 STA ICAUX1,X
02230			 JSR CIOV
02240			 RTS
02250 ;
02260 SNAME	 .AS "S:"
02270			 .HX 9B00
02280 ------------------------------
02290			 .OR $02E0
02300			 .DA START
02310 ------------------------------
```
  
## Attachements  
Attached you'll find the AtariMax Flash Image for a Cart with this programs as well as the individual compound files.  
