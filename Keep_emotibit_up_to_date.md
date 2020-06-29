# Keeping EmotiBit up-to date

## Overview
If you just received your EmotiBit, please checkout our [EmotiBit Getting Started](./Getting_Started.md) startup-guide.

Trying to update EmotiBit Firmware? You are at the right place! **Lets get started!!!**

## Table of Contents
- [Setup](#setup)
- [Programming the Feather](#programming-the-feather)
- [About the WiFi shield](#About-the-WiFi-shield)
## Setup
### Download and install the Arduino IDE
  - https://www.arduino.cc/en/main/software#download
### Add Adafruit Feather boards to Arduino IDE
  - <details>
    <summary><b>Add URL to Adafruit Boards</b></summary>
    <br>
    
    - `File > Preferences > [Settings Tab]`
    - Copy-Paste the following link into `Additional Board Manager URLs:` 
      - https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
    - [*[See Adafruit's page if you'd like instructions with images]*](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/setup)
    </details>
    
  - <details>
    <summary><b>Add support for specific SAMD boards</b></summary>
    <br>
    
    - `Tools > Board: [...] > Boards Manager...`
    - Search for `SAMD`
      - Install `Arduino SAMD Boards (32-bits ARM Cortex-M0+)` *by Arduino*
      - Install `Adafruit SAMD Boards` *by Adafruit* _**(use version 1.5.1)**_
    - [*[See Adafruit's page if you'd like instructions with images]*](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/using-with-arduino-ide)
      - If you're on Windows 7  or 8, the above link also has driver installation instructions (note, however, that EmotiBit software is not officially supported on Windows versions prior to Windows 10)
    </details>
    
### Install firmware libraries
  - Open the Arduino IDE and go to `Tools > Manage Libraries...`
  - Search for and install the following Libraries. **Be sure to install the correct version when specified for any library below**
  - <details>
    <summary><b>Library List</b></summary>
    <br>
    
    - WiFi101 *by Arduino*
    - SdFat *by Bill Greiman*
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
    </details>
    
### Close and re-open Arduino IDE
  - After installing boards or libraries you should close and re-open the Arduino Application to make sure the changes take effect.

## Programming the Feather
- In the Arduino program (IDE), open `File > Examples > EmotiBit FeatherWing > EmotiBit_Example`
  - <img src="./assets/arduino-choose_emotibit_example.png" width="450">
  - Alternatively you can double click the `EmotiBit_Example.ino` file presenst at the location:`Documents/Arduino/libraries/EmotiBit_FeatherWing/examples/Emotibit_Example/` 
- Put the Feather in programming mode by double clicking the reset button. You should see the red LED pulsing.
- In the `Emotibit_Example` Arduino window that opens, Choose `Tools > Board > “Adafruit Feather M0”`
- Choose `Tools > Port > [the correct port for your board]`
  - <img src="./assets/arduino-uploading_FW.png" width="450">

- Click “Upload” button.
  - <img src="./assets/Arduino_upload_button.png" width="350">

## Ready to go!
- Once your feather is successfully uploaded, you are ready to go! [Start working with your data](./Working_with_emotibit_data.md/#Real-Time-Streaming)

## About the WiFi shield
- Adafruit feather M0 works with the `ATWINC1500` for wireless communication. The `ATWINC` exists as a independent submodule to the feather
and might get updates which require a different set of instructions to be followed. 
  - If you are using the feather you received with the EmotiBit, everything is upto data. If you are using 
  a feather purchased independently, check out the documentation to [update the WiFi module](./Contributing_to_emotibit_community/Learn_more_about_emotibit.md/#Update-Feather-WiFi-chip-firmware)  


[comment]: <> (Add links to images below)

[arduino_chooseExample]: ./assets/arduino-choose_emotibit_example.png
[arduino_choosePort]: ./assets/arduino-uploading_FW.png
[arduino_upload_button]: ./assets/Arduino_upload_button.png
