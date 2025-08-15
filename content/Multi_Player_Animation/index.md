---
title: Multi Player Animation
---
# Multi Player Animation  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
  
for MPA files created by Peter Finzels Multi-Player Animator  
  
see also Multi Player Animator  
  
```
;********************************
;**                            **
;** Phoenix SoftCrew ACTION!   **
;** Programme und Tips f. 8Bit **
;**                            **
;** Carsten Strotmann          **
;**                            **
;********************************

; Programname:MPA-Modul
; done by:Carsten Strotmann
; Filename:MPA.ACT
; first Version:01.03.90
; last change:01.03.90

; Player Animation
;
;

; INCLUDE "PMGR.ACT"
; needs PMGR.ACT 

PROC MPA_Load (BYTE ARRAY shape,file)

  Close (1)
  Open (1,file,4)
  Bget (1,shape,$100)
  Close (1)

RETURN

PROC MPA_Set ()

 BYTE gprior=$26F,u
 gprior==%$20

 FOR u=0 TO 3
 DO
  P_Size (u,0)
 OD

RETURN

PROC Animate (BYTE num,x,y,phase,BYTE ARRAY shape)

  CARD shapeph

  shapeph=shape+phase*$10

  P_Pos (num*2,x,y,shapeph,$10)
  P_Pos (num*2+1,x,y,shapeph+$80,$10)

RETURN
```
