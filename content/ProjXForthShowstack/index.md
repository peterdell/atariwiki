---
title: ProjXForthShowstack
---
  
# Showstack  
  
## Displaying Stack Contents  
The contents of the stack are normally invisible. However, properly visualizing  
the current stack contents is important for achieving the desired result. To  
show the stack contents with every  {{{ok}}} prompt, type: {{{showstack}}}  
  
```
ok
showstack
44 7 ok
8
47 7 8 ok
noshowstack
ok
```
  
The topmost stack item is always shown as the last item in the list, immediately before the  
"ok" prompt. In the above example, the topmost stack  
item is 8.  
  
  
__showstack__ ( -- )  
  
Prints the content of the stack preceding the "ok" prompt.  
  
__noshowstack__ ( -- )  
  
Stops printing of the stack content  
  
## Source Code  
  
```
( showstack )

BASE @ ( save base )
HEX

: .SOK .S ." ok" R> 3 + >R ;

2F7B CONSTANT OKPROMPT ( <-- implementation dependent! )
OKPROMPT @ CONSTANT ORGOK
' .SOK CFA CONSTANT NEWOK

: SHOWSTACK NEWOK OKPROMPT ! ;
: NOSHOWSTACK ORGOK OKPROMPT ! ;

BASE ! ( restore base )
." SHOWSTACK loaded..."
  

```
  
