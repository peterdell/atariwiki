# Cycle neutral branching  
  
General Information  
  
Author: Michael J. Mahon   
Assembler: generic   
  
From Michael J. Mahon:  
  
I've found it useful to devise macros to do certain conditional  
operations in constant time. For example, "increment Y if carry set"  
(with A volatile) is:  
```
BCS *+3	  ; Branch to INY
LDA $C8	  ; $C8 = INY
```
  
If Carry is set, the branch takes 3 cycles and the INY 2. If Carry is  
clear, the branch takes 2 cycles and the LDA 3. So this CINY macro  
always takes 5 cycles.  
