---
title: PM examples
---
### PMG examples.  
  
Because some people do have problems every time they try to set PMG, here is simple example showing "A" letter using PMG with mentioning which setting is obligatory and which not.  
In addition, in normal "legal" use (system interrupts on), shadow-registers must be used otherwise efect of writing to registers lasts for at most 1 frame.  
  
It is worth noting, that PMG is drawn by ANTIC (GTIA is fed with bytes read by ANTIC DMA), thus some registers belong to ANTIC, some to GTIA.  
  
```
        org $4000
        ; to avoid blink, here should be a loop waiting for interrupt
        lda #%111110    ; obligatory, double line, no missle DMA;
        sta $22f        ; DMACTL - 62 - single line, normal playfield
        lda #$80        ; obligatory
        sta $D407       ; PMBASE
        lda #$7c        ; obligatory
        sta $D000       ; HPOSP
        lda #1          ; default is good for this example, may be skipped
        sta $26f        ; first PM then PF
        lda #%11        ; obligatory
        sta $D01D       ; GRACTL -set both players and missles        
        lda #2          ; default is good for this example, may be skipped
        sta $D008       ; SIZEP
        lda #$2f        ; this is the color of the
        sta $2c0        ; PCOLR0, surely may be skipped.

        ldx #7
        ; let's display 'A' letter
show
        lda $e108,x     ; get 'A' letter rows from char generator 
        sta $8440,x     ; store it in PLAYER0 memory chunk.
        dex
        bpl show        ; do it eight times
end
        bne end         ; wait for eternity.
        }}}
```
