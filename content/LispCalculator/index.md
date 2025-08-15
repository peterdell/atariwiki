---
title: LispCalculator
---
# A simple Calculator in LISP  
  
General Information  
  
Author: 	Datasoft   
Language: 	LISP   
Compiler/Interpreter: 	InterLisp/65   
  
```
(CALC PUSH POP BINARY UNARY - E N L S D P)
(DEFINEQ CALC '(LAMBDA NIL (PROG (X Y OP STACK) LOOP (POKE 128 0) (TERPRI) (PRINT STACK) (TERPRI) (PRIN1 (QUOTE "Enter> ")) (SETQ IN (READ)) (COND ((# IN) (PUSH IN)) ((MEMBER IN BINARY) (PUSH (APPLY* IN (POP) (POP)))) ((MEMBER IN UNARY) (PUSH (APPLY* IN (POP)))) ((EQ IN (QUOTE Q)) (RETURN)) (T (PRIN1 (QUOTE "}")))) (GO LOOP)))
)
(DEFINEQ PUSH '(LAMBDA (ITEM) (SETQ STACK (CONS ITEM STACK)))
)
(DEFINEQ POP '(LAMBDA NIL (PROG (X) (SETQ X (CAR STACK)) (SETQ STACK (CDR STACK)) X))
)
(SETQ BINARY '(+ * - / P)
)
(SETQ UNARY '(E L N D S)
)
(DEFINEQ - '(LAMBDA (X Y) (SUB X Y))
)
(DEFINEQ E '(LAMBDA (X) (EXP X))
)
(DEFINEQ N '(LAMBDA (X) (SUB 0 X))
)
(DEFINEQ L '(LAMBDA (X) (LOG X))
)
(DEFINEQ S '(LAMBDA (X) (EXP (/ (LOG X) 2)))
)
(DEFINEQ D '(LAMBDA (X) (PROGN (PUSH X) X))
)
(DEFINEQ P '(LAMBDA (X Y) (EXP (* Y (LOG X))))
)
NIL
```
