### XEP 80 Driver for X-Forth  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	FORTH   
Compiler/Interpreter: 	X-Forth   
Published: 	April 2004   
  
This version also works with enhanced 40 Column E: Handler as well as with Software 80 Column Handler (F80.COM, only under BEWE-DOS)  
  
Have fun  
  
Carsten Strotmann carsten@strotmann.de  
  
## How to use  
  
How to build XFORTH with custom E: Handler driver:  
  
XEP80.F This file adds commands to XFORTH to patch the current E: handler vector into XFORTH (CHOUT, $3772 ff.).  
  
Step 1: launch XFORTH.ORG. XFORTH.ORG is a special version of XFORTH without startup banner.  
  
Step 2: Include XEP80.F -> INCLUDE" D:XEP80.F"  
  
Step 3: Save new XFORTH -> INCLUDE" D:MKFRTH.F"  
  
Step 4: Test new XFORTH  
  
```
( PATCH XFORTH E: Handler )

HEX

: GETEHAND ( get address of	  )
			  ( current E: Handler )
  22 0 DO
	 33B I - C@ 
	 45 = IF
		33C I - @ THEN
	 3 +LOOP ;

: CHADR  ( get address of )
			( CHOUT Routine  )
  ' MON 36 + ;

: PATCHE ( Patch XFORTH )
  GETEHAND 6 + DUP 1+
  CHADR !
  CHADR 4 + ! ;

: XEP80 ( Autostart command )
  PATCHE
  44 ' C/L ! 4F 53 C!
  7D EMIT CR
  ." X-FORTH 1.1c 040412/cs" CR
  ." XEP80 Driver" CR CR
  ." OK" CR
  QUIT ;

DECIMAL
```
