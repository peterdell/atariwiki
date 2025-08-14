  
  
# HEAD Tool Sourcecode  
  
```
PROGRAM Head;
(*
  by Erik C. Warren, 14 January, 1987
  for UPDATE...KYAN's Jan./Feb. issue
*)
 TYPE
     PathString = ARRAY~[1..15] OF Char;
  VAR
        fn : PathString;
     nl,lr : Integer;
       inf : Text;
BEGIN
  Write('head file : ');
    ReadLn(fn);
  Write('# of lines: ');
    ReadLn(nl);
  Reset(inf,fn);
  Write(inf^);
  FOR lr := 2 TO nl DO
  BEGIN
    Get(inf);
    Write(inf^);
    WHILE NOT EOLn(inf) DO
    BEGIN
      Get(inf);
      Write(inf^)
    END; (* WHILE inf *)
    WriteLn
  END; (* FOR lr *)
  WriteLn;
  WriteLn(nl,' lines typed from ',fn)
END. (* PROGRAM *)
```
  
