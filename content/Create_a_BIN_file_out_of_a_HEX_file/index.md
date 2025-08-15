---
title: Create a BIN file out of a HEX file
---
# create a BIN file out of a HEX file  
This is an example on how to do it with Mac OS X in the app Terminal:  
  
For a single file please use:  
  
xxd -r -p HEX.IN BIN.OUT  
  
For multiple files in the folder 'IN' to store in the folder 'OUT' please use:  
  
cd ./IN  
for filename in *; do  
xxd -r -p $filename ../OUT/$filename  
done  
