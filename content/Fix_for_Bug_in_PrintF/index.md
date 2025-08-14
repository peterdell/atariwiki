  
  
# Fix for PrintF Routine  
  
  
Fix for PrintF on Action! Toolkit  
  
The PrintF routine on the Action!  
Toolkit works great unless you try to  
print a CARD value greater than  
32767, or try to print the INT value  
-32768.  The reason these problems  
occur is that the PROC PF_NBase in  
the PRINTF.ACT file uses the "/" and  
"MOD" operators, which call the  
cartridge divide routine.  The divide  
routine is a SIGNED divide, so it  
doesn't work for large card values.  
The solution is to insert an UNSIGED  
divide routine into the PRINTF.ACT  
file and use it, instead.  First,  
insert the following code at the  
beginning of PRINTF.ACT:  
```
  CARD Quotient, Remainder

  PROC UDiv( CARD a, divisor )
      DEFINE GETCARRY="~[$2E carry]"
      BYTE carry, i
      CARD temp

      Remainder = 0
      FOR i = 1 TO 16
        DO
          Remainder ==LSH 1
          Quotient ==LSH 1
          IF (a&$8000)#0 THEN
              Remainder ==% 1
          FI
          a ==LSH 1
          temp = Remainder - divisor
          GETCARRY
          IF (carry&1)#0 THEN
              Remainder = temp
              Quotient ==+ 1
          FI
        OD
  RETURN
```
  
Some code in the PROCedure PF_NBase  
must also be changed.  Find the  
section of code that reads as  
follows:  
```
    WHILE n>0
      DO
      d=n MOD base      <-
      IF d<10 THEN
        d==+'0
      ELSE
        d==+55
      FI
      s(ptr)=d
      ptr==-1
      length==+1
      n=n/base          <-
      OD
```
And change the two lines indicated so  
the code reads like this:  
```
    WHILE n>0
      DO
      UDiv( n, base )   <-
      d=Remainder       <-
      IF d<10 THEN
        d==+'0
      ELSE
        d==+55
      FI
      s(ptr)=d
      ptr==-1
      length==+1
      n=Quotient        <-
      OD
```
  
The resulting PrintF routine will  
work properly for all CARD and  
INTeger numbers.  
  
  
