## Overview
If you just received your EmotiBit, please checkout our [EmotiBit Getting Started](./EmotiBit_Getting_Started.md) startup-guide.
Trying to update EmotiBit Firmware? You are at the right place! **Lets get started!!!**

## Table of Contents
- [Setup](#setup)
- [Programming the Feather](#programming-the-feather)

## Setup
- ### Download and install the Arduino IDE
  - https://www.arduino.cc/en/main/software#download
- ### Add Adafruit Feather boards to Arduino IDE
  - #### Point Arduino IDE at Adafruit boards library
    - `File > Preferences > [Settings Tab]`
    - Copy-Paste the following link into `Additional Board Manager URLs:` 
      - https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
    - [*[See Adafruit's page if you'd like instructions with images]*](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/setup)
  - #### Add support for specific SAMD boards
    - `Tools > Board: [...] > Boards Manager...`
    - Search for `SAMD`
    - Install `Arduino SAMD Boards (32-bits ARM Cortex-M0+)` *by Arduino*
    - Install `Adafruit SAMD Boards` *by Adafruit* _**(use version 1.5.1)**_
    - [*[See Adafruit's page if you'd like instructions with images]*](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/using-with-arduino-ide)
- ### Install firmware libraries
  - Open the Arduino IDE and go to `Tools > Manage Libraries...`
  - Search for and install the following Libraries. **Be sure to install the correct version when specified for any library below**
    - WiFi101 by Arduino
    - SdFat by Bill Greiman
    - ArduinoJson _**(version 5.13.5, not v6.x.x)**_
    - Arduino Low Power
    - RTCZero
    - EmotiBit BMI160
    - EmotiBit FeatherWing
    - EmotiBit MAX30101
    - EmotiBit MLX90632
    - EmotiBit NCP5632
    - EmotiBit SI7013
    - EmotiBit XPlat Utils
- ### Close and re-open Arduino IDE
  - After installing boards or libraries you should close and re-open the Arduino Application to make sure the changes take effect.
- ### Update Feather WiFi chip firmware
  - Occasionally there are important updates to the Feather WiFi chip firmware. **If you recently got your Feather M0 WiFi board from us, you're up-to-date and good-to-go**, [but if not you should follow these instructions](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/using-the-wifi-module)
## Programming the Feather
- In the Arduino program (IDE), open `File > Examples > EmotiBit FeatherWing > EmotiBit_Example`
  ![][arduino_chooseExample]
  - Alternatively you can double click the `EmotiBit_Example.ino` file presenst at the location:`Documents/Arduino/libraries/EmotiBit_FeatherWing/examples/Emotibit_Example/` 
- Put the Feather in programming mode by double clicking the reset button. You should see the red LED pulsing.
- In the `Emotibit_Example` Arduino window that opens, Choose `Tools > Board > “Adafruit Feather M0”`
- Choose `Tools > Port > [the correct port for your board]`
![][arduino_choosePort]
- Click “Upload” button.

## Ready to go!
- Once your feather is successfully uploaded, you are ready to go! Grab the [EmotiBit Oscilloscope](https://github.com/emotibit/ofxemotibit/releases/latest), if you have not already got it!

[comment]: <> (Add links to images below)

[arduino_chooseExample]: ../assets/arduino-choose_emotibit_example.png
[arduino_choosePort]: ../assets/arduino-uploading_FW.png
