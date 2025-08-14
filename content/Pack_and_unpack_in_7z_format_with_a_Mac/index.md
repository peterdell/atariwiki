# Pack and unpack in 7z format with a Mac  
First open the Terminal app and type in:  
  
brew install p7zip  
  
The program itself is called: '7z'  
  
In Terminal you can type in:  
  
man 7z  
  
for further information about the program. Please type 'q' to quit the help menu and return to Terminal.  
  
For a smart handling, please type in:  
  
cd <path of the folder, you want to work with>  
  
for example:  
  
cd folder  
  
Even more smart is to just type in 'cd ' (please don't forget the blank after the letter d and then just drag & drop the folder with the archive inside the Terminal window to the actual cursor position! That saves you a lot of typing! :-)  
  
## Example for packing  
For packing a file or an archive, please type in:  
  
7z a file.7z <path of the file>  
  
file.7z is the name of the archive which will be created in 7z format with the suffix 7z.  
  
<path of the file> must be the path on your Mac leading to the file and the file itself at the end, of course. The same is true when dealing with a folder.  
  
## Example for unpacking  
For unpacking a file or an archive, please type in:  
  
7z x <path of the archive.7z>  
  
The program will then unpack the file 'archive.7z' in the same folder.  
  
## Example for packing with compression and strong AES-256 encryption  
7z does not store the owner/group of the file, so adding files using tar before 7z is a good practice:  
  
tar cpvf test.tar test.jpg  
  
7z a -p -mx=9 -mhe -t7z test.7z test.tar  
  
Terminal will ask you after pressing return for your password. Please repeat it once for security reasons and afterwards you are finished. For unpacking please use the example described above.  
  
## Credits  
- Tomasz 'Kr0tki' Krasuski for telling us about the best packer available  
- Carsten Strotmann for sharing the knowledge on how to do it on a Mac as smart as possible  
  
## References  
- [https://www.7-zip.org/download.html](https://www.7-zip.org/download.html)  
- [https://sourceforge.net/projects/sevenzip/](https://sourceforge.net/projects/sevenzip/)  
- [https://www.pontikis.net/blog/easily-compress-encrypt-files-using-7z-p7zip-linux](https://www.pontikis.net/blog/easily-compress-encrypt-files-using-7z-p7zip-linux) ; further info for compression with strong AES-256 encryption  
