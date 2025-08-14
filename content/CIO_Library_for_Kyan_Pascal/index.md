# CIO Library for Kyan Pascal  
  
CIO EQUATES FILE  
  
While you program with your Atari, you will frequently use  
input and output operations, and you will invariably use CIO  
to do these operations (except for specialized operations, in  
which case you may use something like SIO).  CIO has many  
labels associated with it such as ICCMD and ICAX1, which you  
will use often.  But if you EQUate these labels in different  
routines, the Kyan Macro Assembler (AS) will hand you a  
'multiply defined label' error, so you must equate these  
labels globally (which means right after your global VARiable  
declarations).  
  
I have created an include file, CIOEqu.i, to make these  
global equates, which may then be used by assembly language  
routines throughout your program.  It is not an all-  
encompassing file--that is, it does not contain equates for  
every CIO label and command number, just most of the more  
commonly encountered ones.  You may, of course, add missing  
labels and commands to this file.  
  
This file should generally be the first one that you include  
after your global VARiable declarations, since its labels may  
be used by other included routines.  The function GetCha is a  
routine that makes use of CIOEqu.i.  It is available in this  
data library under the filenames GETCHR.DOC and GETCHR.PAS.  
  
(CIOEQU.PAS should be renamed to CIOEQU.I after you download  
it.)  
  
  
## CIOEQU.I  
  
```
#A
;_________CIO equates file__________
;
;-->cio labels:
ICCMD EQU $0342 ;command byte
ICCOM EQU $0342 ;cover both bases
ICSTA EQU $0343 ;status
ICBAL EQU $0344 ;LSB for buffer
ICBAH EQU $0345 ;MSB  "    "
ICBLL EQU $0348 ;buffer length LSB
ICBLH EQU $0349 ;  "      "    MSB
ICAX1 EQU $034A ;auxillary byte one
ICAX2 EQU $034B ;    "      "   two
CIOV  EQU $E456 ;The big vector!
;
;-->iocb numbers: 
iocb0 EQU $00
iocb1 EQU $10
iocb2 EQU $20
iocb3 EQU $30
iocb4 EQU $40
iocb5 EQU $50
iocb6 EQU $60
iocb7 EQU $70
;
;-->cio commands:
open EQU $03
getrec EQU $05
getch EQU $07
putrec EQU $09
putch EQU $0B
close EQU $0C
status EQU $0
;
;-->fms commands
rename EQU $20
delete EQU $21
protect EQU $23
unprotect EQU $24
point EQU $25
note EQU $26
format EQU $FE
;
;-->S: display commands
draw EQU $11
fill EQU $12
;
;-->aux commands
read EQU 4
conread EQU 5
readdir EQU 6
write EQU 8
append EQU 9
update EQU 12
conrw EQU 13
;
;This is not an 'Omni-File'...Only the
;more commonly used CIO things are
;included.  You may add to it without
;any problems.
#
```
  
## CIOLIB .PAS  
  
```
(*             CIOLib.i
               ________
       (C) 1986  Erik C. Warren
    Routines to access CIO calls.
Last Updated:  30 July, 1986
  These routines are in the public
domain and may not be sold, except for
the price of the software media, with-
out the expressed, written permission
of the author.                       *)

FUNCTION Close(IOCB_Num: Integer): Integer;
BEGIN
 Close:= 1;
 IOCB_Num:= IOCB_Num * 16;
#A
  stx _t
  ldy #7
  lda (_sp),y  ;IOCB
  tax
  lda #12      ;close command
  sta $342,x
  jsr $e456    ;ciov
  tya          ;same as icsta
  ldy #5
  sta (_sp),y  ;store in Close
  ldx _t
#
END;(* Close *)

FUNCTION Open(IOCB_Num,Ax1,Ax2: Integer;               VAR Dev: Device_String)
             : Integer;
BEGIN
 Open:= 1;
 IOCB_Num:= IOCB_Num * 16;
(*  stack: opn  num  ax1  ax2  dev  
            5    13   11   9    7    *)
#A
 stx _t
 ldy #13
 lda (_sp),y  ;IOCB
 tax
 lda #3       ;open command
 sta $342,x
 dey 
 dey          ;11
 lda (_sp),y  ;icax1
 sta $34a,x
 dey
 dey          ;9
 lda (_sp),y  ;icax2
 sta $34b,x
 dey          ;8
 lda (_sp),y  ;dev MSB
 sta $345,x   ;icbah
 dey          ;7
 lda (_sp),y  ;icbal
 sta $344,x
 jsr $e456    ;ciov
 tya          ;same as icsta
 ldy #5
 sta (_sp),y  ;store in Open
 ldx _t
#
END;(* Open *)

FUNCTION Get_Byte(IOCB_Num: Integer;
                    VAR GB: Integer)
                 : Integer;
VAR TB: Integer;
BEGIN
 TB:= 0;
 Get_Byte:= 1;
 GB:= 0;
 IOCB_Num:= IOCB_Num * 16;
(*  stack: get  num   gb   tb
           7/8 11/12 9/10 5/6      *)
#A
 stx _t
 ldy #11
 lda (_sp),y  ;IOCB
 tax
 lda #7       ;get char command
 sta $342,x
 lda #$00     ;zero out the unused
 sta $348,x   ;store in accumulator
 sta $349,x   ;...after CIOV jump
 jsr $e456
 sty _t+1     ;hold temporarily
 ldy #5
 sta (_sp),y  ;put byte in GB
 lda _t+1     ;get status back
 ldy #7
 sta (_sp),y  ;store in Get_Byte
 ldx _t
#
GB:= TB
END;(* Get_Byte *)

FUNCTION Put_Byte(IOCB_Num: Integer;
                        PB: Integer)
                 : Integer;
BEGIN
 Put_Byte:= 1;
 IOCB_Num:= IOCB_Num * 16;
(*  stack: put  num   pb
            5    9    7            *)
#A
 stx _t
 ldy #9
 lda (_sp),y  ;IOCB
 tax
 lda #11      ;put char command
 sta $342,x
 lda #$00     ;zero out the unused
 sta $348,x   ;put from accumulator
 sta $349,x
 ldy #7
 lda (_sp),y  ;put PB in accumulator
 jsr $e456
 tya          ;same as icsta
 ldy #5
 sta (_sp),y  ;store in Put_Byte
 ldx _t
#
END;(* Put_Byte *)
```
  
