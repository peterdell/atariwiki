---
title: Forth Macros
---
# Collection of Forth Macro definitions  
  
## Wil Baden  
  
```
( A New Definition for Simple Macro ) 

( The simplest form of macro -- parameterless string replacement. 

: MACRO :   
    CHAR WORD COUNT POSTPONE SLITERAL 
    POSTPONE EVALUATE 
    POSTPONE ; IMMEDIATE 
; 

Parameters can be provided by replacing `EVALUATE` with `SEQUENTIAL-EVALUATE`. 
I believe such definition works on all Standard Forths. 

) 

( Simple Macro -- Evaluate Alternating Texts and Parameters Sequentially. ) 

    : SPLIT-AT-CHAR              ( a n char -- a+k n-k a k ) 
        >R  2DUP                             ( a n a+k n-k)( R: char) 
            BEGIN  DUP WHILE  OVER C@ R@ = 
            0= WHILE  1 /STRING  REPEAT THEN 
        R> DROP                                            ( R: ) 
        DUP >R  2SWAP  R> -                  ( a+k n-k a k) 
    ; 

    : SEQUENTIAL-EVALUATE      ( ... caddr u "ccc"... -- ??? ) 
        BEGIN                                          ( caddr u) 
            [CHAR] \ SPLIT-AT-CHAR  2SWAP SWAP >R >R   ( caddr u) 
            EVALUATE                                   ( ) 
        R@ WHILE 
            BL WORD COUNT EVALUATE   
            R> R> SWAP  1 /STRING                      ( caddr u) 
        REPEAT                                         ( ) 
        R> R> 2DROP 
    ; 

: MACRO :   
    CHAR WORD COUNT POSTPONE SLITERAL 
    POSTPONE SEQUENTIAL-EVALUATE 
    POSTPONE ; IMMEDIATE 
; 

( Examples. ) 
MACRO :GO " ANEW NONCE : (GO) " 
MACRO GO  " (GO) NONCE " 
MACRO ??  " IF \ THEN " 
MACRO #DO " 0 MAX 0 ?DO " 
MACRO ORIF  " ?DUP 0= IF " 
MACRO ANDIF " DUP IF DROP " 
MACRO H     " HEX \ DECIMAL " 
MACRO 'TH   " CELLS \ + " 

( 
-- 
Wil Baden   Costa Mesa, California 
)
```
