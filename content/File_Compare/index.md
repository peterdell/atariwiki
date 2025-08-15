---
title: File Compare
---
# File Compare in ACTION!  
  
General Information  
  
Author: 	Mark Rose   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	March, 1985   
  
Compare - Check if two files are the same.  
  
```
; Compare - Check if two files are
;	the same.

; by Mark Rose - March, 1985


PROC CmpFile( BYTE f1, f2 )
	 BYTE c1, c2
	 CARD i,
			nErrors

	 i = 0
	 nErrors = 0
  ; Until end-of-file, compare a char
  ; from each file and bump count of
  ; errors, if not the same.
	 DO
		; Get one character from each file.
		  c1 = GetD( f1 )
		  c2 = GetD( f2 )
		  IF (EOF(f1)#0) OR (EOF(f2)#0) THEN
				EXIT
		  FI
		; If chars dont compare, inform
		; user.
		  IF c1 # c2 THEN
				nErrors ==+ 1
				PrintF( "%H: %H %H%E", i, c1, c2 )
		  FI
		  i ==+ 1
	 OD
	 IF (EOF(f1)#0) AND (EOF(f2)=0) THEN
		  PrintE( "File 1 is shorter" )
	 ELSEIF (EOF(f1)=0) AND (EOF(f2)#0) THEN
		  PrintE( "File 2 is shorter" )
	 ELSE
		  IF nErrors = 0 THEN
				PrintE( "Files compare exactly" )
		  ELSE
				PrintE( "Files are the same length" )
		  FI
	 FI
RETURN



PROC Compare()
  ; Need strings for two file names.
	 BYTE ARRAY fn1( 30 ), fn2( 30 )

  ; Get the two input files
	 Print( "File 1: " )
	 InputS( fn1 )
	 Print( "File 2: " )
	 InputS( fn2 )

  ; and open them.
	 Close( 1 )
	 Open( 1, fn1, 4, 0 )
	 Close( 2 )
	 Open( 2, fn2, 4, 0 )

  ; Perform the compare
	 CmpFile( 1, 2 )

  ; and close up.
	 Close( 1 )
	 Close( 2 )
RETURN
```
