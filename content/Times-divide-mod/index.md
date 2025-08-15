---
title: Times-divide-mod
---
__*/mod__ "times-divide-mod" ( n1 n2 n3 -- n4 n5 )  
  
  
  
||Forth79||Forth83||ANSI||Forth200x  
|    X    |   X    |  X  |    X  
  
  
  
%%tabbedSection  
%%tab-english  
Multiply n1 by n2 producing the intermediate double-cell result d. Divide d by n3 producing the single-cell remainder n4 and the single-cell quotient n5. An ambiguous condition exists if n3 is zero, or if the quotient n5 lies outside the range of a single-cell signed integer.  
/%  
%%tab-deutsch  
Zuerst wird n1 mit n2 multipliziert und ein 32-bit Zwischenergebnis er­zeugt. n4 ist der Rest und n5 der Quotient aus dem 32-bit-Zwischener­gebnis und dem Divisor n3. n4 hat das gleiche Vorzeichen wie n3 oder ist Null. Das Produkt von n1 mal n2 wird als 32-bit Zwischenergebnis dargestellt, um eine größere Genauigkeit gegenüber dem sonst gleichwer­tigen Ausdruck n1 n2 * n3 /mod zu erhalten. Eine Fehlerbedingung be­steht, falls der Divisor Null ist oder der Quotient außerhalb des Inter­valls (-32768...32767) liegt.  
/%  
/%  
  
