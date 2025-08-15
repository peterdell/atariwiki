---
title: SEROUT
---
||Read/Write||ADR||HEXADR||NAME||Description||OS  
|Read|53773|$D20D|SERIN|Serial Port Data Output|all  
|Write|53773|$D20D|SEROUT|Serial Port Data Input|all  
  
  
# Write  
Serial port data output. Usually written to in the event of a serial data out interrupt. Writes to the eight (one byte) parallel holding register that is transferred to the serial shift register when a full byte of data has been transmitted. This "holding" register is used to contain the bits to be transmitted one at a time (serially) as a one-byte unit before transmission.  
  
# Read  
Serial port input. Reads the one-byte parallel holding register that is loaded when a full byte of serial input data has been received. As above, this holding register is used to hold the bits as they are received one bit at a time until a full byte is received. This byte is then taken by the computer for processing. Also used to verify the checksum value at location 49 ($31).  
The serial bus is the port on the Atari into which you plug your cassette or disk cable. For the pin values of this port, see the OS User's Manual, p. 133, and the Hardware Manual.  
  
---
See also:  
  
previous: [POTGO](../POTGO/index.md)  
  
next: [IRQEN](../IRQEN/index.md),[IRQST](../IRQEN/index.md)  
