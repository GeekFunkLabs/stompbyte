# stompbyte
 make an ATMega328p produce drum sounds/patterns using PCM when a button is pressed/released
## flashing to ATMega328p

Use the following command to flash the compiled .hex file to the ATMega328p using the SPI interface on a Raspberry PI
```
sudo avrdude -c linuxspi -P /dev/spidev0.0 -p m328p -U flash:w:stompbyte.ino.arduino_standard.hex:i
```

## fuse settings
E:FF, H:DF, L:EF
```
sudo avrdude -c linuxspi -P /dev/spidev0.0 -p m328p -U lfuse:w:0xef:m -U hfuse:w:0xdf:m -U efuse:w:0xff:m
```
