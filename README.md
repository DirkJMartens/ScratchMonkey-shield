# ScratchMonkey-shield
HVPP shield for Arduino Uno using ScratchMonkey hardware and software

The original "programmers.txt" file provided is not compatible with the newer versions of the Arduino IDE. 
Both syntax and location have changed. However, they can be quite easily modified to make them compatible. 
1. Location: 
- Inside your sketch folder, create a folder called "hardware" 
- If you have installed boards using the Board Manager, the folder may already exist. 
- Create a folder inside it called "ScratchMonkey" and inside that create another folder called "avr". 
- Copy the 3 files into this "avr" folder. 
2. Syntax: 
- Changes to "programmers.txt" include the addition of 
    - ".program.protocol", ".program.tool", ".program.params.verbose", ".program.params.quiet" and ".program.extra_params". 
    - The "extra_params" value of "-Pcom4" defines COM4 as the port that the Arduino Uno is connected to. 
    - The "-F" options can be removed because it is used to ignore an invalid signature. 
- The content of the "platform.txt" file is a copy of the bottom section of the file with the same name in the Arduino installation folder (in "Programs Files (x86)" on Windows). 
- The "boards.txt" can be empty but must exist. I put a "#" comment file as github doesn't accept empty files. 

After dropping these 3 files into the "avr" folder, restarting the Arduino IDE should show 6 new programmers. 
When used in combination with the stock-version of "avrdude", only the last 3 ("STK500 mode") are usable. 
If you recompile the "avrdude" source code modified with the patch, the first 3 should also work. 
Ensure you are using the right connection diagram: ISP versus HV-serial versus HV-parallel uses different wiring between programmer and target. 
And only the patched version will have the LEDs working. 
