||ADR||HEXADR||NAME||Description||OS  
|548,549|$0224,$0225|VVBLKD|Vertical Blank Deferred Register|both  
  
VBLANK deferred register; system return from interrupt, initialized to 59710 ($E93E, in the new OS "B" ROMs; 59653; $E905), the exit for the VBLANK routine. NMI.  
  
These two VBLANK vectors point to interrupt routines that occur at the beginning of the VBLANK time interval. The stage one VBLANK routine is executed; then location [CRITIC](../CRITIC/index.md) 66/$42 is tested for the time-critical nature of the interrupt and, if a critical code section has been interrupted, the stage two VBLANK routine is not executed with a JMP made through the immediate vector [VVBLKI](../VVBLKI/index.md). If not critical, the deferred interrupt VVBLKD is used. Normally the VBLANK interrupt bits are enabled (BIT 6 at location [NMIEN](../NMIEN/index.md) 54286/$D40E is set to one). To disable them, clear BIT 6 (set to zero).  
  
The normal seguence for VBLANK interrupt events is: after the OS test, JMP to the user immediate VBLANK interrupt routine through the vector [VVBLKI](../VVBLKI/index.md) at 546,547, then through [SYSVBV](../SYSVBV/index.md) at 58463/$E45F. This is directed by the OS through the VBLANK interrupt service routine at 59345/$E7D1 and then on to the user-deferred VBLANK interrupt routine vectored at 548,549. it then exits the VBLANK interrupt routine through [XITVBV](../XITVBV/index.md) 58466/$E462 and an RTI instruction.  
  
If you are changing the VBLANK vectors during the interrupt routine, use the [SETVBV](../SETVBV/index.md) routine at 58460/$E45C. An immediate VBI has about 3.800 machine cycles of time to use, a deferred VBI has about 20.000 cycles. Since many of these cycles are executed while the electron beam is being drawn, it is suggested that you do not execute graphics routines in deferred VBI's.  
  
If you create your own VBI's, terminate an immediate VBI with a JMP to [SYSVBV](../SYSVBV/index.md) 58463/$E45F and a deferred VBI with a JMP to [XITVBV](../XITVBV/index.md) 58466/$E462. To bypass the OS VBI routine [SYSVBL](../SYSVBL/index.md) at 59345/$E7D1 entirely, terminate your immediate VBI with a JMP to [XITVBV](../XITVBV/index.md) 58466/$E462.  
  
see also: [VDSLST](../VDSLST/index.md), [VVBLKI](../VVBLKI/index.md), [SYSVBV](../SYSVBV/index.md), [Interrupt](../Interrupt/index.md)  
