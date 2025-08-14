# Butterfly Demo  
  
General Information  
  
Author: 	Michael Mitchell   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	01/20/85   
  
```
; butterfly  by michael mitchell
; 01/20/85
PROC DEMO2()
CARD A,B,C,D,X,Y,J,K,COL,I,Q
	Graphics(11)

  Poke(710,0)
  Color=00
  A=1 B=1 C=1 D=1
  X=Rand(70)+1
  Y=Rand(190)+1
  J=Rand(50)+1
  K=Rand(190)+1

  For I=1 TO 9400 
  DO
	 Plot(X,Y) 
	 Drawto(J,K)
	 Plot(J,Y) 
	 Drawto(X,K)
	 X==+A 
	 Y==+B 
	 J==+C 
	 K==+D 

	 Q=Rand(50)
	 IF Q>40 THEN  
		COL==+1  
	 FI  
	 IF COL>14 THEN 
		COL=1 
	 FI

	 COLOR=COL

	 IF X>=79 THEN A=-A X==+A  FI
	 IF J>=79 THEN C=-C J==+C FI
	 IF J<=0 THEN C=-C J==+C FI
	 IF X<=0 THEN A=-A X==+A FI
	 IF Y>=191 THEN B=-B Y==+B  FI
	 IF K>=191 THEN D=-D K==+D  FI
	 IF K<=0 THEN D=-D K==+D  FI
	 IF Y<=0 THEN B=-B Y==+B FI

  OD
RETURN
```
