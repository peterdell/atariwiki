  
  
# ATARI Rainbow Effect  
  
```
;**********************************************************************
;*                                                                    *
;* PhoeniX SoftCrew  ACTION! Programme                                *
;**********************************************************************


;  Programmname    :Rainbow
;  Filename        :RAINBOW.ACT
;  von             :Carsten Strotmann
;  letzte Aenderung:12.10.91
;  Bemerkung       :fuer M.Heinzig


PROC Rainbow ()

BYTE vcount=$D40B, wsync=$D40A,
     rtclok=$14, color=$D018, u=$7,
     ch=764

 ch=$FF

 DO
  wsync=u
  color=vcount+rtclok
 UNTIL ch#$FF
 OD

RETURN

```
  
