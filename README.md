# optiboot-installer
Arduino as ISP

## Description
Using the Arduino IDE, it is possible to update the Arduino Nano bootloader from the old one (*ATmega328P (Old Bootloader)*) to the new Optiboot (*ATmega328P*) by using another Arduino (e.g., a Nano) as an ISP programmer.

## Connections

The following table shows how to connect the two Arduinos, keeping in mind that only the programmer Arduino is connected via USB.

| Arduino ISP (Master) | Arduino Target (Slave) |
| -------------------- | ---------------------- |
| 5V                   | 5V                     |
| GND                  | GND                    |
| D10                  | RST                    |
| D11                  | D11                    |
| D12                  | D12                    |
| D13                  | D13                    |

## Instructions

Linux environment (Ubuntu) using Flatpak.

1. Install Arduino IDE v2 via Flatpak.
2. Install Arduino AVR Boards from the Arduino IDE (*Tools &rarr; Board &rarr; Boards Manager*).
3. In `~/.arduino15/packages/arduino/hardware/avr/<AVR_VERSION>`, modify the setting `nano.menu.cpu.atmega328old.bootloader.file` in the `boards.txt` file by copying the value from `nano.menu.cpu.atmega328.bootloader.file`. By modifying this configuration, regardless of the selected processor (referring to the programmer Arduino), the new bootloader will be uploaded.
4. Restart the Arduino IDE.
5. Upload the `ArduinoISP.ino` sketch to the programmer Arduino (remember to select the correct board, port, and processor in the *Tools* menu, referring to the programmer Arduino).
6. Select *Arduino as ISP* in *Tools &rarr; Programmer*.
7. Burn the new bootloader via *Tools &rarr; Burn Bootloader*.
   1. If errors occur, try burning the bootloader again by first selecting *AVR ISP* as the programmer (this will fail), then switching back to *Arduino as ISP* and burning the bootloader again.