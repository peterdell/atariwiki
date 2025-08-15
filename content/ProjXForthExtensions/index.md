---
title: ProjXForthExtensions
---
  
  
# X-Forth Definitions  
  
  
### ?  
  
```
: ? ( addr -- )
  @ . ;
```
  
### Alias  
  
```
: ALIAS ( xt -- )
  <BUILDS CFA , DOES> @ EXECUTE ;
```
  
### Align  
  
```
: ALIGN ( -- )
  HERE 1 AND ALLOT ;
```
  
### Aligned  
  
```
: ALIGNED ( addr -- a-addr )
  DUP 1 AND + ;
```
  
  
### Cell+  
  
```
: CELL+ ( a-addr1 -- a-addr2 )
  2 + ;
```
  
### Cells  
  
```
: CELLS ( n1 -- n2 )
  2 * ;
```
  
  
### CVariable  
  
```
:  CVARIABLE ( b -- )
  <BUILDS C, DOES> C@ ;
```
  
### Defer  
  
```
: DEFER ( -- )
  <BUILDS 0 , DOES> @ DUP IF EXECUTE ELSE DROP THEN ;
```
  
### IS  
  
```
: IS ( xt -- )
  ~[COMPILE] ' ! ;
```
  
### To  
  
```
: TO ( x -- )
  ~[COMPILE] ' CELL+ ! ;
```
  
### Value  
  
```
: VALUE ( x -- )
  <BUILDS , DOES> @ ;
```
  
  
  
