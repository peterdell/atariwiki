# Accessing Memory  
  
  
## Reading Memory locations  
  
In Basic, we use PEEK(addr) to read a memory location. This example read the first joystick  
  
```
...
100 STICK = PEEK(632)
110 IF STICK = 15 THEN PRINT "centered"
120 IF STICK = 14 THEN PRINT "up"
130 IF STICK = 13 THEN PRINT "down"
...
```
  
In Forth, there are two words to read memory. {{{ @ }}} (called FETCH) reads a 16bit value from a memory location and places the value on the stack. {{{ C@ }}} (called C-FETCH) reads a 8bit value (a byte).  
  
Both words need (=consume) the address on the stack.  
  
```
@  ( addr -- 16b )
C@ ( addr --  8b )
```
In the Atari, Memory location 632 ([STICK0](../STICK0/index.md)/$278) is the shadow register for the first joystick port ([PORTA](../PORTA/index.md)/54016).  
So the above BASIC example would be in FORTH:  
  
```
&632 C@
DUP 15 = IF ." centered " THEN
DUP 14 = IF ." up " THEN
    13 = IF ." down " THEN
    
```
  
## Writing memory locations  
  
The counterpart to @ (FETCH) and C@ (C-FETCH) are ! (STORE) and C! (C-STORE). These words take a value and an address from the stack and store the value at the address. The Stack comments for this words are:  
  
```
!   ( 16b addr -- )
C!  (  8b addr -- )
```
  
The below BASIC line changes the background color of the screen to black, writing the value 0 in memory location 709 ([COLOR1](../COLOR1/index.md)):  
  
```
100 POKE 709,0
```
  
In Forth, we write  
```
0 709 C!
```
