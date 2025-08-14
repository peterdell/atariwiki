Forty-byte character line buffer, used to temporarily buffer one physical line of text when the screen editor is moving screen data. The pointer to this buffer is stored in 100, 101 ($64, $65) during the routine.  
  
Dieser Puffer (40 ($28) Zeichen lang) wird vom Bildschirmtreiber benötigt, um hier temporär Daten während des Verschiebens des Bildschirminhaltes zu speichern. Auf diesen Puffer wird durch ADRESS (100,101; $64,$65) gezeigt. Bei den XL- und XE-Geräten ist dieser Puffer entfallen.  
