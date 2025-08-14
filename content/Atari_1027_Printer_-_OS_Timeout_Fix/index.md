  
  
# Atari 1027 Printer, OS Timeout Fix  
  
```
;      ----------------------------------------------------------------
;      1027 Printer Timeout Fix  (Ver. 2)                 (AUTORUN.SYS)
;      Joe Miller   10 Mar 1985
;
;      This patch corrects the 1027 printer timeout problem by prevent-
;      ing the Operating System from generating an incorrect Data Frame
;      checksum.  It consists of two logical modules.  The first module
;      is executed once (at initialization) to chain into the "serial
;      output ready" IRQ process.  The second module is invoked when an
;      IRQ is generated for each serial output byte.  It checks to see
;      if an invalid checksum is going to be sent for the current data
;      frame, and, if so, prevents it from happening.
;
;      NOTE:  This code is implemented as a standard "AUTORUN.SYS" file
;             so that it may be used with any version of ATARI DOS.
;             With some care, it may also be embedded directly within
;             your own application program.  Note usage of cassette
;             buffer.  Assemble with AMAC.
;      ----------------------------------------------------------------


FIXORG EQU     $0480           ; Location of SIO patch
VSEROR EQU     $020C           ; Serial Output Ready IRQ vector
CHKSUM EQU     $0031           ; SIO checksum accumulator
BUFRLO EQU     $0032           ; SIO output buffer pointer


       ORG     FIXORG          ; Start SIO patch
       PHP                     ; Save processor status
       SEI                     ; Disable IRQs for a moment
       LDA     VSEROR          ; Save current SIO output ready address
       STA     UVSER
       LDA     VSEROR+1
       STA     UVSER+1
       LDA     #low SIOFIX     ; Chain our fix into IRQ process
       STA     VSEROR
       LDA     #high SIOFIX
       STA     VSEROR+1
       PLP                     ; Re-enable interrupts
       RTS                     ; Return to OS -->

YSAVE  DS      1               ; Temporary for Y-register 
UVSER  DS      2               ; Serial Output Ready IRQ chain address

SIOFIX LDA     CHKSUM          ; For each SIO 'Output Ready' interrupt
       BNE     SIOJMP          ; If current checksum is zero, then
       STY     YSAVE           ;    Save Y register
       LDY     #0              ;    Initialize index
       LDA     (BUFRLO),Y      ;    Get first buffer byte
       BEQ     YRESTR          ;    If 1st byte <> 0, then
       PLA                     ;       This data frame would cause timeout
       STA     CHKSUM          ;       Save stacked byte in checksum
       INY                     ;       Bump output buffer index
       CLC                     ;       'Pre-calculate' corrected checksum
       LDA     (BUFRLO),Y      ;       Add second byte in output buffer
       ADC     CHKSUM          ;       To first byte    (already sent)
       ADC     #0              ;       Including possible carry
       PHA                     ;       Save it on stack (NOT in CHKSUM!!)
                               ;    Endif
YRESTR LDY     YSAVE           ;    Restore Y-register
                               ; Endif
SIOJMP JMP     (UVSER)         ; Chain into system's interrupt server

       END     FIXORG          ; End ----------------------------------

```
  
