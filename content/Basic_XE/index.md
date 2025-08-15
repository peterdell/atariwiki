---
title: Basic XE
---
# Basic XE  
OSS, 1984  
  
  
## Background  
Basic XE is the ultimate development of the original [Atari_BASIC](../Atari_BASIC/index.md) code, after its development was taken over by Optimized Systems Software (OSS).  
  
OSS released [Basic_XL](../Basic_XL/index.md) in 1984, adding many new features as well as the FAST command. FAST cached line numbers that were the target of jumps (GOTO and FOR/NEXT loops), addressing one of the two major reasons for the notoriously slow performance of Atari BASIC. The main addition to Basic XE, compared to Basic XL, was a solution to the other big problem in Atari BASIC, the low-performance math code.  
  
In Atari BASIC, all numbers are stored in a 6-byte binary-coded-decimal form. This includes line numbers and array indexes. Every time one of these is encountered, the system sends it into the operating system's BCD library, which had extremely poor performance. Basic XE replaced this library with its own, running at over twice the performance of the original code. This had spin-off effects throughout the average program, not only speeding up actual mathematical functions, but also internal functions like looking up line numbers.  
  
With that exception, the changes between Basic XE and Basic XL are minor, mostly related to handling the increased RAM capabilities of the XE series. However, Basic XE it did not include the AUTORUN runtime library found in Basic XL, meaning that programs that used Basic XE's new functionality could not run on machines that did not have a Basic XE cartridge. However, programs that used only the Basic XL extensions could be written in Basic XE and then linked to the XL's AUTORUN runtime library.  
  
The release of [Turbo-BASIC_XL](../Turbo-BASIC_XL/index.md) at roughly the same time as Basic XE meant that Basic XE was largely forgotten in the market. TURBO-BASIC had all the features of Basic XE and many more, and also shipped with a compiler that not only made stand-alone programs but ran them dozens of times faster as well.  
  
## BASIC XE source code  
- [BASIC_XE_4.2-1_master_with_DOS_2.0D.atr](attachments/BASIC_XE_4.2-1_master_with_DOS_2.0D.atr) ; please use with OSS MAC/65; Yotta-thanks to all who help us here  
- [BASIC_XE_4.2-2_slave_with_DOS_2.0D.atr](attachments/BASIC_XE_4.2-2_slave_with_DOS_2.0D.atr) ; please use with OSS MAC/65; Yotta-thanks to all who help us here  
- [BASIC_XE_4.2-3_fp_with_DOS_2.5.atr](attachments/BASIC_XE_4.2-3_fp_with_DOS_2.5.atr) ; please use with OSS MAC/65; Yotta-thanks to all who help us here  
  
To enable building BASIC XE 4.2 for M091 cartridges, a change has to be made in the D1:MASTER2 file: in line 290, change the value of _27128 to 1. Then follow the normal assembly steps. It results in an object file that loads the four banks to the $3000-$6FFF area in the "1M09" order. Retrieving the bank data in a correct order results in an M091 ROM image.  
  
Thank you so much Tomasz 'Kr0tki' Krasuski for the info in building the runtime, we owe you so much. :-)))  
## CAR-Image  
- [Basic_XE_4.1.car](attachments/Basic_XE_4.1.car)  
- [Basic_XE_4.2.car](attachments/Basic_XE_4.2.car) ; '034M'-version created by a good soul from AtariAge ; thank you so much good soul! :-)))  
  
## ROM-Images  
- [BASIC_XE_4.1.rom](attachments/BASIC_XE_4.1.rom)  
- [OSS_Basic_XE_7.2_universal.rom](attachments/OSS_Basic_XE_7.2_universal.rom) ; should work with SpartaDOS ; this is __not__ an official OSS-, ICD- nor FTe- product ; author unknown  
  
## BIN-Image  
- [Basic_XE_v4.2_1986-02-09Lawrow_Stephen_D.US034M.bin](attachments/Basic_XE_v4.2_1986-02-09Lawrow_Stephen_D.US034M.bin) ; '034M'-version created by a good soul from AtariAge ; thank you so much good soul! :-)))  
- [Basic_XE_v4.2_1986-02-09Lawrow_Stephen_D.US043M.bin](attachments/Basic_XE_v4.2_1986-02-09Lawrow_Stephen_D.US043M.bin) ; just runs in Altirra with OSS '043M' ; thank you so much Tomasz 'Kr0tki' Krasuski for building the 1st runtime, we owe you so much. :-)))  
- [Basic_XE_v4.2_1986-02-09OSSUSM091.bin](attachments/Basic_XE_v4.2_1986-02-09OSSUSM091.bin) ; 'M091'-version created by Tomasz 'Kr0tki' Krasuski; thank you so much Tomasz 'Kr0tki' Krasuski for building the runtime, we owe you so much. :-)))  
  
## ATR-Image  
- [BASIC_XE_Extension_Disk.atr](attachments/BASIC_XE_Extension_Disk.atr) ; original BASIC XE Extension Disk, works with with version 4.1  
- [BASIC_XE_4.2_Extension_Disk_with_DOS_XL_v2.30p.atr](attachments/BASIC_XE_4.2_Extension_Disk_with_DOS_XL_v2.30p.atr) ; BASIC XE Extension Disk, works with with version 4.2 ; thank you so much drac030 from AtariAge, your work is very much appreciated! :-)  
- [Some example programs](attachments/BXL_BXE_programs.zip) ; thanks to Charlie Chaplin from AtariAge. :-)  
- [Basic XE Detokenizer Ver. 1.11 (4-6-89)](attachments/Basic_XE_Detokenizer_Ver._1.11_4-6-89_by_Psycho.atr)  
  
## Manuals  
- [OSS-Basic XE Reference Manual](https://data.atariwiki.org/DOC/OSS_BASIC_XE_Reference_Manual.pdf) 39.0 MB, OCR, onesided, incredible quality made by GoodByteXL. Thank you so much GoodByteXL, you really make the best PDF-files available. Please go ahead with your outstanding work! :-)))  
- [Optimized Systems Software, Inc. - SOFTWARE LICENSE AGREEMENT](attachments/Optimized_Systems_Software_Software_License_Agreement.pdf) ; thanks to Atarimania  
  
## XEP80 driver for BASIC XE  
- [xep80bxe.arc](attachments/xep80bxe.arc) ; this is the driver for the XEP80 to work with OSS BASIC XE (.COM file)  
- [XEP80_BASIC_XE.atr](attachments/XEP80_BASIC_XE.atr) ; same as above on an atr-image  
  
## Info  
- [Basic XE Information on Wikipedia](http://en.wikipedia.org/wiki/Optimized_Systems_Software#BASIC_XE)  
  
## Images  
![](attachments/BASIC_XE_4.2.jpg)  
OSS BASIC XE 4.2 - startscreen  
  
![](attachments/BasicXE.png)  
OSS BASIC XE 4.2 - manual cover  
