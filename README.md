# ScratchMonkey-shield
HVPP shield for Arduino Uno using ScratchMonkey hardware and software. 

Based on the work of Matthias Neeracher. Details on https://github.com/microtherion/ScratchMonkey. 

The original "programmers.txt" file provided is not compatible with the newer versions of the Arduino IDE. 
Both syntax and location have changed. However, they can be quite easily modified to make them compatible. 
(Refer to the "Issues" section of Matthias' github for some details). 

1. Location of Arduino IDE config files: 
- Inside your sketch folder, create a folder called "hardware" 
- If you have installed boards using the Board Manager, the folder may already exist. 
- Create a folder inside it called "ScratchMonkey" and inside that create another folder called "avr". 
- Copy the 3 files into this "avr" folder. 

2. New syntax of config files: 
- Changes to "programmers.txt" include the addition of ".program.protocol", ".program.tool", ".program.params.verbose", ".program.params.quiet" and ".program.extra_params". 
- The content of the "platform.txt" file is a copy of the bottom section of the file with the same name in the Arduino installation folder (in "Programs Files (x86)" on Windows). 
- The "boards.txt" can be empty but must exist. I put a "#" comment file as github doesn't accept empty files. 

3. AVRDUDE Software: 
- After dropping these 3 files into the "avr" folder, restarting the Arduino IDE should show 6 new programmers. 
- When used in combination with the stock-version of "avrdude", only the last 3 ("STK500 mode") are usable. 
- If you recompile the "avrdude" source code modified with the patch, the first 3 should also work (have not tested/tried myself). 
- Regardless of "avrdude" version used, the connections/wiring between the Uno-programmer and target-chip will be different. 
- And only the patched version of "avrdude" will have the LEDs working in ISP and HVSP modes. 

4. Shield Hardware: 
- Further, ensure you are using the right connection diagram depending on whether you want to program using ISP, HVSP or HVPP. 
- The target AVR chip you use will change the wiring. Kindly refer to the documentation of Scratchmonkey for details. 
- ISP-method: 
  - The ISP-method can use a standard "Arduino as ISP" shield as it uses only the standard 6 ICSP connections (MISO/MOSI/SCK/SS/Vcc/GND). 
  - The LED status will not be correct since wiring and pinout is different, even when using the patched avrdude software. 
  - To use the ScratchMonkey shield as an ISP programmer, open the ScratchMonkey sketch in the Arduino IDE, select "Arduino Uno" under "Tools - Board" and select the appropriate COM port. 
  - Then use "Upload" to load the ScratchMonkey sketch into your Arduino Uno board. 
  - Next load the sketch you want to upload into your target chip into the Arduino IDE (e.g. Blink). 
  - Install/wire up your target chip and in the Arduino IDE, select the appropriate target under "Tools - Board" (e.g. ATMega328 on breadboard) and select "ScratchMonkey" under "Tools - Programmer". 
  - Then use "Upload using Programmer" (NOT "Upload") to load the Blink sketch into the target. 
  - If you use "Upload" instead of "Upload using Programmer" you will overwrite the ScratchMonkey sketch in the Arduino Uno programmer instead of loading the Blink sketch into the target chip. 
- HVPP-method: 
  - The shield I created is the "HVPP" version (see pic). It is implemented on an Arduino Uno protoboard shield using wire-wrapping and ZIF-socket. 
  - In the bottom-right hand corner is the connection header for +12V, +5V and GND. 
  - For the HVPP-shield, no status lights are available so the stock version of "avrdude" works. 
