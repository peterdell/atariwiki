---
title: Implementations of NEXT on 6502
---
# Implementations of NEXT in Forth Systems for the 6502 CPU  
  
### FIG-FORTH (also X-FORTH, ANTIC FORTH and other derivatives of FIG-FORTH ...)  
  
```
NEXT
   LDY #1
   LDA (IP),Y ; Hi-Byte of wordaddress
   STA W+1    ; store in W-Reg
   DEY
   LDA (IP),Y ; Lo-Byte of wordaddress
   STA W      ; store in W-Reg
   CLC
   LDA IP     ; increment IP by 2
   ADC #2
   STA IP
   BCC L54
   INC IP+1
L54
   JMP W-1    ; indirect jump to (W)

```
### 64FORTH (Tom Zimmer)  
```
NEXT  LDY   #1 
      LDA  (IP),Y 
      STA   W+1 
      DEY 
      LDA  (IP),Y 
      STA  W 
      LDA  (W),Y 
      STA  TMP 
      INY 
      LDA  (W),Y 
      STA   TMP+1 
      DEY 
      CLC 
      LDA   IP 
      ADC  #2 
      STA   IP 
      BCC  L816E 
      INC   IP+1 
L816E  JMP  (TMP)
```
See [http://groups.google.de/group/comp.lang.forth/browse_thread/thread/19f7f2102e020583/8d1b52cf069d1258](http://groups.google.de/group/comp.lang.forth/browse_thread/thread/19f7f2102e020583/8d1b52cf069d1258)  
  
### FOCO65  
  
[https://github.com/piotr-wiszowaty/foco65](https://github.com/piotr-wiszowaty/foco65)  
  
```
next
 ldy #0
 lda (ip),y  ; lade naechste Adresse (IP=Instruction Pointer)
 sta w       ; und speichere in die Speicherstelle "w"
 iny
 lda (ip),y
 sta w+1
 lda #2      ; den Instruction-Pointer um zwei erhoehen, so das
 clc         ; dieser auf den naechsten Befehl zeigt
 adc ip
 sta ip
 lda #0
 adc ip+1
 sta ip+1
 ldy #0
 lda (w),y   ; Sprung-Adresse des naechsten Befehls laden
 sta z       ; und in die Speicherstelle "z" schreiben
 iny
 lda (w),y
 sta z+1
 jmp (z)     ; indirekt an die Adresse in Speicherstelle "z"
             ; springen
```
