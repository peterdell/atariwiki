# Print Inline Strings  
  
General Information  
  
Author: Holger Picker pickerh@uni-muenster.de   
Published: comp.sys.apple2.programmer   
  
```
;****************************************
; 24-Jul-2000        StringWritePC
;
;        PC        = pointer to string
; ==>        A,X,Y        = saved
;
;****************************************

stringwritepc:        
                STA        strpc5+1;        save A
                PLA
                STA        strpc2+1;        pull return address
                PLA
                STA        strpc2+2
                BNE        strpc3;                jump always (should not be zero)

strpc2:                
                LDA        $ffff;                read characters from string
                BEQ        strpc4;                endmarker reached?
                JSR        cout;                print character
strpc3:                
                INC        strpc2+1;        increment address
                BNE        strpc2
                INC        strpc2+2
                BNE        strpc2;                jump always (should not become zero)

strpc4:                
                LDA        strpc2+2;        push address on stack
                PHA
                LDA        strpc2+1
                PHA
strpc5:
                LDA        #0;                restore A
                RTS
```
