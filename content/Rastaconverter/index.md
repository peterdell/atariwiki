# Rastaconverter  
  
Rastaconverter is a Windows/Linux based utility which iteratively converts ordinary jpeg/gif/png files into executable files which display the pictures natively on the Atari 8-bit. Rastaconverter uses all the power of display list interrupts and player missile graphics to allow the maximum number of colours possible on the screen concurrently.  
  
## Download Location  
  
[Rastaconverter](https://github.com/ilmenit/RastaConverter) source, executable and help files.  
  
## Information  
  
Rastaconverter is developed by Jakub "Ilmenit" Debski and is currently in its 7th beta version.  
  
## Graphical Limitations on the Atari 8-bit  
  
In graphics mode 15, the Atari 8-bit is capable of displaying 4 colours on a 160x192 (typical) screen. This is normally referred to as the limit in the number of colours that this screen can display. However, this ignores colours supplied by "Player Missile Graphics" (Atari sprites) and those introduced by a "display list interrupt". A display list interrupt (DLI) is some code which is executed while the screen is being drawn and can swap out one colour in place of another (amongst other possibilities).  
  
## Linking to Other Executables  
  
[Integrator](http://www.arsoft.netstrefa.pl/pliki_programy/Integrator3.10.zip) can be used to link Rastaconverter with other executables.  
  
## Generator  
{{  
RastaConverterBeta5.1/Generator  
  
├── build.bat  
  
├── mads.exe  
  
├── no_name.asq  
  
└── no_name.h  
}}  
