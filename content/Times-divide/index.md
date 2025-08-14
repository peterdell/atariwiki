__*/__ "times-divide" ( n1 n2 n3 -- n4 )  
  
  
  
||Forth79||Forth83||ANSI||Forth200x  
|    X    |   X    |  X  |    X  
  
  
  
%%tabbedSection  
%%tab-english  
Multiply n1 by n2 producing the intermediate double-cell result d. Divide d by n3 giving the single-cell quotient n4. An ambiguous condition exists if n3 is zero or if the quotient n4 lies outside the range of a signed number.  
/%  
%%tab-deutsch  
Zuerst wird n1 mit n2 multipliziert und ein 32-bit Zwischenergebnis er­zeugt. n4 ist der Quotient aus derm 32-bit Zwischenergebnis und dem Divisior n3. Das Produkt von n1 mal n2 wird als 32-bit Zwischenergebnis dargestellt, um eine größere Genauigkeit gegenüber dem sonst gleichwer­tigen Ausdruck n1 n2 * n3 / zu erhalten. Eine Fehlerbedingung besteht, wenn der Divisor Null ist, oder der Quotient auperhalb des Intervalls (­ -32768.. 32767) liegt.  
/%  
/%  
  
