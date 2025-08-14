# Check and compare files with a Mac in the Terminal app  
There are different ways to check and compare files on a Mac in the Terminal app. We introduce just some, the user can work with:  
  
SHA-1:  
shasum -a 1 file    ;   file: just drag & drop a file from any place directly to the line in the Terminal app.  
  
SHA-256:  
shasum -a 256 file    ;   file: just drag & drop a file from any place directly to the line in the Terminal app.  
  
MD5:  
md5 file    ;   file: just drag & drop a file from any place directly to the line in the Terminal app.  
  
To compare 2 files (DOS), try:  
fc /b file1 file2 >log.txt   ;   in the log.txt (same directory) you get the results.  
  
on a Mac in the Terminal app:  
cmp -l file1 file2  
