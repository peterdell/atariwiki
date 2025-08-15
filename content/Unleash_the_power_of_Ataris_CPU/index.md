---
title: Unleash the power of Ataris CPU
---
### Unleash the power of Ataris CPU  
  
By Ed Stewart  
(from A.N.A.L.O.G. 2, March/April 1981)  
  
Would you like to get as much as a 30% increase in speed from Your Atari 6502 CPU? Would you also like to get this benefit without any additional capital expense? If your answer is no you probably don't like apple pie either, but if your answer is yes, read on, and I will tell you how to accomplish such a feat with one simple BASIC POKE in the right place.  
  
First a little background information about one of the many things going on inside your ATARI computer. The particular thing that I want you to know about is how display information reaches your TV screen. There is a specific hardware chip called ANTIC that has most of the responsibility for seeing that the display gets to your TV screen. ANTIC does this by operating independently from the main 6502 CPU in your computer. ANTIC is in fact a primitive CPU in it's own right. It executes a program which is located in RAM just as the 6502 executes a Program in RAM or ROM, We can therefore call the Atari a multiprocessing computer since more than one CPU may be active at any time. A peculiar and somewhat unfortunate thing happens when a multiprocessing system such as the Atari is actively executing instructions both CPUs desire access to memory simultaneously. The two CPUs cannot both access memory at the same time so one must wait until the other completes it's access request. This memory access conflict is common to all computers containing more than one CPU - from micros to macros - and is generally not something to be concerned about.  
  
The ANTIC chip fetches it's data from memory using a technique called "Direct Memory Access" or DMA. Whenever this memory fetch is occurring the 6502 is temporarily halted. DMA is said to be "stealing" a portion of the computer's available time called a cycle. There are 1,789,790 cycles of computer time available per second. If DMA had not "stolen" that cycle of computer time the 6502 would not have been halted and therefore would have finished it's program instructions sooner. It is only logical to conclude that the more this DMA activity occurs in behalf of the ANTIC chip, the more our 6502 will be slowed down.  
  
The ANTIC chip re-displays the entire TV display 60 times each second. During each of these 60 times many computer cycles are stolen from the 6502. During each of these 60 times the ANTIC chip also "interrupts" the 6502 and causes it to perform such tasks as updating various software timers and reading game controllers (joysticks and paddles). When the 6502 finishes what it must do in response to the ANTIC "interrupt" it may continue with what it was doing previous to being sidetracked by ANTIC. You should be getting the picture by now that although ANTIC is indispensable it causes a slowdown in the 6502 CPU, but how much?  
  
I wrote a simple BASIC program for my Atari 800 in an attempt to answer this question. A FOR/NEXT loop was executed 100,000 times with no intervening statements as follows,.  
  
```
20 FOR 1=1 TO 100000:NEXT I
```
  
The first thing to measure was how long this loop executes with no ANTIC DMA active. A POKE 559,0 turned DMA off and the TV screen went black, A POKE 559,34 turned DMA back on and the original display was restored. The FOR/NEXT loop was executed in graphics modes 0-8 with DMA active and the executive times were observed as shown in table 1. The execution times with DMA increased from as little as 10% for graphics 3 to as much as 47% for graphics 8. It is reasonable to see that if you do a lot of number crunching and you don't need the TV screen or the software timers and game controllers then turn off the ANTIC DMA for a while and you'll get your answer back sooner. It is also apparent from the chart below that your programs will execute faster if you are executing in graphics modes 3, 4, or 5.  
  
I hope you have learned a little bit more about the Atari computer and how the ANTIC DMA interferes with the 6502 CPU. You may in fact someday be able to unleash that latent power within during a computer chess tournament, and when someone asks how in the world you did it you can smile and say - me and my DMA.  
  
  
||graphics mode || execution seconds || % increase (over no-DMA)  
| NO DMA  |  148 |  
| GRAPHICS 0 | 216 | 46  
| GRAPHICS 1 | 188 | 27  
| GRAPHICS 2 | 186 | 26  
| GRAPHICS 3 | 163 | 10  
| GRAPHICS 4 | 164 | 11  
| GRAPHICS 5 | 167 | 13  
| GRAPHICS 6 | 173 | 17  
| GRAPHICS 7 | 185 | 25  
| GRAPHICS 8 | 218 | 47  
