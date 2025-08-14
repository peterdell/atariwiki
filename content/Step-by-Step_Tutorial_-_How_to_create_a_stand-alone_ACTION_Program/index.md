### Step-by-Step Tutorial: How to create a stand-alone ACTION! Program  
  
1. download a RUNTIME Source, either the original OSS Runtime -> [Original_ACTION_System_Runtime_Source](../Original_ACTION_System_Runtime_Source/index.md) or the alternative Runtime (Peter Finzel, Carsten Strotmann) -> [Alternative_ACTION_Runtime_Source](../Alternative_ACTION_Runtime_Source/index.md)  
1. (optional) delete all runtime parts your program don't need (like SOUND etc), but be aware of dependencies  
1. Include the Runtime File at the top of your ACTION! Source, INCLUDE "D:SYSTEM.ACT"  
1. save your ACTION! Source to disk, clear the ACTION! editor  
1. go to the ACTION! Monitor, complie your Program from Disk 'C "D:MYPGM.ACT"'  
1. Save the compiled binary to disk with 'W "D:MYPGM. COM"'  
1. switch off Computer, remove ACTION! Cart, boot DOS and test your Program from DOS  
  
  
```
INCLUDE "D:SYSTEM.ACT"

PROC main()
 BYTE I=[10],J=[15]
 GRAPHICS(2)
 PRINTDE(6,"Hello World")
 I=I*J ; shows that multiplication works
RETURN
```
