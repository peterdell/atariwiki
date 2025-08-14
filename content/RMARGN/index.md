||ADR||HEXADR||NAME||Description||shadow||OS  
|83|$0053|RMARGN|Right margin of text|none|All  
  
  
Right margin of the text screen initialized to 39 ($27). Both locations 82 and 83 are user-alterable, but ignored in all GRAPHICS modes except zero and the text window.  
Margins work with the text window and blackboard mode and are reset to their default values by pressing RESET. Margins have no effect on scrolling or the printer. However, DELETE LINE and INSERT LINE keys delete or insert 40 character lines (or delete one program line), which always start at the left margin and wrap around the screen edge back to the left margin again. The right margin is ignored in the process. Also, logical lines are always three physical lines no matter how long or short you make those lines.  
The beep you hear when you are coming to the end of the logical line works by screen position independent of the margins. Try setting your left margin at 25 (POKE 82,25) and typing a few lines of characters. Although you have just a few characters beyond 60, the buzzer will still sound on the third line of text.  
  
Previous: [LMARGN](../LMARGN/index.md)  
  
Next: [ROWCRS](../ROWCRS/index.md)  
