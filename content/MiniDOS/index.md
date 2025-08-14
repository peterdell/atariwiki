# MiniDOS  
  
```
; PROGRAM TO ACT AS SORT OF A MINI-DOS    VERSION 1.0
; DENNIS NEWTON    --  9/27/83

BYTE RTS=[$60],BANK=$D500

BYTE ARRAY FNAME(50) ; USED BY ALL ROUTINES

;*******************************************************************************

PROC GETFNAME(BYTE ARRAY PROMPT) ; GETS AND FORMATS FILE NAME INTO FNAME
  BYTE ARRAY FN1(25),FN2(25) ; LOCAL FILE NAMES FOR BUILDING FNAME
  
  
  PRINT(PROMPT) : INPUTS(FN1)
  IF FN1(0)=0 THEN ; NO NAME TYPED
    SCOPY(FNAME,"D:*.*") ; SUBSTITUTE DEFAULT
  ELSE
    IF FN1(2)#': AND FN1(3)#': THEN
      SCOPY(FN2,"D:")
      SASSIGN(FN2,FN1,3,25)
      SCOPY(FN1,FN2)
    FI
    SCOPY(FNAME,FN1)
  FI
  PUTE()
RETURN

;*******************************************************************************

PROC DIR()
  BYTE ARRAY BUFFER(40)
  
  GETFNAME("DIR: ")
  GRAPHICS(0)
  OPEN(3,FNAME,6,0)
  DO
    INPUTSD(3,BUFFER)
    PRINT(BUFFER): PRINT("   ")
  UNTIL EOF(3) : OD
  PUTE() 
RETURN

;*******************************************************************************

PROC CIO(BYTE CMD, BYTE ARRAY NAME)

  XIO(3,0,CMD,0,0,NAME)
RETURN


;******************************************************************************

PROC RENAME()
  
  GETFNAME("RENAME: ")
  CIO(32,FNAME)           
RETURN

;*******************************************************************************

PROC ERASE()
 
  BYTE ANS
  BYTE ARRAY FTEMP(25)
  
  GETFNAME("ERASE: ")
  SCOPY(FTEMP,FNAME)
  IF SCOMPARE(FTEMP,"D:*.*") = 0  THEN
    PRINT("˝ERASE ALL FILES?  ARE YOU SURE?")
    ANS=GETD(2) 
    IF ANS # 'Y THEN : RETURN  : FI
  FI
  CIO(33,FNAME)
RETURN

;*******************************************************************************

PROC PROTECT()
  
  GETFNAME("PROTECT: ")
  CIO(35,FNAME)          
RETURN

;*******************************************************************************

PROC UNPROTECT()
 
  GETFNAME("UNPROTECT: ")
  CIO(36,FNAME)
RETURN

;*******************************************************************************

PROC FORMAT()
 
  BYTE ANS
  
  PRINTE("FORMAT:  ˝ARE YOU SURE? ")
  ANS=GETD(2)                      
  IF ANS='Y THEN
    PRINT("INSERT CORRECT DISK AND PRESS ANY KEY")
    ANS=GETD(2) 
    CIO(254,"D:*.*")
  FI
RETURN

;*******************************************************************************

PROC TYPETEXT()
  
  BYTE CH,KBD=764,DEVICE

  CLOSE(4)
  GETFNAME("TYPE: ")
  PRINT("TO PRINTER ALSO (Y/N)? ") : DEVICE=GETD(2)   
  IF DEVICE='Y THEN   
    OPEN(4,"P:",8,0)
  FI
  GRAPHICS(0)
  OPEN(3,FNAME,4,0)
  DO
    CH=GETD(3)  
    IF DEVICE='Y THEN : PUTD(4,CH) : FI
    PUT(27) : PUT(CH)
    IF KBD # 255 THEN : KBD = 255 : EXIT : FI
  UNTIL EOF(3) : OD
  PUTE():CLOSE(4)
RETURN

;*******************************************************************************

PROC WAIT() ; WAIT FOR KEY PRESS
  BYTE DUMMY
    
  PUTE() : PRINTE("ANY KEY TO RETURN TO MENU")
  DUMMY=GETD(2)
RETURN
  
;*******************************************************************************

PROC MENU()

    GRAPHICS(1)
    CLOSE(3)
    PRINTDE(6,"ACTION! Mini Dos")     
    PRINTDE(6," ")
    PRINTDE(6,"CHOOSE ONE OF THE   FOLLOWING:")  : PRINTDE(6," ")
    PRINTDE(6,"  dIRECTORY")
    PRINTDE(6,"  rENAME")
    PRINTDE(6,"  eRASE")
    PRINTDE(6,"  pROTECT")
    PRINTDE(6,"  uNPROTECT")
    PRINTDE(6,"  fORMAT DISK")
    PRINTDE(6,"  tYPE TEXT FILE")  
    PRINTDE(6," ExIT TO ACTION!")
RETURN

;*******************************************************************************

PROC ADOS() ; MAIN CONTROL ROUTINE

  BYTE CHOICE,LMRGN=82
  
  BANK=0 : LMRGN=0 : CLOSE(2) :  OPEN(2,"K:",4,0)
  DO
    MENU()
    CHOICE=GETD(2)
  
    IF     CHOICE='D THEN : DIR() : WAIT()
    ELSEIF CHOICE='R THEN : RENAME()
    ELSEIF CHOICE='E THEN : ERASE()
    ELSEIF CHOICE='P THEN : PROTECT()
    ELSEIF CHOICE='U THEN : UNPROTECT()
    ELSEIF CHOICE='F THEN : FORMAT()
    ELSEIF CHOICE='T THEN : TYPETEXT() : WAIT()
    FI
    CLOSE(3)
           
  UNTIL CHOICE='X : OD
  GRAPHICS(0) : CLOSE(2)
RETURN


```
