---
title: How to find the revision number of ACTION
---
# How to find the revision number of ACTION!  
The ACTION! cartridge itself has gone through a couple of changes since its first appearance in August 1983. You can tell which version you have by using the "?" (display memory) command in the monitor to examine cartridge address $BOOO. To jump into the monitor simply press SHIFT & CONTROL & M to jump into the monitor in ACTION! Then type "?$B000" and hit RETURN. ACTION! should now show the content of the $B000 register. If this byte equals $31 hex, you have the original version 3.1. A value of $33 hex indicates version 3.3, in which a number of minor 3.1 bugs have been corrected. The final version is 3.6 ($36 hex at $BOOO). The following two pictures show this in detail.  
  
## Pictures  
![](attachments/Action_version1.jpg)  
ACTION! - monitor mode with typed in "?$B000"  
  
![](attachments/Action_version2.jpg)  
ACTION! - monitor mode result after typed in "?$B000" ; here version 3.6 was in use  
