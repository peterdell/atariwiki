# Query Console Keys  
  
General Information  
  
Author: 	Paul B. Loux   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	1986   
  
## How to use  
  
Description: three functions are provided which test if the user is pressing one of the START, SELECT or OPTION console buttons. Returns a one if pressed, zero if not.  
  
```
;************************************
;*											 *
;*(C)Copyright 1986 by Paul B. Loux *
;*											 *
;* These routines are in the public *
;* domain,  and  are not to be sold *
;* for a profit. They may be freely *
;* distributed, provided  that this *
;* header remains in place. Use and *
;* enjoy! PBL, CIS 72337,2073.		*
;*											 *
;************************************
;*											 *
;*  File CONSOL.LIB					  *
;*											 *
;*  Description: three functions	 *
;*	 are provided which test if	 *
;*	 the user is pressing one of	*
;*	 the START, SELECT or OPTION	*
;*	 console buttons.  Returns a	*
;*	 one if pressed, zero if not.  *
;*											 *
;************************************

MODULE

BYTE CONSOL=$D01F

BYTE FUNC Start()
  IF CONSOL&1 THEN RETURN(0) FI
RETURN(1)

BYTE FUNC Select()
  IF CONSOL&2 THEN RETURN(0) FI
RETURN(1)
 
BYTE FUNC Option()
  IF CONSOL&4 THEN RETURN(0) FI
RETURN(1)

;************************************
;
; Example of usage: 

PROC Test6()

BYTE value

DO

IF Start() THEN PRINTE("Start") FI
IF Option() THEN PRINTE("Option") FI
IF Select() THEN PRINTE("Select") FI

OD

RETURN
```
