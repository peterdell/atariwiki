---
title: Page Flip Routine for Basic
---
# Page Flip Routine for Basic  
  
  
## Page Flip  
  
```
10 ;Page flipping routine. After using
20 ;GR.24, GR.9-11, call this routine
30 ;with X=USR(1536) to toggle
40 ;background and foreground page.
50 ;Background page is the one that
60 ;PLOT and DRAWTO effect, and
70 ;foreground is the one that is
75 ;displayed.
80 ;
90       *=  $0600
0100 MEMTOP = $02E5  Mem top pointer.
0110 SAVMSC = $58    Video mem pointer
0120 SDLSTL = $0230  Start of DL.
0130 DLPNT1 = $CB    Two unused words
0140 DLPNT2 = $CD    in zero page.
0150     LDY #0
0160     CLC 
0170     LDA SDLSTL  Find the
0180     ADC #5      two
0190     STA DLPNT1  display
0200     LDA SDLSTL+1 list
0210     ADC #0      references
0220     STA DLPNT1+1 to video
0230     LDA DLPNT1  memory
0240     ADC #96     and store
0250     STA DLPNT2  them in
0260     LDA DLPNT1+1 unused
0270     ADC #0      part of
0280     STA DLPNT2+1 page 0.
0290     LDA SDLSTL+1 Find area
0300     SEC         to store
0310     SBC #31     screen 2
0320     STA MEMTOP+1 safely.
0330     LDA SAVMSC+1 Insure that
0340     CMP (DLPNT1),Y foreground
0350     BNE NORM    and
0360     LDA MEMTOP+1 background
0370     STA SAVMSC+1 are
0380     BNE CLEAR   different.
0390 NORM TAX        Swap both
0400     LDA (DLPNT1),Y of the
0410     STA SAVMSC+1 foreground
0420     TXA         pointers
0430     STA (DLPNT1),Y and
0440     CLC         the one
0450     ADC #$0F    background
0460     STA (DLPNT2),Y pointer.
0470 CLEAR LDA SAVMSC+1 Set up the
0480     STA SCRPNT+1 indexed
0490     LDA SAVMSC  addressing
0500     STA SCRPNT  command.
0510     LDA #0      Quickly
0520     LDX #30     clear
0530 LOOP STA 0,Y    out
0540     INY         7680 byte
0550     BNE LOOP    buffer
0560     INC SCRPNT+1 for the
0570     DEX         new
0580     BNE LOOP    screen.
0590     PLA         Unused parameter
0600     RTS         Return.
0610 SCRPNT = LOOP+1
0620 ;The SCRPNT pointer is used to
0630 ;modify code on the fly.  This
0640 ;allows us to use Indexed
0650 ;addressing which is faster
0660 ;than Post-indexed indirect
0670 ;addressing in the inside loop.
0680     .END 

```
  
## Copy / Clear Page  
  
```
10 ;Page flipping routine. After using
20 ;GR.24, GR.9-11, call this routine
30 ;with X=USR(1664) to copy backgrnd
40 ;to foregrnd page.  Backgrnd page
50 ;is the one PLOT and DRAWTO
60 ;effect, and foregrnd is the one
70 ;displayed.
80 ;To clear the whole background
90 ;screen, just do an X=USR(1715)
0100 ;
0110     *=  $0680
0120 MEMTOP = $02E5  Mem Top pointer.
0130 SAVMSC = $58    video mem pointer
0140 SDLSTL = $0230  Pointer to DL
0150     LDX SDLSTL+1 Find an
0160     INX         area
0170     STX FORPNT+1 to store
0180     TXA         background
0190     SEC         screen
0200     SBC #32     and set
0210     STA MEMTOP+1 up the
0220     STA SAVMSC+1 indexed
0230     STA BAKPNT+1 addressing
0240     LDA SAVMSC  commands
0250     STA BAKPNT  for
0260     STA FORPNT  copying.
0270     LDY #0      Copy
0280     LDX #30     the
0290 LOOP LDA 0,Y    7680
0300     STA 0,Y     byte
0310     INY         background
0320     BNE LOOP    buffer
0330     INC BAKPNT+1 to
0340     INC FORPNT+1 the
0350     DEX         foreground
0360     BNE LOOP    screen.
0370     PLA         Unused parameter
0380     RTS         Return.
0390 CLS LDA SDLSTL+1 Make sure
0400     SEC         there's a
0410     SBC #31     background
0420     STA MEMTOP+1 screen.
0430     STA CLSPNT+1 Set
0440     LDA SAVMSC  indexed
0450     STA CLSPNT  addressing.
0460     LDA #0      Fill
0470     LDX #30     the
0480     LDY #0      7680
0490 LOOP2 STA 0,Y   byte
0500     INY         background
0510     BNE LOOP2   buffer
0520     INC CLSPNT+1 with
0530     DEX         zeroes
0540     BNE LOOP2   (clear).
0550     PLA         Pull unused argument.
0560     RTS         Return.
0570 CLSPNT = LOOP2+1
0580 BAKPNT = LOOP+1
0590 FORPNT = LOOP+4
0600     .END 
```
