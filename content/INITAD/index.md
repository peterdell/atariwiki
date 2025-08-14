||ADR||HEXADR||NAME||OS  
|738,739|$02E2,$02E3|INITAD|both  
  
Initialization address read from the disk. An autoboot file must load an address value into either RUNAD above or INITAD. The code pointed to by INITAD will be run as soon as that location is loaded. The code pointed to by RUNAD will be executed only after the entire load process has been completed. To return control to DOS after the execution of your program, end your code with an RTS instruction.  
  
see also: [RUNAD](../RUNAD/index.md)  
