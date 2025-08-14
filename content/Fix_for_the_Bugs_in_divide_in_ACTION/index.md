# Fix for the Bugs in divide in ACTION!  
  
```
;The following Action! routine will provide you with a fix for the bugs
;in divide in Action! It should be self-explanatory...

MODULE ; NEWDIVI.ACT

; (c) 1983 ACS

; Copyright (c) 1983
; by Action Computer Services (ACS)
; Permission is granted to duplicate
; and/or distribute the contents of
; this file to any licensed user of
; OSS ACTION.  This copyright notice
; must be replicated in all such
; copies.  Copies of this file may
; not be sold or otherwise used for
; monetary gain.

; This file fixes the problems with
; the ACTION! divide routine and
; should be included within all your
; ACTION! programs until such time
; as an update ROM is available.

; TO USE:
;      'INCLUDE' this file in front
;      of all your PROCedures and
;      FUNCtions.

; e.g. INCLUDE "D2:NEWDIVI.ACT"

PROC DivI=*()
[ $20 $A06C $85 $86 $A2 $10 $26 $82
    $26 $83 $26 $86 $26 $87 $38 $A5
    $86 $E5 $84 $A8 $A5 $87 $E5 $85
    $90 $04 $85 $87 $84 $86 $CA $D0
    $E5 $A5 $82 $2A $26 $83 $A6 $83
    $4C $A032]

PROC REMI=*()
[$20 DivI $86A5 $87A6 $60]

SET $4EA=DivI
SET $4EC=RemI

; End of MODULE NEWDIVI.ACT
```
