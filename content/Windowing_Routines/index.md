# Windowing Routines  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
  
```
;******************************
;**								  **
;** PHOENIX SOFTCREW			**
;** STANDARTROUTINEN			**
;** WINDOWS "WINDOW.INC"	  **
;******************************


PROC W_Init=$9800()

;-------------------------------------

PROC W_Load ()

Close (6)
Open (6,"D:WINDOW.OBJ",4,0)

Bget (6,$9800,$3F9)

Close (6)

W_Init ()

Open (6,"W:",12,0)

RETURN

;------------------------------------

PROC W_Open (BYTE xp,yp,xl,yl)


XIO (6,0,52,xp,yp,"W:")

XIO (6,0,50,xl,yl,"W:")

RETURN

;------------------------------------

PROC W_Close ()

XIO (6,0,51,0,0,"W:")

RETURN

;-----------------------------------
PROC W_Pos (BYTE x,y)

XIO (6,0,53,x,y,"W:")

RETURN

;-----------------------------------
PROC WMem (BYTE posh,posl,lenh,lenl)

XIO (6,0,54,posh,posh,"W:")

XIO (6,0,55,lenh,lenl,"W:")

RETURN
;-----------------------------------

PROC W_Print (BYTE x,y,BYTE ARRAY text)

 W_Pos (x,y)
 PrintD (6,text)

RETURN

;-----------------------------------

PROC W_InputS (BYTE x,y,BYTE ARRAY out,text)

 W_Print (x,y,out)
 InputSD (6,text)

RETURN
;-----------------------------------

PROC W_Cls ()

 PutD (6,$7D)

RETURN
;-----------------------------------
PROC W_PrintB (BYTE x,y,val)

 W_Pos (x,y)
 PrintBD (6,val)

RETURN
;-----------------------------------
PROC W_PrintC (BYTE x,y,CARD val)

 W_Pos (x,y)
 PrintCD (6,val)

RETURN
;-----------------------------------
```
