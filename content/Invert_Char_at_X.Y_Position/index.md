  
  
# Invert Char at X/Y Position  
  
contributed by Michael P./WASEO/ABBUC 27.06.2007  
  
```
(* Invert l chars at x,y, PD, Author:Michael P./WASEO/ABBUC 27.06.2007 *) 
(* max 255 chars, needs the PEEK function from the Kyan lib/docu *) 
Procedure InvertXY(x,y,l:Integer); 
var adrinv:integer; 
begin 
  adrinv:= peek(88)+peek(89)*256+(y*40)+x; 
#A 
  LDY #5 ;OFFSET ADRINV:L 
  LDA (_SP),Y 
  STA _T 
  LDY #6 ;OFFSET ADRIV:H 
  LDA (_SP),Y 
  STA _T+1 
  LDY #7 ;OFFSET LENGTH:L 
  LDA (_SP),Y 
  STA _T+2; ;Length TO _T+2 
  LDY #0 
L1 LDA (_T),Y ;LOAD CHAR TO ACCU 
  EOR #128 ;INVERT CHAR 
  STA (_T),Y ;STORE CHAR BACK 
  INY ;Increase Counter 
  CPY _T+2 ;Length reached? 
  BNE L1 ;NO: Back to L1 
# 
end;
   

```
  
