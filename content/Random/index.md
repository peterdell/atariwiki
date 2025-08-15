---
title: Random
---
# Creating Random numbers  
  
this code is Atari 8bit specific, as its using the POKEY chip as the source for randomness  
  
```
: RND ( -- n ) \\ Random Number 0-$FF
  $D20A C@ ;

\\ Random Numner 0..n-1
: RANDOM ( n -- 0..n-1 )
  RND $100 * RND + UM* NIP ;
```
  
RND will return a random number between 0 - 255 from the Pokey Noise Randomizer. The Word RANDOM will return a 16bit random number between 0-65535.  
