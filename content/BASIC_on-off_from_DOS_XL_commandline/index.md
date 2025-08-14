  
  
# BASIC on / off from DOS XL commandline  
  
for DOS XL and OS/A+, may also work on SpartaDos and other Commandline DOS Versions  
  
```
00010 ;SAVE"D:BASIC.SYN
00020          .LI OFF
00030 ; This program checks the OS/A+
00040 ; command input buffer, and
00050 ; then either removes or
00060 ; installs the BASIC rom on
00070 ; XL series computers.  It
00080 ; does this by setting BASICF
00090 ; then executing a warmstart,
00100 ; to reset the OS variables for
00110 ; the correct RAM size.
00120 ;
00130 ; TYPE:
00140 ;       BASIC I for BASIC in.
00150 ;       BASIC O for BASIC out.
00160 ;
00170 ******************************
00180 *  Daniel L. Moore 03/17/84  *
00190 ******************************
00200 ;
00210 BOOT     .EQ $9
00220 DOSVEC   .EQ $A
00230 DOSINI   .EQ $C
00240 ;
00250 LOADFLG  .EQ $CA rev A,B BASIC
00260 ;
00270 VECTMP   .EQ $D4  FP register 0
00280 INITMP   .EQ $D6
00290 ;
00300 BASICF   .EQ $3F8
00310 ;
00320 DOSINIT  .EQ $7E0 for FMS v.2
00330 ; OS/A+ equates.
00340 CPBUFP   .EQ $A   next char.
00350 CPCMDB   .EQ $3F  command buff.
00360 ;
00370          .OR $4000
00380 ;
00390 ; Test for XL series computer
00400 START    LDA $FCD8
00410          CMP #$A2
00420          BEQ DOS
00430 ; Save run vector
00440          LDA DOSVEC
00450          STA VECTMP
00460          LDA DOSVEC+1
00470          STA VECTMP+1
00480 ; Save init vector.
00490          LDA DOSINI
00500          STA INITMP
00510          LDA DOSINI+1
00520          STA INITMP+1
00530 ; Check the command input
00540 ; buffer for an 'I or 'O.
00550          LDX #1 assume OUT
00560          LDY #CPBUFP
00570          LDA (DOSVEC),Y
00580          CLC
00590          ADC #CPCMDB+1
00600          TAY
00610          LDA (DOSVEC),Y
00620          CMP #'O       out?
00630          BEQ SET.IT
00640          DEX
00650          CMP #'I       in?
00660          BEQ SET.IT
00670 ; Not 'I or 'O, exit to CP/A.
00680          RTS
00690 ; Set BASIC in/out.
00700 SET.IT   STX BASICF
00710          LDA #$32  clear cmnd
00720          STA (DOSVEC),Y
00730 ; Set init/run vector to
00740 ; continuation code.
00750          LDA #CONT
00760          STA DOSVEC
00770          STA DOSINI
00780          LDA /CONT
00790          STA DOSVEC+1
00800          STA DOSINI+1
00810 ; Set BOOT to succesfull disk
00820 ; boot so SynAssembler will not
00830 ; attempt to run.
00840          LDA #01
00850          STA BOOT
00860 ; Let the OS switch BASIC,
00870 ; reset the memory size, and
00880 ; open E: at the new RAMTOP.
00890          JMP $E474   Warmstart
00900 ;
00910 ; Restore init/run vectors.
00920 CONT     LDA VECTMP
00930          STA DOSVEC
00940          LDA VECTMP+1
00950          STA DOSVEC+1
00960          LDA INITMP
00970          STA DOSINI
00980          LDA INITMP+1
00990          STA DOSINI+1
01000 ; Init DOS ($7E0 for FMS.)
01010 ; If you are running OS/A+ v.4
01020 ; add DOSINIT JMP (DOSINI)
01030 ; after the label DOS, and
01040 ; delete the DOSINIT equate
01050 ; above.
01060          JSR DOSINIT
01070 ; If BASIC IN, then set BASIC
01080 ; 'load in progress' flag, so
01090 ; all BASIC work areas will be
01100 ; cleared.  (force a NEW)
01110          LDA BASICF
01120          BNE DOS
01130          LDA #$FF
01140          STA LOADFLG
01150 ; Return to DOS.
01160 DOS      JMP (DOSVEC)
01170 ;
01180 ;
01190 END      .LI ON

```
  
