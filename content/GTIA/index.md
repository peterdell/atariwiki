''__copied from "Mapping the ATARI" as an example only! Needs to be re-written or completely written from scratch!__''  
  
GTIA (or CTIA) is a special television interface chip designed exclusively for the Atari to process the video signal. ANTIC controls most of the C/GTIA chip functions. The GTIA shifts the display by one-half color clock off what the CTIA displays, so it may display a different color than the CTIA in the same piece of software. However, this shift allows players and playfields to overlap perfectly.  
  
There is no text window available in GTIA modes, but you can create a defined area on your screen with either a DLI (see COMPUTE!, September 1982) or by POKEing the GTIA mode number into location 87 ($57), POKEing 703 with four and then setting the proper bits in location 623 ($26F) for that mode. Only in the former method will you be able to get a readable screen, however. In the latter you will only create a four line, scrolling, unreadable window. You will be able to input and output as with any normal text window; you just won't be able to read it! GTIA, by the way, apparently stands for "George's Television Interface Adapter." Whoever George is, thanks, but what is CTIA?  
  
See the OS User's Manual, the Hardware Manual, De Re Atari and COMPUTE!, July 1982 to September 1982, for more information.  
