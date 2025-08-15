---
title: COM File Segment Dump
---
# COM File Segment Dump  
  
General Information  
  
Author: 	A. B. Langdon   
Language: 	ACTION!   
Compiler/Interpreter: 	ACTION!   
Published: 	9/84-4/28/85   
  
```
; LOaDPT 9/84-4/28/85, A. B. Langdon

; Read executable file to see where
; its segments load and its entry point(s) are.

SET $491=$4000 SET 14=$491^
BYTE rts=[$60] ;
;INCLUDE "D:SYSLIB.ACT"
;INCLUDE "D:SYSIO.ACT"

; Using channel 1, Close caused "system error" with DOS 2.1 but not DOS XL.
; ACS bbs has a block read (BLKIO.ACT) in machine code segments that is
; smaller and has a general purpose call to CIO. Here, I'll leave mine
; as it illustrates use of the language and is just as fast.

; First global ARRAY, other than BYTE ARRAY of length less than 257,
; is placed AFTER rest of program (undocumented?).
BYTE ARRAY buffer(257)	; locate the buffer.

CARD FLen, ; File length up to 64K
	  i, CSum
BYTE OpOK, CSum0=CSum, CSum1=CSum+1

BYTE CIO_status ; global for CIO return value (per ACS convention)

CARD FUNC GetAD(BYTE chan CARD addr, len) ; Block read
  TYPE IOCB=[BYTE hid,dno,com,sta
				 CARD badr,put,blen
				 BYTE aux1,aux2,aux3,aux4,aux5,aux6]
  IOCB POINTER ic
  BYTE chan16
  BYTE POINTER b
  chan16 = (chan&$07) LSH 4
  ic = $340+chan16
  ic.com = 7 ; read
  ic.blen = len
  ic.badr = addr
  [$AE chan16 $20 $E456 $8C CIO_status] ; LDX chan, JSR CIO; STY CIO_status
  IF CIO_status = $88 THEN EOF(chan)=1 FI
  FLen ==+ ic.blen  ; this to RETURN is special to this application.
  b = addr
  FOR i = 1 TO ic.blen DO
	 CSum0 ==+ b^
	 CSum1 ==+ CSum0
	 b ==+ 1
  OD
RETURN (ic.blen)

CARD FUNC GetCD(BYTE chan) ; Read a word
  CARD c
  GetAD(chan,@c,2)
RETURN (c)

PROC FixFlSp(BYTE ARRAY FileSpec)
  IF FileSpec(2)<>': AND FileSpec(3)<>': THEN ; prefix "D:" to file name
	 FileSpec^==+2
	 i=FileSpec^
	 WHILE i>2 DO
		FileSpec(i)=FileSpec(i-2)
		i==-1
	 OD
	 FileSpec(1)='D  FileSpec(2)=':
  FI
; Could also convert to upper case: if >$60 then subtract $20.
RETURN

PROC SysErr(BYTE errno)

PROC MyError(BYTE errno)
  IF errno=$80 THEN Error=SysErr Error(errno) FI
  PrintF("error %I. Try again%E",errno)
  OpOK=0
RETURN

PROC End=*() [$68$AA$68$CD$2E8$90$5$CD$2E6$90$F3 $48$8A$48$60]
; entry: PLA; TAX; PLA; CMP MEMLO+1; BCC lab; CMP MEMTOP+1; BCC entry;
; lab: PHA; TXA; PHA; RTS
; Trace back thru RTS's and return to cartridge or DOS.
; From ACS bulletin board.

PROC LoadPt()
  CHAR ARRAY FileSpec(20)
  BYTE b, SHFLOK=$2BE
  CARD fwa, lwa, BufLen, MEMTOP=$2E5, MEMLO=$2E7
  BufLen=MEMTOP-$80-buffer
  SysErr=Error
  DO
	 Print("File Spec=")
	 SHFLOK=$40 ; upper case
	 InputS(FileSpec)
	 IF FileSpec^=0 THEN END() FI
	 FixFlSp(FileSpec)
	 Close(2)
	 OpOK=1 Error=MyError Open(2,FileSpec,4,0)
  UNTIL OpOK OD
  Error=SysErr
  FLen=0 CSum0=0 CSum1=0

  i=GetCD(2)
  IF i<>$FFFF THEN ; is it a LOAD file?
	 PrintF("Bad load file header=%H%E",i)
	 Close(2)
	 RETURN
  FI

  DO; Code block
	 DO
		fwa=GetCD(2)
		IF fwa=0 THEN ; may get 0 before EOF in DOS 4.
		  FLen==-2  CSum1==-CSum0-CSum0 ; ignore these 2 bytes
		  EOF(2)=1
		FI
		IF EOF(2)<>0 THEN
		  PrintF("End of file. %H bytes%E",FLen)
		  PrintF(" checksum=%H%E",CSum)
		  Close(2)
		  RETURN
		FI
	 UNTIL fwa<>$FFFF OD; Skip embedded $FFFF
	 lwa=GetCD(2)
	 IF (fwa=$2E2 OR fwa=$2E0) AND lwa=fwa+1 THEN
		IF fwa=$2E0 THEN Print("INIT")
						ELSE Print("RUN") FI
		i=GetCD(2)
		fwa==+2
		PrintF(" at %H%E",i)
	 ELSE
		PrintF("fwa, lwa %H %H%E",fwa,lwa)
		IF fwa<MEMLO AND lwa>$700 THEN
		  PrintF("ACHTUNG! This loads into%Eyour DOS (MEMLO=%H)%E",MEMLO)
		FI
	 FI
	 WHILE lwa>=fwa DO ; just pass over these bytes
		i=lwa-fwa+1 IF i>BufLen THEN i=BufLen FI
		i=GetAD(2,buffer,i)
		fwa==+i
	 OD
  OD
  Close(2)
RETURN

PROC Main()
  device=0 ; in case MAC/65 has been here
  DO
	 LoadPt()
	 PrintE(" (RETURN to end)")
  OD
RETURN
```
