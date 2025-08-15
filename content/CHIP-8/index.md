---
title: CHIP-8
---
# CHIP-8  
  
Joseph Weisbecker introduced CHIP-8 in BYTE magazine in December 1978, and from 1976 to 1979 COSMAC VIP computers were shipped with CHIP-8 and many sample programs and games. But against Apple II, Atari 400/800, Commodore PET and Tandy TRS80 the COSMAC VIP had no chance on the market and disappeared from the scene, and with it CHIP-8.  
  
In 1990 there was a range of calculators with a graphical display, the HP48 series. These calculators were similarly limited in display area and memory to the early kit calculators of the 1970s. In addition, the HP48 series lacked accessible high-level languages such as BASIC for programming. In September 1990, Andreas Gustafsson released a CHIP-8 interpreter for the HP48SX, specifically to facilitate game development on the HP48. CHIP-48 is popular on the HP48 platform and inspires ports of CHIP-8 to other platforms.  
In 1991, Erik Bryntse releases SCHIP (Super-CHIP), an extension of the CHIP-8 interpreter for the HP48S and HP48SX calculators. SCHIP increases the screen resolution to 128x64 and adds some new commands to the machine language, e.g. to store data beyond the lifetime of the programs (e.g. for highscore tables).  
  
Today there are many developments of CHIP-8, there are CHIP-8 computers available as kits or ready to use, CHIP-8 implementations in FPGA, annual programming contests and modern development environments for CHIP-8 programs.  
  
Similar to BASIC 10 liners or 256B demo contests, programming a CHIP-8 machine is a challenge. It is fascinating how much fun developers can have with the limited CHIP-8 system. A bonus for developers is that CHIP-8 programs can now run on a wide range of platforms, from 8-bit home computers like the Atari 8-bit or Sinclair Spectrum, to Windows, Linux and MacOS, to mobile devices like mobile phones and tablets.  
  
In 2006 Pawel Kalinowski (aka "pkali" or "pirx" on AtariAge) released a CHIP-8 and SCHIP interpreter for the Atari 8-bit. You can find the CHIP-8 interpreter under the name "CHIP8.COM" on magazine disc 153, together with a collection of CHIP-8 and SCHIP games.  
When started, the CHIP-8 interpreter presents a list of the CHIP-8 programmes on the disc. A game can be selected with the cursor keys and started with the RETURN key.  
  
The Escape key terminates the current CHIP-8 programme and the menu with the list of CHIP-8 programmes on the floppy appears.  
In the lower part of the screen the interpreter shows the assignment of the CHIP-8 hex keys to the Atari keyboard. The file CHIP8.CFG can be used to assign the keys and the Atari joystick to the CHIP-8 keys individually for each CHIP-8 program. For the included programs there are already entries in this file, for new programs a new configuration line has to be added. On the AtariWiki page about CHIP-8 there is a collection of CHIP-8 configuration lines for new programs and games.  
  
A comment in the configuration file starts with a slash "/", the rest of the line is ignored.  
For each program there is a line in the configuration file which translates the joystick functions of the Atari 8bit to the hex keys of the CHIP-8.  
  
Additionally the speed of the CHIP-8 program can be set to slow down too fast games.  
  
Example of an entry in the configuration file:  
  
```
/GAMENAME keyUP kDOWN kL kR kF speed
/8chars!! 1char 1char 1c 1c 1c 1char
/
/        U D L R F S
/
ALIEN    1 2 3 C A 3
```
  
Here the following configuration is defined for the program (game) "Alien":  
- Joystick up = CHIP-8 button 1  
- Joystick down = CHIP-8 button 2  
- Joystick left = CHIP-8 button 3  
- Joystick right = CHIP-8 button C  
- Joystick fire = CHIP-8 button A  
- Speed = 3 (higher value = slower)  
  
If you make speed adjustments to the CHIP-8 programs, you should test them on real Atari hardware. The results of a test in the Atari emulator are not always transferable to real hardware.  
  
The START key of the Atari switches off the slowdown of the CHIP-8 programs, so that the programs then run at maximum speed (and often much too fast).  
  
# Ressources  
  
## ROMs  
  
