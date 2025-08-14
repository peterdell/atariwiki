# Floored Arithmetics  
  
  
If z is any real number, then the floor of z is the greatest integer less than or equal to z.  
  
- The floor of +.6 is 0  
- The floor of -.4 is -1  
  
## floored division  
  
Integer division in which the remainder carries the sign of the divisor or is zero, and the quotient is rounded to its arithmetic floor.  Note that, except for error conditions, n1 n2 SWAP OVER /MOD ROT * + is identical to n1.  
  
Examples:  
  
|| dividend || divisor || remainder || quotient  
|   10   |     7   |     3   |       1  
|   -10  |      7  |      4  |       -2  
|    10  |     -7  |     -4  |       -2  
|   -10  |     -7  |     -3  |        1  
  
