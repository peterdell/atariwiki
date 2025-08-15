---
title: ProjXForthSieve
---
  
  
# Sieve of Eratosthenes Benchmark  
  
---
from Sieve of Eratosthenes Benchmark Page  
http://www.bagley.org/~doug/shootout/bench/sieve/sieve.gforth  
  
With many annotations  
http://www.bagley.org/~doug/shootout/bench/sieve/alt/ann.sieve.forth  
  
gives wrong result in XFORTH, have to investigate  
---
```
DECIMAL

8192 CONSTANT SIZE

1 VARIABLE FLAGS SIZE 2 - ALLOT

FLAGS SIZE + CONSTANT ENDFLAGS

: FLAGMULTS ( n toaddr fromaddr -- )
  DO
    0 I C! DUP
  +LOOP ;

: PRIMES ( -- n )
FLAGS SIZE -1 FILL
0 2
ENDFLAGS FLAGS
DO
  I C@
  IF
    DUP I + DUP ENDFLAGS <
    IF
      ENDFLAGS SWAP FLAGMULTS
    ELSE
      DROP
    THEN
    SWAP 1+ SWAP
  THEN
  1+
LOOP
DROP ;
```
---
  
Original BYTE FORTH Benchmark  
http://www-personal.umich.edu/~williams/archive/forth/utilities/byteprimes.fs.html  
  
```
( Eratosthenes sieve benchmark )
( original BYTE benchmark )

8190 CONSTANT SIZE
-1 VARIABLE FLAGS SIZE ALLOT

: PRIMES
  FLAGS SIZE -1 FILL
  0 SIZE 0 DO
    I FLAGS + C@ IF
      I 2 * 3 + DUP I + BEGIN
        DUP SIZE < WHILE
          DUP FLAGS + 0 SWAP C! OVER +
      REPEAT DROP DROP 1+
  THEN LOOP ;

```
  
---
  
  
from GNU Forth distribution (Bernd Paysan)  
http://www.jwdt.com/~paysan/gforth.html  
  
```
( Sieve by bernd paysan )

DECIMAL

-1 VARIABLE FLAGS 8190 ALLOT
FLAGS 8190 + CONSTANT EFLAG

: PRIMES ( -- n )
FLAGS 8190 -1 FILL 0 3 EFLAG FLAGS
DO I C@
  IF DUP I + DUP EFLAG <
    IF EFLAG SWAP
      DO 0 I C! DUP +LOOP
    ELSE DROP THEN SWAP 1+ SWAP
    THEN 2 +
  LOOP DROP ;

```
  
