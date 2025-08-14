  
  
# Jump to DOS  
  
```
;
; TODOS.ACT
;

;  This little PROCedure allows you to exit any ACTION! program to the
;  ATARI DOS 2.0S DUP.SYS Menu.
;
;  WARNING:  This PROC will work properly ONLY if you have WARM booted
;            your system with an ATARI 2.0S DOS.SYS file on the diskette
;            in Drive #1.  Furthermore, you must have a diskette with
;            with DUP.SYS on it in Drive #1 before calling this PROC.
;
;  You may return to the ACTION! environment by selecting option "B"
;  (Run Cartridge) from the DUP.SYS Menu, but your ACTION! program will
;  have been wiped out by the exit to DUP.SYS!
;
;
;  Enjoy!
;
;  Brad Paulsen [CIS PPN 70035,1050]


PROC ToDOS()
               
  [
   $6C$0A$00
  ]

RETURN

```
  
  
