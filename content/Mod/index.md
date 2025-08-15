---
title: Mod
---
__MOD__ "modulo" ( n1 n2 -- n3 )  
  
  
  
||Forth79||Forth83||ANSI||Forth200x  
|    X    |   X    |  X  |    X  
  
  
  
%%tabbedSection  
%%tab-english  
Divide n1 by n2, giving the single-cell remainder n3. An ambiguous condition exists if n2 is zero.  
/%  
%%tab-deutsch  
n3 ist der Rest der Division von n1 durch den Divisor n2. n3 hat daßelbe Vorzeichen wie n2 oder ist Null. Eine Fehlerbedingung besteht, wenn der Divisor Null ist oder der Quotient außerhalb des Intervalls (­-32768..32767) liegt.  
/%  
/%  