- ROMs for CHIP-8. [https://github.com/kripod/chip8-roms](https://github.com/kripod/chip8-roms)  
- 8 bit Peggle clone written in CHIP-8 Assembly [https://github.com/Chromatophore/Octopeg](https://github.com/Chromatophore/Octopeg)  
- A repository of community-submitted Chip8 programs and their metadata [https://github.com/JohnEarnest/chip8Archive](https://github.com/JohnEarnest/chip8Archive)  
- HP 48 Chip Games [https://www.hpcalc.org/hp48/games/chip/](https://www.hpcalc.org/hp48/games/chip/)  
- A collection of CHIP-8 programs and documentation [https://github.com/mattmikolay/chip-8](https://github.com/mattmikolay/chip-8)  
  
## Development  
  
- A Chip8 IDE [https://github.com/JohnEarnest/Octo](https://github.com/JohnEarnest/Octo)  
- A collection of documentation on the CHIP-8 and related virtual machines [https://github.com/trapexit/chip-8_documentation](https://github.com/trapexit/chip-8_documentation)  
- Mastering CHIP‐8 [https://github.com/mattmikolay/chip-8/wiki/Mastering-CHIP%E2%80%908](https://github.com/mattmikolay/chip-8/wiki/Mastering-CHIP%E2%80%908)  
- Mastering SuperChip [http://johnearnest.github.io/Octo/docs/SuperChip.html](http://johnearnest.github.io/Octo/docs/SuperChip.html)  
- OctoJam [https://itch.io/jam/octojam-7](https://itch.io/jam/octojam-7)  
- Forth for CHIP-8 [https://internet-janitor.itch.io/squad](https://internet-janitor.itch.io/squad)  
- CHIP-8 extensions and compatibility [https://chip-8.github.io/extensions/#a-note-on-modern-implementations](https://chip-8.github.io/extensions/#a-note-on-modern-implementations)  
- Chip-8 Technical Reference v1.0 [http://devernay.free.fr/hacks/chip8/C8TECH10.HTM](http://devernay.free.fr/hacks/chip8/C8TECH10.HTM)  
  
## CHIP-8 Machines  
- Chip-8 and Superchip-8 emulator for Atari 8-bit [https://github.com/pkali/Chip-8](https://github.com/pkali/Chip-8)  
- AtariAge - Chip8 emulator version 1.0 [https://forums.atariage.com/topic/82003-chip8-emulator-version-10/](https://forums.atariage.com/topic/82003-chip8-emulator-version-10/)  
- CHIP-8 is an assembler, debugger, and emulator [https://massung.github.io/CHIP-8/](https://massung.github.io/CHIP-8/)  
- CHIP48 - A CHIP-8 interpreter for the HP48SX (version 2.20) [https://groups.google.com/g/comp.sys.handhelds/c/zv7XZKIDS34](https://groups.google.com/g/comp.sys.handhelds/c/zv7XZKIDS34)  
- A CHIP-8 interpreter, assembler and disassembler in C (Linux, Windows) [https://github.com/wernsey/chip8](https://github.com/wernsey/chip8)  
- CHIP emulator for the PC, with source code and executables for DOS systems. [https://www.hpcalc.org/details/5458](https://www.hpcalc.org/details/5458)  
- SuperChip interpreter for the 49G. Runs games written specifically for use with SuperChip. [https://www.hpcalc.org/details/4774](https://www.hpcalc.org/details/4774)  
- HP48-Superchip [https://github.com/Chromatophore/HP48-Superchip](https://github.com/Chromatophore/HP48-Superchip)  
- CHIP-8 emulator for Emacs [https://depp.brause.cc/chip8.el/](https://depp.brause.cc/chip8.el/)  
- How to write an emulator (CHIP-8 interpreter) [https://multigesture.net/articles/how-to-write-an-emulator-chip-8-interpreter/](https://multigesture.net/articles/how-to-write-an-emulator-chip-8-interpreter/)  
- David Winter's CHIP-8 emulation page [https://www.pong-story.com/chip8/](https://www.pong-story.com/chip8/)  
  
  
## Misc  
- Awesome CHIP-8 [https://chip-8.github.io/links/](https://chip-8.github.io/links/)  
- Chip-8 bei Tindie [https://www.tindie.com/stores/chip8/](https://www.tindie.com/stores/chip8/)  
- BUILD YOUR OWN CHIP-8 COMPUTER [https://chip-8.com/build-your-own-computer](https://chip-8.com/build-your-own-computer)  
- CB2 microcomputer [https://www.tindie.com/products/cb2micro/cb2-microcomputer/](https://www.tindie.com/products/cb2micro/cb2-microcomputer/)  
  
