---
title: Disable BREAK key
---
# Disable BREAK Key (for BASIC USR call)  
  
```
00010          .LI OFF
00020 *
00030 *************************
00040 *                       *
00050 * BREAK-Disable-Routine *
00060 *                       *
00070 **************************
00080 *
00090 *
00100 *
00110 POPMSK   .EQ $10
00120 IRQEN    .EQ $D20E
00130 *
00140 *
00150 *
00160 START    PLA         Keine Parameter
00170 *
00180          LDA POPMSK
00190          AND #$7F    Break IRQ
00200          STA POPMSK  sperren
00210          STA IRQEN
00220          RTS
```
