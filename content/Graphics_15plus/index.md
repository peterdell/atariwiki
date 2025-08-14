# Graphics 15+  
  
This is a small example on how to use Graphics 15+ with CC65  
  
General Information  
  
Author: 	Carsten Strotmann   
Language: 	C   
Compiler/Interpreter: 	cc65   
Published: 	2003   
  
Download: [GRA.ATR](attachments/GRA.ATR)  
  
How to get 320x192 Pixel with 4 colors? (Idea: Mario Krix)  
  
To get more colors in hi-res mode (Graphics 8 / Antic Mode $F, 320x192 1 Color), it is possible to mix it with the Graphics 15 Mode (160x192, 4 Colors, Antic Mode $F). This is done be changing the Antic Mode every line. On a normal CRT this lines will melt together.  
  
To get an uniform background, we place 4 Players + 4 Missiles in the Background. The Screen Memory can be used as normal, either direct or through ATARI OS graphic commands.  
  
## Graphics 15+ in C (cc65) (first alpha)  
```
/* -*- C -*- ****************************************************************
 *
 *           Copyright 2003 Carsten Strotmann.
 *               License GPL
 *
 *
 *  System        : cc65 ATARI Target
 *  Module        : 
 *  Object Name   : $RCSfile: GraphicsFifteenPlusCC.txt,v $
 *  Revision      : $Revision: 1.1 $
 *  Date          : $Date: 2003/01/12 21:05:00 $
 *  Author        : $Author: CarstenStrotmann $
 *  Created By    : Carsten Strotmann
 *  Created       : Sun Jan 12 18:12:49 2003
 *  Last Modified : <030112.2152>
 *
 *  Description   Test ATARI Graphics 15+ Mode
 *
 *  Notes
 *
 *  History
 *   
 *  $Log: GraphicsFifteenPlusCC.txt,v $
 *  Revision 1.1  2003/01/12 21:05:00  CarstenStrotmann
 *  none
 *
 *  Revision 1.1  2003/01/12 21:03:00  CarstenStrotmann
 *  none
 *
 *  Revision 1.1  2003/01/12 20:59:58  CarstenStrotmann
 *  none
 *
 *
 ****************************************************************************
 *
 *  Copyright (c) 2003 Carsten Strotmann.
 * 
 *  All Rights Reserved.
 *
 ****************************************************************************/

#include <atari.h>
#include <stdio.h>

typedef unsigned word;
typedef unsigned char byte;

static void g15plus(void)
{
    word dlvec;
    byte anticcmd;
    byte cnt;
    
    graphics(15);            /* Graphics 15 + 16 */
    dlvec = *(word*) 0x0230; /* Display List Startaddress */
    cnt = 0;
    
    do 
    {
        anticcmd = *(byte*) dlvec;
        
        if ((cnt & 0x01) == 1) /* ever odd line */
        {
            if ((anticcmd & 0x0e) == 0x0e)
            {
                *(byte*) dlvec = anticcmd | 0x0f;  /* change to Gr. 8 */
            }
        }
        
        if ((anticcmd & 0x40) == 0x40) /* skip adress reload */
        {
            dlvec++;
            dlvec++;
        }
        dlvec++; /* next line */
        cnt++;
    }
    while (anticcmd != 0x41);   
    
    /* enable background Player / Missile */
    
    *(byte*) 0x022f = 0x2e;   /* enable PM Graphics */
    *(byte*) 0xd01d = 0;      /* disable ANTIC Player & Missile */
    
    *(word*) 0xd00D = 0xffff; /* all bits on Player 0+1 */
    *(word*) 0xd00F = 0xffff; /* all bits on Player 2+3 */
    *(byte*) 0xd011 = 0xff;   /* all bits on Missiles   */
    *(word*) 0xd008 = 0x0303; /* Player 0+1 4xsize      */
    *(word*) 0xd00a = 0x0303; /* Player 2+3 4xsize      */
    *(byte*) 0xd00c = 0xff;   /* all Missiles 4xsize    */
    
    *(byte*) 0xd000 = 0x30;   /* Position Player        */
    *(byte*) 0xd001 = 0x50;
    *(byte*) 0xd002 = 0x70;
    *(byte*) 0xd003 = 0x90;
    
    *(byte*) 0xd004 = 0xB0;   /* Position Missiles      */
    *(byte*) 0xd005 = 0xB8;
    *(byte*) 0xd006 = 0xC0;
    *(byte*) 0xd007 = 0xC8;
    
    *(word*) 0x2c0  = 0x0;   /* Color of PM=background */
    *(word*) 0x2c2  = 0x0;
    
    *(byte*) 0x026f = 1; /* player priority        */
    
    printf("Graphics 15+ Testscreen");
}
int main(void)
{
    g15plus();
    getchar();
    return(0);    
}



```
  
