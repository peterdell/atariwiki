# Load APL Display-List Files  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION   
Published: 	24.03.90   
  
```
;********************************
;**                            **
;** Phoenix SoftCrew ACTION!   **
;** Programme und Tips f. 8Bit **
;**                            **
;** Carsten Strotmann          **
;**                            **
;********************************

; Programname:DL-Lade Modul
; done by:Carsten Strotmann
; Filename:DLLOAD.ACT
; first Version:24.03.90
; last change:24.03.90
; load APL-Displaylist
;

PROC Dlload (BYTE ARRAY file)

BYTE byt
CARD start,end

BYTE POINTER adr

Close (1)
Open (1,file,4)

WHILE EOF(1)=0
DO
start=GetD (1)
start==+GetD(1)*$100

IF start=$FFFF THEN
start=GetD (1)
start==+GetD(1)*$100

end=GetD (1)
end==+GetD (1)*$100

FOR adr=start TO end
DO
byt=GetD(1)
adr^=byt
OD
FI
OD

RETURN
```
