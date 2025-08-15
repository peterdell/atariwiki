---
title: Clear Screen
---
# Clear Screen  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	FORTH   
Compiler/Interpreter: 	volksForth   
Published: 	2007   
  
The word CLS clears the screen and sets the cursor to the home position. This is done on the Atari by printing the ATASCII value 125.  
  
In some Forth Versions this is an alias for the word PAGE.  
  
```
 : CLS \\ Clear Screen
  &125 EMIT ;
```
