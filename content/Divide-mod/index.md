---
title: Divide-mod
---
__/mod__ "divide-mod" ( n1 n2 -- n3 n4 )  
  
  
  
||Forth79||Forth83||ANSI||Forth200x  
|   X     |   X    |  X  |    X  
  
  
  
%%tabbedSection  
%%tab-english  
Divide n1 by n2, giving the single-cell remainder n3 and the single-cell quotient n4. An ambiguous condition exists if n2 is zero.  
/%  
%%tab-deutsch  
n3 ist der Rest und n4 der Quotient aus der Division von n1 durch den Divisor n2. n3 hat dasselbe Vorzeichen wie n2 oder ist Null. Eine Fehlerbedinguag besteht, wenn der Divisor Null ist oder der Quotient ausserhalb des Intervalls (-32768 .. 32767 ) liegt.  
/%  
/%  
  
