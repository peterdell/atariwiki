  
  
# OS Vectors  
  
```
MODULE
;*********************************
;** 
;** OS-Vector collection
;** ACTION-Proceduren
;** Januar 1990 by PhoeniX SoftCrew
;**
;** FILE:OSROUT.ACT
;**
;*********************************

;(Jump through DOSVEC $0A)
PROC DOSR =$C434 ()

; (Jump through DOSINI $0C)
PROC DOS =$C649 ()

; (Jump through CASINI $02)
PROC CASINI =$C6AE ()

; (Jump through RUNAD $2E0)
PROC RUNADR =$C7E0 ()

; (Jump through "adr")
PROC JMP =$F2AD ()

PROC Jump (CARD adr)

  CARD addr=$64
  addr=adr
  JMP ()

RETURN

; ( insert line at cursorposition)
PROC INSERT =$F50C ()

; (delete line at cursorposition)
PROC DELETE =$F520 ()

; (move Cursor down to last line)
PROC DOWN =$F55F ()

; (init screen-editor)
PROC EDITOR =$F6BC ()

; (clear line)
PROC CLEARLINE =$F7E2 ()

; (scroll Screen)
PROC SCROLL =$F7F7 ()

; (Keyclick sound)
PROC CLICK =$F983 ()

; (Casette-beep Sound)
PROC BEEPWAIT =$FDFC (BYTE times)

; (read key)
PROC KBGET =$F302 ()

```
  
