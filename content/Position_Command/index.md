# Position Cursor  
  
The word POS moves the cursor to the X / Y position given.  
  
```
: POS ( x y -- ) \\ Position Cursor 
  $54 C! $55 ! ;
```
  
VolksForth has a build in word called 'at':  
  
```
AT ( row col -- )
```
