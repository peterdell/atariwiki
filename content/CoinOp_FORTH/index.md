---
title: CoinOp FORTH
---
## Documentation for Atari Coin Op FORTH And Swarthmore Extensions by Brock A. Miller, David E. McIntyre, and Eugene A. Klotz. May 31, 1983.  
  
  
Images courtesy of Kay Savetz and his [AtariAge post](https://atariage.com/forums/topic/238258-atari-coin-op-forth-and-swarthmore-extensions/). See the *Attach* tab above for the images and a PDF of the manual.  
  
  
This is a programming language that was - as far as I can tell - unreleased to the public until now. Atari Coin Op FORTH seems to be a variant on fig-FORTH.  
  
  
This file contains the manual itself (127 pages) followed by 10 pages of "ephemera" that was in the binder with the manual:  
- a letter from Gene Klotz to Bob Kahn at Atari  
- Fig-FORTH editor instructions  
- Atari FIG Additions sheet  
- Terminal Input-Output sheet  
- FORTH Handy Reference sheet  
- a printout describing the editor  
  
  
Here's some more info on the language from Mike Albaugh, via email to me on June 19 2015: "Coinop forth was developed in Atari coinop division by Steve Calfee and I, based on DECUS forth for the PDP-11. Steve modified the dictionary structure to speed compiles, and used direct threaded code rather than the standard indirect threaded code. This makes it not really forth, but improved performance. I ported the base system to the 400/800. Ed Logg added hooks for the graphics and sound routines in the OS, making Colleen Forth. Later, as Forth became popular and fig forth came out, we did a port of it to the 800 as well. A major visible difference is that fig forth uses the new operators for stores ( ! and C! ) rather than the original ( = and = ) which DECUS, coinop, Colleen forth does. Fig forth also allows meta compilation, which came in handy for the cartridge version of my Point Of Purchase demo. Compared to Colleen Forth, though, it compiles (LOADs) really slowly. That was longer than I expected. Anyway, CoinOp forth was created mainly to allow relatively quick development of software tools on the 6502, where performance was not crucial, but was still important."  
