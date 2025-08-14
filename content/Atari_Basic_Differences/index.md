# Differences between Basic Dialects  
# Vergleich der Verschiedenen Basic Dialekte:  
%%tabbedSection  
%%tab-English  
Even the name of the command is the same, the syntax used in different basic dialects is different. The table below shows the different commands available in the Basic dialects.  
/%  
%%tab-Deutsch  
Trotz gleichlautendem Befehl, kann die Syntax der einzelnen Dialekte abweichen!  
/%  
/%  
### Eigenschaften  
|                        || ATARI-Basic|| Turbo-Basic 1.5|| BASIC A+ || BASIC-XL || BASIC-XE|| MS-BASIC  
|__Year                __ | 1979        | 1985            | 1983      | 1984      | 1985     | 1981  
|__Size                __ | 8k          |                 | 16k       | 16k       | 27k      |  
|__Size in RAM         __ | 8k          |                 | 15k       | 8k        | 8k       |  
|__Compiler            __ |             | x               | -         | -         | -        | -  
|__Runtime             __ |             | x               | -         | x         | -        | -  
|__Unlimited Strings   __ | x           | x               |           |           |          |  
|__String Array        __ |             |                 |           |           | x        | x  
|__Number of Variables __ | 128         |                 |           |           | 128      |  
|__Parameter passing   __ | -           | -               |           |           | x        |  
|__Local variables     __ | -           | -               |           |           | x        |  
|__Lowercase characters__ | -           | x               | x         | x         | x        |  
|__Reverse characters  __ | -           | x               | x         | x         | x        |  
  
  
### Befehlsübersicht  
|| ATARI-Basic|| Turbo-Basic 1.5|| BASIC A+|| BASIC-XL|| BASIC-XE|| MS-BASIC  
| -| -| | | |  
| | !| | | |  
| | %GET| | | |  
| | %PUT| | | |  
| &| &| &| &| &| &  
| *| *| *| *| *| *  
| .| .| .| .| .| .  
| /| /| /| /| /| /  
| :| :| :| :| :| :  
| -| -| &| &| &| &  
| ^| ^| ^| ^| ^| ^  
| +| +| +| +| +| +  
| <| <| <| <| <| <  
| =| =| =| =| =| =  
| >| >| >| >| >| >  
| ABS| ABS| ABS| ABS| ABS| ABS  
| ADR| ADR| ADR| ADR| ADR|  
| | | | | | AFTER  
| AND| AND| AND| AND| AND| AND  
| ASC| ASC| ASC| ASC| ASC| ASC  
| ATN| ATN| ATN| ATN| ATN| ATN  
| | | | | | AUTO  
| | BGET| BGET| BGET| BGET|  
| | BLOAD| | | |  
| | BPUT| BPUT| BPUT| BPUT|  
| | BRUN| | | |  
| | | BUMP| BUMP| BUMP|  
| BYE| BYE| BYE| BYE| BYE|  
| CHR$| CHR$| CHR$| CHR$| CHR$| CHR$  
| | CIRCLE| | | |  
| | | | | | CLEAR  
| | | | | | CLEAR STACK  
| CLOAD| CLOAD| CLOAD| CLOAD| CLOAD| CLOAD  
| CLOG| CLOG| CLOG| CLOG| CLOG| CLOG  
| CLOSE| CLOSE| CLOSE| CLOSE| CLOSE| CLOSE  
| CLR| CLR| CLR| CLR| CLR|  
| | CLS| | | | CLS  
| COLOR| COLOR| COLOR| COLOR| COLOR| COLOR  
| COM| COM| COM| COM| COM|  
| | | | | | COMMON  
| CONT| CONT| CONT| CONT| CONT| CONT  
| COS| COS| COS| COS| COS| COS  
| | | CP| CP| CP|  
| CSAVE| CSAVE| CSAVE| CSAVE| CSAVE| CSAVE  
| DATA| DATA| DATA| DATA| DATA| DATA  
| | DEC| | | |  
| | | | | | DEF  
| | | | | | DEFDBL  
| | | | | | DEFINT  
| | | | | | DEFSGN  
| | | | | | DEFSTR  
| DEG| DEG| DEG| DEG| DEG| DEG  
| | DEL| DEL| DEL| DEL| DEL  
| | DELETE| | | |  
| DIM| DIM| DIM| DIM| DIM| DIM  
| | DIR| DIR| DIR| DIR|  
| | DIV| | | |  
| | DO| | | |  
| DOS| DOS| DOS| DOS| DOS| DOS  
| | DPEEK| DPEEK| DPEEK| DPEEK|  
| | DPOKE| DPOKE| DPOKE| DPOKE|  
| DRAWTO| DRAWTO| DRAWTO| DRAWTO| DRAWTO|  
| | DSOUND| | | |  
| | DUMP| | | |  
| | ELSE| ELSE| ELSE| ELSE| ELSE  
| END| END| END| END| END| END  
| | ENDIF| ENDIF| ENDIF| ENDIF|  
| | ENDPROC| | | |  
| | | ENDWHILE| ENDWHILE| ENDWHILE|  
| ENTER| ENTER| ENTER| ENTER| ENTER|  
| | | | | | EOF  
| | | ERASE| ERASE| ERASE|  
| | ERL| | | | ERL  
| | ERR| ERR| ERR| ERR| ERR  
| | | | | | ERROR  
| | EXEC| | | |  
| | EXIT| | | |  
| | EXOR| | | |  
| EXP| EXP| EXP| EXP| EXP| EXP  
| | | FAST| FAST| FAST|  
| | FCOLOR| | | |  
| | | | | | FILL  
| | FILLTO| | | |  
| | | FIND| FIND| FIND|  
| FOR| FOR| FOR| FOR| FOR| FOR  
| | FRAC| | | |  
| FRE| FRE| FRE| FRE| FRE| FRE  
| GET| GET| GET| GET| GET| GET  
| | GO#| | | |  
| GOSUB| GOSUB| GOSUB| GOSUB| GOSUB| GOSUB  
| GOTO| GOTO| GOTO| GOTO| GOTO| GOTO  
| GRAPHICS| GRAPHICS| GRAPHICS| GRAPHICS| GRAPHICS| GRAPHICS  
| | HEX$| HEX$| HEX$| HEX$|  
| | | HSTICK| HSTICK| HSTICK|  
| | | HITCLR| HITCLR| HITCLR|  
| IF| IF| IF| IF| IF| IF  
| | INKEY$| | | | INKEY$  
| INPUT| INPUT| INPUT| INPUT| INPUT| INPUT  
| | | | | | INPUT AT  
| | INSTR| | | | INSTR  
| INT| INT| INT| INT| INT| INT  
| | | | | | KILL  
| | | LEFT$| LEFT$| LEFT$| LEFT$  
| LEN| LEN| LEN| LEN| LEN| LEN  
| LET| LET| LET| LET| LET| LET  
| | | | | | LINE INPUT  
| | | | | | LINE INPUT AT  
| LIST| LIST| LIST| LIST| LIST| LIST  
| LOAD| LOAD| LOAD| LOAD| LOAD| LOAD  
| | | | | LOCAL|  
| LOCATE| LOCATE| LOCATE| LOCATE| LOCATE|  
| | LOCK| | | | LOCK  
| LOG| LOG| LOG| LOG| LOG| LOG  
| | | LOMEM| LOMEM| LOMEM|  
| | LOOP| | | |  
| LPRINT| LPRINT| LPRINT| LPRINT| LPRINT|  
| | | LVAR| LVAR| LVAR|  
| | | | | | MERGE  
| | | MID$| MID$| MID$| MID$  
| | | MISSILE| MISSILE| MISSILE|  
| | MOD| | | |  
| | MOVE| MOVE| MOVE| MOVE|  
| | | | | | NAME TO  
| NEW| NEW| NEW| NEW| NEW| NEW  
| NEXT| NEXT| NEXT| NEXT| NEXT| NEXT  
| NOT| NOT| NOT| NOT| NOT| NOT  
| NOTE| NOTE| NOTE| NOTE| NOTE| NOTE  
| | | NUM| NUM| NUM|  
| ON| ON| ON| ON| ON| ON  
| | | | | | ON ERROR GOTO  
| OPEN| OPEN| OPEN| OPEN| OPEN|  
| | | | | | OPTION  
| OR| OR| OR| OR| OR| OR  
| PADDLE| PADDLE| PADDLE| PADDLE| PADDLE| PADDLE  
| | PAINT| | | |  
| | PAUSE| | | |  
| PEEK| PEEK| PEEK| PEEK| PEEK| PEEK  
| | | PEN| PEN| PEN|  
| PLOT| PLOT| PLOT| PLOT| PLOT| PLOT  
| | | | | | PLOT TO  
| | | PMADR| PMADR| PMADR|  
| | | PMCLR| PMCLR| PMCLR|  
| | | PMCOLOR| PMCOLOR| PMCOLOR|  
| | | PMGRAPHICS| PMGRAPHICS| PMGRAPHICS|  
| | | PMMOVE| PMMOVE| PMMOVE|  
| | | PMWIDTH| PMWIDTH| PMWIDTH|  
| POINT| POINT| | | |  
| POKE| POKE| POKE| POKE| POKE| POKE  
| POP| POP| POP| POP| POP|  
| POSITION| POSITION| POSITION| POSITION| POSITION|  
| PRINT| PRINT| PRINT| PRINT| PRINT| PRINT  
| | | | | | PRINT AT  
| | | PRINT USING| PRINT USING| PRINT USING| PRINT USING  
| | PROC| | | |  
| | | | | PROCEDURE|  
| | | PROTECT| PROTECT| PROTECT|  
| PTRIG| PTRIG| PTRIG| PTRIG| PTRIG| PTRIG  
| PUT| PUT| PUT| PUT| PUT| PUT  
| RAD| RAD| RAD| RAD| RAD|  
| | RAND| | | |  
| | | RANDOM| RANDOM| RANDOM|  
| | | | | | RANDOMIZE  
| READ| READ| READ| READ| READ| READ  
| REM| REM| REM| REM| REM| REM  
| | RENAME| RENAME| RENAME| RENAME|  
| | RENUM| RENUM| RENUM| RENUM| RENUM  
| | REPEAT| | | |  
| RESTORE| RESTORE| RESTORE| RESTORE| RESTORE| RESTORE  
| | | | | | RESUME  
| RETURN| RETURN| RETURN| RETURN| RETURN| RETURN  
| | | RGET| RGET| RGET|  
| | | RIGHT$| RIGHT$| RIGHT$| RIGHT$  
| RND| RND| RND| RND| RND| RND  
| | | RPUT| RPUT| RPUT|  
| RUN| RUN| RUN| RUN| RUN| RUN  
| SAVE| SAVE| SAVE| SAVE| SAVE| SAVE  
| | | | | | SAVE LOCK  
| | | | | | SCRN$  
| | | SET| SET| SET|  
| SETCOLOR| SETCOLOR| SETCOLOR| SETCOLOR| SETCOLOR| SETCOLOR  
| SGN| SGN| SGN| SGN| SGN| SGN  
| SIN| SIN| SIN| SIN| SIN| SIN  
| | | | | SORT|  
| SOUND| SOUND| SOUND| SOUND| SOUND| SOUND  
| SQR| SQR| SQR| SQR| SQR| SQR  
| | | | | | STACK  
| STATUS| STATUS| STATUS| STATUS| STATUS| STATUS  
| STEP| STEP| STEP| STEP| STEP| STEP  
| STICK| STICK| STICK| STICK| STICK| STICK  
| STOP| STOP| STOP| STOP| STOP| STOP  
| STR$| STR$| STR$| STR$| STR$| STR$  
| STRIG| STRIG| STRIG| STRIG| STRIG| STRIG  
| | | | | | STRING$  
| | | SYS| SYS| SYS|  
| | | TAB| TAB| TAB|  
| TAN| TAN| TAN| TAN| TAN| TAN  
| | TEXT| | | |  
| THEN| THEN| THEN| THEN| THEN| THEN  
| | TIME| | | | TIME  
| | TIME$| | | | TIME$  
| TO| TO| TO| TO| TO| TO  
| | TRACE| TRACE| TRACE| TRACE|  
| | | TRACEOFF| TRACEOFF| TRACEOFF|  
| TRAP| TRAP| TRAP| TRAP| TRAP|  
| | | | | | TROFF  
| | | | | | TRON  
| | TRUNC| | | |  
| | UINSTR| | | |  
| | UNLOCK| | | | UNLOCK  
| | | UNPROTECT| UNPROTECT| UNPROTECT|  
| | UNTIL| | | |  
| USR| USR| USR| USR| USR| USR  
| VAL| VAL| VAL| VAL| VAL| VAL  
| | | | | | VARPTR  
| | | | | | VERIFY  
| | | VSTICK| VSTICK| VSTICK|  
| | | WAIT| WAIT| WAIT|  
| | WEND| | | |  
| | WHILE| WHILE| WHILE| WHILE|  
| XIO| XIO| XIO| XIO| XIO| XIO  
| | | | | XTEND|  
