||ADR||HEXADR||NAME||Description||OS  
|66|$0042|CRITIC|Critical I/O Flag|both  
  
Critical I/O region flag; defines the current operation as a time- critical section when the value here is non-zero. Checked at the NMI process after the stage one VBLANK has been processed.  
  
POKEing any number other than zero here will disable the repeat action of the keys and change the sound of the CTRL-2 buzzer.  
Zero is normal; setting [CRITIC](../CRITIC/index.md) to a non-zero value suspends a number of OS processes including system software timer counting (timers two, three, four and five; see locations 536 to 558; $218 to $22E).  
  
It is suggested that you do not set [CRITIC](../CRITIC/index.md) for any length of time. When one timer is being set, [CRITIC](../CRITIC/index.md) stops the other timers to do so, causing a tiny amount of time to be "lost". When [CRITIC](../CRITIC/index.md) is zero, both stage one and stage two VBLANK procedures will be executed. When non-zero, only the stage one VBLANK will be processed.  
