# Rambit Turbocharger for Atari Datarecorders  
  
![](attachments/Rambit_logo.jpg)  
  
The purpose of this interface from the UK is to use high transfer rates for compact cassettes which are used with the two models of the 1010 datarecorders and the XC12 (or Phonemark) datarecorder.  
  
The Rambit system consists of a small circuit board containing an IC and a small handful of components, and a tape containing the conversion utility program which is designed to be used either on its own or with an Assembler/Editor cartridge. You will need this cartridge to assist in altering multi-stage load tapes to single stage before converting them to the Rambit format.  
  
The circuit board is easily fitted inside your cassette unit. There are 5 leads to be soldered to the printed circuitry, and the 1010 required that a track be cut and a wire link and capacitor be installed. The instructions give a step-by-step guide, and a diagram of the tracks is supplied to assist in the connection of the leads from the interface board. Without this interface converted programs will not load, and Rambit will not convert BASIC programs however the interface in no way interferes with normal usage of the cassette unit.  
  
Tapes converted to Rambit format all have a short normal speed boot section at the front of the tape which then controls the loading of the program itself loading it at the incredible speed of 3300-3600 baud. Rambit's loader program loads into Page 0 and the lower half of the stack on Page 1 so that most of the computer's memory can be loaded without fear of overwriting the loader program.  
  
When used in conjunction with an Assembler/Editor cartridge, Rambit will also save assembled machine code in the high-speed format. The resulting tape can be booted in just the same manner as a game, and it will automatically run if RUNAD is loaded in the code. It is required to include the binary file identification bytes, normally automatically included with the assembled program when saved to tape, so it can be preferred to save the code from the Assembler/Editor directly to tape in the normal fashion, and then load it back with Rambit for conversion. The loader program for these binary files loads Page 7 and the lower half of Page 8, and the appropriate loader is automatically added by Rambit.  
  
Rambit's function is to save consecutive areas of memory or single or compound files produced by the Assembler/Editor cartridge at the 3300-3600 baud rate mentioned. Single stage load tapes follow Rambit's conventions already, so converting these is a matter of using the utility's 'L' command to load the original, and the 'S' command to save the converted program to a blank tape. A verification facility allows the checking of the new tape's loading ability. A variety of other commands, many of which bear a close similarity to those in the Assembler/Editor cartridge allow one to display and alter memory.  
  
Multi-stage programs require to be changed to single stage first. The instructions give a guide as to how to do this, but basically you have to use the Assembler/Editor cartridge with the utility to load the first stage in order to locate where the main section is to be loaded and from where it should be done. Once this has been accomplished, the main section is loaded with the 'L' command and then you have to add the boot address information to the start of the program in memory.  
  
## Flac-files  
Because the cassette uses the Rambit format, it is not possible to create cas- or atr-files of this tape. You can download the flac-files and record them on a cassette.  
[Rambit_cassette_Side1_V1.flac](attachments/Rambit_cassette_Side1_V1.flac)  
[Rambit_cassette_Side2_V2.flac](attachments/Rambit_cassette_Side2_V2.flac)  
  
## Manual  
Including schematics for the 1010 and XC12 datarecorders.  
[Rambit_Manual.pdf](attachments/Rambit_Manual.pdf)  
  
## Pictures of the interface (right-click to save the larger images)  
![](attachments/Rambit1.jpg)  
![](attachments/Rambit2.jpg)  
![](attachments/Rambit3.jpg)  
  
## Mediapictures  
![](attachments/Rambit_Cassette.jpg)  
Cassette of the Rambit Turbocharger  
  
## Thank you  
Many thanks to Page6.org. Parts of the review have been used in this article.  
