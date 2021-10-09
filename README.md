# SplitKeeb

### SplitKeeb is a custom designed split keyboard based on the QMK Firmware and 2 Arduino Pro Micros.

This keyboard was a joint project with my friends David and Raheel. 


![Split Keyboard](https://i.imgur.com/PnGtwbe.jpeg)

![KiCad view](https://i.imgur.com/sWV3AiR.png)

![Real Life PCB](https://i.imgur.com/Sz99NFG.jpg)

This is a *split* keyboard design, and uses I2C to communicate over a TRRS audio cable (4 poles). 

The parts list is as follows:
* 62 of any Cherry MX style key Switch
* 62 1N4148 Zener Diodes
* 2 identical Resistors from a range of 2.2k Ohms to 10k Ohms (4.7k recommended) 
* 2 Arduino Pro Micros
* 2 PJ-320A TRRS Female Jacks
* 1 TRRS Male to Male wire
* 10 M3 x 8mm Bolts
* 10 M3 nuts

The 2 resistors are for the I2C line, make sure to solder them to whichever board you want to use as the 'main' side.
This design allows resistors to be soldered to both sides, enabling the user to easily switch between either halves as the 'main' side. 

Make sure to plug in the TRRS cable **BEFORE** you plug in the USB cable, otherwise you risk shorts as the TRRS cable supplies power to the other board.

To program the keyboard, the eaisest method is to use the [QMK Toolbox](https://github.com/qmk/qmk_toolbox), and flash both Pro Micros with the same 'SplitKeeb.hex' file. After both boards have been flashed, plug in the TRRS cable, and then plug in USB, and the keyboard should work as normal. 

Switching between Main/Master halves can be made easy by flashing the EEPROM of the arduinos with their handedness. The steps are as follows:
* Add '#define EE_HANDS' to your config file.
* Enter your qmk environment and cd into your qmk firmware folder. 
* With the left side of your keyboard plugged in, type 'make kb:default:avrdude-split-left' where kb is the filepath of your keyboard and default is the filepath of your keymap. After some compilation, the environment will prompt you to put your arduino into flash mode, which can be done by shorting RESET to GROUND. 
* Repeat with the right side plugged in, this time typing 'make kb:default:avrdude-split-right'

This permenantly flashes the 'handedness' of the keyboard to each arduino. 

