# U-Basic  
drac030 from Poland  
  
The U-BASIC is a version of [Atari_BASIC](../Atari_BASIC/index.md) Revision C that has been recompiled so that it resides under the OS ROM in the XL and XE machines. As a result, it offers 8k RAM more for your programs: depending on the configuration, there should be up to 46042 bytes free. This is very useful when you have a program that is too large to use with DOS installed, it should be able to run with any DOS using U-BASIC.  
  
U-BASIC also replaces the original, and very slow, floating-point math libraries found in the Atari OS ROM as part of its loading process. These are replaced by the routines from Charles's Marslett fast FP package, originally part of the Newell FASTCHIP upgrade. These are slightly slower than the versions found in [Turbo-BASIC_XL](../Turbo-BASIC_XL/index.md), but much, much faster than the version found in the original ROM, which was also used in Atari BASIC.  
  
There are no special hardware requirements, an XL/XE computer with 6502 and 64k RAM ought to be enough.  
## References  
- [Infos](http://drac030.krap.pl/en-ub-info.php)  
- [Downloads](http://drac030.krap.pl/en-ub-pliki.php)  
