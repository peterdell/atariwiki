  
  
# Access Sparta DOS Command Line Parameters  
  
```
;sdos.act
;bill aycock, 9/89
;support for sparta parameter passing
;also: see the SDCS manual pp.108-111


module


;--------------------------------------
;dummy routine for crunching args
;set to correct address in _setup()
;this routine gets one parameter from
; the cmd line and inserts a drive
; spec ("Dn:") in front
;returns the parameter in comfname
;

proc _zcr()


;--------------------------------------
;setup routine
;returns zero if sparta not installed
;else returns 1 and sets up _zcr() addr
;

byte func _setup()
 byte sparta=$700
 card dosvec=10

 if sparta#'S then return(0) fi
 _zcr=dosvec+3

return(1)


;--------------------------------------
;find command line length
;returns length of command line
;

byte func _cmdlen()
 card dosvec=10
 byte pointer _cmdline
 byte i

 _cmdline=dosvec+63
 for i=0 to 63 do
   if _cmdline^=155 then exit fi
   _cmdline==+1
 od
return(i)


;--------------------------------------
;get entire command line
;pass addr of a 65-byte-long string
;returns entire cmd line in the string
;

proc _getcmds(byte array cmds)
 card dosvec=10
 byte pointer _cmdline
 byte i,j

 _cmdline=dosvec+63
 i=_cmdlen()
 cmds^=i
 for j=1 to i do
   cmds(j)=_cmdline^
   _cmdline==+1
 od
return


;--------------------------------------
;find how many parameters on cmd line
;returns number of parameters...
;
;     INCLUDING PROGRAM NAME!
;

byte func _howmany()
 card dosvec=10
 byte pointer _argbuf
 byte pointer _bufoff
 byte i,j

 _argbuf=dosvec+33
 _bufoff=dosvec+10

 _bufoff^=0
 i=_cmdlen()
 j=0
 while _bufoff^ < i do
   _zcr()
   j==+1
 od
return(j)


;--------------------------------------
;get default drive number
;returns ASCII VALUE of default drive
;

byte func _ddrive()
 card dosvec=10
 byte pointer _argbuf2
 byte pointer _bufoff
 byte i

 _argbuf2=dosvec+34 ;2nd char of buffer
 _bufoff=dosvec+10

 _bufoff^=0
 for i=1 to _howmany() do ;skip _all_!
   _zcr()
 od
 _zcr()
return(_argbuf2^)


;--------------------------------------
;get a specific parameter
;pass param number to get, and
;  addr of a 29-byte-long string
;returns desired param in the string
;NOTE: param #0 is program name!
;

proc _getparm(byte which
              byte array parm)
 card dosvec=10
 byte pointer _argbuf
 byte pointer _bufoff
 byte i

 parm^=0
 if which>(_howmany()-1) then return fi

 _argbuf=dosvec+33
 _bufoff=dosvec+10

 _bufoff^=0
 for i=1 to which do ;skip to desired
   _zcr()            ;  parameter
 od

 _zcr()
 for i=1 to 28 do
   if _argbuf^=155 then exit fi
   parm(i)=_argbuf^
   _argbuf==+1
 od
 parm^=i-1
return


;--------------------------------------
;demo routine
;this demonstrates the above routines
;
;NOTE: you MUST call _setup() and get
;  a positive result before calling
;  any of the other routines here...
;  otherwise, it's crash city!
;

proc demo()

 byte array parameter(29)
 byte array command(65)
 byte i,j

 pute()
 if _setup()=0 then
   printe("SpartaDOS not installed!")
   return
 fi

 i=_cmdlen()
 printf("command line is %B chars long%E%E",i)

 _getcmds(command)
 printe("command line:")
 printe(command)
 pute()

 i=_ddrive()
 printf("default drive is D%C:%E%E",i)

 i=_howmany()
 printf("%B parameters were passed%E",i)
 printf("(including parameter #0!)%E%E")

 printe("parameter number, value:")
 for j=0 to i-1 do
   _getparm(j,parameter)
   printf(" %B  %S%E",j,parameter)
 od

return

;---- end of sdos.act -----------------
```
  
