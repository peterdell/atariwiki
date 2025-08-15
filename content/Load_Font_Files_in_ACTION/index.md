---
title: Load Font Files in ACTION
---
# Load Font Files in ACTION!  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	28.03.90   
  
```
;********************************
;**									 **
;** Phoenix SoftCrew ACTION!	**
;** Programme und Tips f. 8Bit **
;**									 **
;** Carsten Strotmann			 **
;**									 **
;********************************

; Programname:Font Lader
; done by:Carsten Strotmann
; Filename:FONT.ACT
; first Version:28.03.90
; last chnage:28.03.90
; Font Handling

; needs IO.ACT
;

							
PROC Font_Load (BYTE ARRAY file,BYTE page)

  Close (1)
  Open (1,file,4)

  Bget (1,page*$100,$400)

  Close (1)

RETURN

PROC Font (BYTE page)

  BYTE chbas=$2F4

  chbas=page

RETURN

PROC Old_Font ()

  Font ($E0)

RETURN

BYTE FUNC Set_Ramtop (BYTE page)

  BYTE ramtop=$6A,crmode=$57

  ramtop==-page

  Graphics (crmode)

RETURN (ramtop)
```
