# CX85 Keypad Interrrupt Handler  
  
original Atari source from the CX-85 Disk  
  
```
  ;DEMONSTRATION OF CX-85 KEYPAD INTERRUPT HANDLER                            
  ;FLORA P. NG   3/08/82                
  ;                                     
  ;This keypad interrupt handler detects and handles all                      
  ;keys pressed on a CX-85 keypad plugged into port 2.                        
  ;This is assembled using Atari Macro Assembler.                             
  ;                                     
  TIMER   EQU     $30                   
  TIMER1  EQU     6                     
  START   EQU     $9    ;START MASK     
  SELECT  EQU     $A    ;SELECT MASK    
  OPTION  EQU     $C    ;OPTION MASK    
  BPOT    EQU     $08   ;BPOT BIT MASK  
  VVBLKD  EQU     $224  ;VERTICAL BLANK INTERRUPT                             
  STRIG1  EQU     $285  ;TRIGGER 1      
  ATTRACT EQU     $4D   ;ATTRACT MODE FLAG                                    
  CH      EQU     $2FC  ;KEYBOARD CODE  
  ALLPOT  EQU     $D208 ;ALL POT STATUS 
  PORTA   EQU     $D300 ;PORTA          
  SETVBV  EQU     $E45C ;ROUTINE FOR SETTING VECTORS                          
  DOSINI  EQU     $0C   ;WARM START ADDR
                                        
  CONSOL  EQU     $D01F ;CONSOL SWITCH PORT                                   
  BREAK   EQU     $11   ;BREAK KEY FLAG 
  ;LOCATED IN PAGE 6 BUT MAY BE REASSEMBLED ELSEWHERE                         
  ;                                     
  ;INITIAL ENTRY POINT TO ESTABLISH VBLANK ENTRY                              
  ;SYSTEM RESET KEY RESETS VBLANK VECTORS,                                    
  ;HENCE CHAIN TO DOS INIT              
  ;SAVE VALUE IN DOSINI                 
          ORG     $600                  
  COLDST: LDA     DOSINI                
          STA     WRMEXT+1              
          LDA     DOSINI+1              
          STA     WRMEXT+2              
  ;REPLACE DOSINI WITH WARMST           
          LDA     #LOW WARMST           
          STA     DOSINI                
          LDA     #HIGH WARMST          
          STA     DOSINI+1              
  ;CHAIN KEYPAD INTO DEFERRED VBLANK PROCESSING                               
  ;SAVE VVBLKD FOR KEYPAD EXIT POINT    
  KPADVBI: LDA     VVBLKD               
          STA     EXIT+1                
          LDA     VVBLKD+1              
          STA     EXIT+2                
  ;                                     
  ;REPLACE VVBLKD WITH KEYPAD ENTRY POINT                                     
          LDY     #LOW KPAD             
          LDX     #HIGH KPAD            
          LDA     #7      ;DEFERRED VBI 
          JSR     SETVBV                
          RTS                           
  ;                                     
  ;ENTERED WHEN USER HITS SYSTEM RESET  
  ;REESTABLISH VBLANK VECTOR            
  WARMST: JSR     KPADVBI               
  WRMEXT: JMP     0       ;CHAIN TO DOSINI                                    
  ;                                     
  ;                                     
  ;KEYPAD TRANSLATION TABLE             
  ;                                     
  KPADTAB: DB     $0C,$0C  ;FUNCTION 1  
          DB      $14,$34  ;FUNCTION 2  
          DB      $10,$07  ;FUNCTION 3  
          DB      $18,$26  ;FUNCTION 4  
          DB      $1C,$32  ;0           
          DB      $19,$1F  ;1           
          DB      $1A,$1E  ;2           
          DB      $1B,$1A  ;3           
          DB      $11,$18  ;4           
          DB      $12,$1D  ;5           
          DB      $13,$1B  ;6           
          DB      $15,$33  ;7           
          DB      $16,$35  ;8           
          DB      $17,$30  ;9           
          DB      $1D,$22  ;.           
          DB      $1F,$0E  ;-           
          DB      $1E,$06  ;+ENTER      
          DB      0        ;END OF TABLE
                                        
  ;ENTERED AT EACH VBLANK TO READ THE KEYPAD                                  
  KPAD:   LDA     STRIG1  ;KEY PRESSED? 
          BNE     KPADDM  ;EXIT FOR KEY NOT PRESSED                           
          LDA     #0      ;RESET ATTRACT
   MODE                                 
          STA     ATTRACT               
  ;DETERMINE VALUE OF KEY PRESSED       
          LDA     PORTA   ;READ CABLE PIN OF PORT 2                           
          LSR     A                     
          LSR     A                     
          LSR     A                     
          LSR     A                     
          STA     TEMP                  
          LDA     ALLPOT  ;READ ALLPOT FOR 5TH CABLE PIN STATUS               
          AND     #BPOT   ;MASK FOR 5TH  PIN                                   
          EOR     #BPOT   ;COMPLEMENT BIT (O IS VALID)                        
          ASL     A                     
          ORA     TEMP    ;A HAS KEY VALUE                                    
          LDY     #0      ;INIT COUNTER 
  ;                                     
  ;SCAN TRANSLATION TABLE               
  KPADCK: CMP     KPADTAB,Y       ;MATCH KEYPAD TABLE ENTRY?                  
          BEQ     KPADMAT ;JUMP IF MATCH                                        
          INY             ;INC TO NEXT ENTRY                                  
          INY                           
          LDX     KPADTAB,Y       ;END OF TABLE?                              
          BEQ     EXIT    ;EXIT FOR END OF TABLE                              
          BNE     KPADCK                
  ;                                     
  ;KEY VALUE MATCHES                    
  ;PUT NEW KEYCODE IN CH AND RESET AUTO-REPEAT                                
  KPADMAT: TAX            ;SAVE KEY VALUE                                     
          INY             ;GET POKEY KEYCODE                                  
          LDA     KPADTAB,Y       ;A HAS KEYCODE                              
          CMP     #$FF    ;VECTOR ROUTINE?                                    
          BEQ     KPADFUN ;EXIT FOR VECTOR ROUTINE                            
          CMP     KPADCOD ;SAME AS PRIOR KEYCODE?                             
          BEQ     KPADSAM ;BRANCH IF SAME                                     
          STA     KPADCOD ;ELSE STORE NEW KEYCODE                             
          STA     CH                    
          LDA     #TIMER  ;RESET TIMER  
          STA     KPADREP               
          BNE     EXIT1                 
  ;                                     
  KPADDM: LDA     #$C0     ;LOAD DUMMY VARIABLE                               
          STA     KPADCOD               
  EXIT1:                                
  ************************************* 
          LDA     #1      ;RESET BRK PRESS FLAG                               
          STA     BRKPRS                
  ************************************* 
          BNE     EXIT                  
                                        
  ;SAME AS PRIOR KEY, CHECK AUTO-REPEAT 
  KPADSAM: LDX     KPADREP ;AUTO-REPEAT EXPIRED?                              
          DEX             ;DEC TIMER    
          BNE     KPADXX  ;BRANCH IF NOT                                        
          STA     CH      ;STORE KEYCODE                                        
          LDA     #TIMER1 ;RESET TIMER  
          STA     KPADREP               
          BNE     EXIT1                 
  KPADXX: STX     KPADREP               
  ;                                     
  ;EXIT THIS VBLANK INTERRUPT           
  EXIT:   JMP      0       ;CHAIN TO DEFERRED VBLANK                          
  TEMP:   DB       0   ;TEMP VARIABLE   
  KPADCOD: DB      0   ;PRIOR KEYCODE   
  KPADREP: DB      $30 ;AUTO-REPEAT TIMER                                     
  ;                                     
  ;IF NO $FF IN TRANSLATION TABLE, THE SeCTIONS                               
  ;ENCLOSED WITHIN *** MAY BE DELETED   
  ************************************* 
  BRKPRS: DB       1   ;BREAK PRESS FLAG                                        
  ;                                     
  ;FUNCTION VECTOR TABLE                
  KPADFTB: DW     KPADF1   ;F1 VECTOR   
          DW      KPADF2   ;F2 VECTOR   
          DW      KPADF3   ;F3 VECTOR   
          DW      KPADF4   ;F4 VECTOR   
  ;GET FUNCTION VECTOR                  
  KPADFUN: DEY                          
          LDA     KPADFTB,Y             
          STA     KPADFV+1              
          INY                           
          LDA     KPADFTB,Y             
          STA     KPADFV+2              
  ;CALL TO FUNCTION VECTOR              
  KPADFV: JSR     0       ;CALL TO FUNCTION                                   
          JMP     EXIT                  
  KPADF1: LDA     BRKPRS                
          BEQ     KPADFR                
          LDA     #0      ;BREAK PRESSED                                        
          STA     BREAK                 
          STA     BRKPRS                
          LDA     #$C0    ;LOAD DUMMY KEYCODE                                 
          STA     KPADCOD               
  KPADFR: RTS                           
  KPADF2: LDA     #OPTION               
          STA     CONSOL                
          RTS                           
  KPADF3: LDA     #SELECT               
          STA     CONSOL                
          RTS                           
  KPADF4: LDA     #START                
          STA     CONSOL                
          RTS                           
  **************************************
                                        
          END     COLDST                
```
