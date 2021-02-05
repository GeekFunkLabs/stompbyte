# StompByte
The StompByte uses an ATMega328p produce drum sounds/patterns using PCM when a button is pressed/released. Holding the button for 2sec will change sounds/patterns, and play a short preview. There are 10 samples and 3 patterns:
1. muted kick
1. rock kick
1. tr808 kick
1. woodblock
1. cross stick
1. tambourine
1. handclap
1. mario bump
1. mario fireball
1. mario jump
1. pattern: rock kick – woodblock – tambourine – woodblock
1. pattern: tr808 kick – tambourine – handclap – tambourine
1. pattern: mario bump – mario fireball – mario jump – mario fireball
 
## Compiling/Flashing
The code is written for the Arduino IDE. The code can be most easily compiled and flashed to the ATMega328P by swapping it with the ATMega in an Arduino UNO and uploading the code, then swapping the ATMega back into the StompByte. You can also use your own programmer, in which case you should use the Boards Manager in the IDE to install the DIY AVR boards definitions, then select the ATMega328P as your board and select 16MHz crystal/resonator as your processor speed.To compile a .hex file for flashing directly using your own programmer, choose "Export compiled Binary" in the IDE.

To program your ATMega328P using a Raspberry Pi, make the following connections from the GPIO header:

RPi Physical Pin | ATMega328P
-------------|-----------
23 (SCLK) | 19 (SCK)
21 (MISO) | 18 (MISO)
19 (MOSI) | 17 (MOSI)
22 (GPIO25) | 1 (RESET)
2 (5V) | 7 (VCC)
6 (GND) | 8 (GND)

You must also connect a 16MHz clock source (quartz oscillator) to pins 9&10 (XTAL1&2) on the ATMega, and ground each pin through a 22pF capacitor. Enter the following commands to flash the compiled .hex file and properly set the fuses (E:FF, H:DF, L:EF) on the ATMega328p using the SPI interface on a Raspberry PI:
```
sudo apt install avrdude
sudo avrdude -c linuxspi -P /dev/spidev0.0 -p m328p -U flash:w:stompbyte.ino.arduino_standard.hex:i
sudo avrdude -c linuxspi -P /dev/spidev0.0 -p m328p -U lfuse:w:0xef:m -U hfuse:w:0xdf:m -U efuse:w:0xff:m
```

## Modifying
You can change the sounds in the StompByte by modifying the code and re-flashing the ATMega328P as described above. You must save your audio samples as 8-bit, 8kHz .wav files - the ATMega328P can store roughly ~4 seconds total of audio this way. Convert your samples to an array of integers and replace the contents of the variables at the top of _stompbyte.ino_ - you may want to rename some of the variables. Consult the comments in _PCM.h_ for help converting your samples to integers.
