# File Select Shell  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
  
This code requires the [Binary_File_Load_in_ACTION](../Binary_File_Load_in_ACTION/index.md) Module and the [File_Select_Box](../File_Select_Box/index.md) Module  
  
```
;********************************
;**									 **
;** Phoenix SoftCrew ACTION!	**
;** Programme und Tips f. 8Bit **
;**									 **
;** Carsten Strotmann			 **
;**									 **
;********************************

; Programname:ComLoad
; done by:Carsten Strotmann
; Filename:COMLOAD.ACT
; first Version:19.02.90
; last chnage:24.03.90
; Load com files from disk
; MC-Routine by Matthias Drees
;
;

INCLUDE "SYSTEM.ACT"
INCLUDE "DIVERS.ACT"
INCLUDE "STRING.ACT"
INCLUDE "FILESEL.ACT"
INCLUDE "BLOAD.ACT"

PROC ComLoad ()

  BYTE ARRAY file (20)

  AllClose ()
  Bload_Init ()

  Cls ()
  SetColor (2,0,5)
  C_Off ()

  PrintE (" Com File Loader - PhoeniX SoftCrew ")
  PrintE ("------------------------------------")

  Position (5,5)
  Print ("Choose file:")

  Scopy (file,"D1:*.COM")

  DO
	 Filesel (file) 
  UNTIL file(2)#'?
  OD

  Close (1)
  Open (1,file,4,0)

  Bload ()

RETURN
```
