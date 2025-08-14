212-217  
$D4-$D9  
FR0  
  
Floating point register zero; holds a six-byte internal form of the FP number. The value at locations 212 and 213 are used to return a two-byte hexadecimal value in the range of zero to 65536 ($FFFF) to the BASIC program (low byte in 212, high byte in 213). The floating point package, if used, requires all locations from 212 to 255. All six bytes of FR0 can be used by a machine language routine, provided FR0 isn't used and no FP functions are used by that routine. To use 16 bit values in FP, you would place the two bytes of the number into the least two bytes of FR0 (212, 213; $D4, $D5), and then do a JSR to $D9AA (55722), which will convert the integer to its FP representation, leaving the result in FR0. To reverse this operation, do a JSR to $D9D2 (55762).  
