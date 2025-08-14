# ACTION OBJECT CODE RELOCATION PROGRAM: Copyright © 1984  OSS, Inc.  
The program was distributed in the golden age via BBS only. It was not sold to the public. Therefore we thank Alfred from AtariAge so much for saving it to us. Alfred, we are all deep in your debt. Thank you so much. :-)  
  
The program SIMPLREL.ACT on this BBS may be used to cause an ACTION! program to load and run at a different address than that address at which it was compiled. The same program will also work for assembly language object files, providing you also follow the given instructions. The program takes two object files as input and produces a third file which will load and run at a desired address. The relocating program prompts the user for the two input files, which must have been compiled one page (256 bytes) apart. It then prompts for an output file name (the relocated file), the page number of the starting address of the first file, and the page number of the desired destination address. Both page numbers must be decimal values. For example, specifying 32 as the destination page will cause the output file to load at address 32*256 ($2000), not $3200. See part V, "The ACTION! Compiler", chapter 2, page 144, for information on compiling programs to a specified address (Used to compile the two object files one page apart). In order to use the relocating program, download SIMPLREL.ACT and read the instructions therein.  
## SIMPLREL.ACT  
```
; Copyright © 1984  OSS, Inc.

; Permission is granted to change, duplicate, or distribute this program
; free of charge, provided:
;   1.  This copyright message is retained intact.
;   2.  The program is not sold for profit.

DEFINE File1   = "1",
       File2   = "2",
       OutFile = "3"

PROC Relocate()
    BYTE ARRAY name1( 20 ),
               name2( 20 ),
               outName( 20 )
    BYTE destPage, c1, c2, basePage

    ; Ask user for file names,
    Print( "File 1: " )
    InputS( name1 )
    Print( "File 2: " )
    InputS( name2 )
    Print( "Relocated file: " )
    InputS( outName )

    ; address of first file,
    Print( "Page of file 1 (decimal):   " )
    basePage = InputB()

    ; and destination address (page number)
    Print( "Destination page (decimal): " )
    destPage = InputB()
    Print( "Relocating to page " )
    PrintBE( destPage )

    ; Open the files
    Close( File1 )
    Open( File1, name1, 4, 0 )
    Close( File2 )
    Open( File2, name2, 4, 0 )
    Close( OutFile )
    Open( OutFile, outName, 8, 0 )

    ; And perform the relocation
    DO
        ; Get one byte from each file
        c1 = GetD( File1 )
        c2 = GetD( File2 )

        ; Check for end of file
        IF Eof( File1 ) THEN
            EXIT
        FI

        ; If bytes differ, then relocate
        IF c1 = c2 THEN
            PutD( OutFile, c1 )
        ELSEIF (c2-c1 = 1) OR (c1-c2 = 1)
            ; Bytes differ by exactly one page - relocate.
            PutD( OutFile, c1-basePage+destPage )
        ELSE
            ; Bytes differ by more than one page - error!
            PrintE( "Object files are not 1 page apart!" )
            PrintE( "Aborting program..." )
            EXIT
        FI
    OD

    Close( File1 )
    Close( File2 )
    Close( OutFile )
RETURN

```
