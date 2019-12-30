## Overview
If you just received your EmotiBit, please checkout our [EmotiBit Getting Started](https://github.com/EmotiBit/EmotiBit_Docs/blob/EmotiBit-V2/Hello_EmotiBit-Introduction_to_EmotiBit/EmotiBit_Getting_Started.md) startup-guide.
This guide describes how to update the firmware on the EmotiBit.
## Table of Contents
- [Setup](#setup)
- [Programming the Feather](#programming-the-feather)

## Setup
- Download and install the Arduino IDE - https://www.arduino.cc/en/main/software
- Follow these instructions to install the correct board libraries 
  - https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/setup
    - <details>
      <summary>To summarize the above link</summary>
      <br>
      
        - Preferences > Additional Board Manager URLs
        - Copy-Paste the link: https:<span></span>//adafruit.github.io/arduino-board-index/package_adafruit_index.json
      </details>
  
  - https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/using-with-arduino-ide
    - <details>
      <summary>To summarize the above link</summary>
      <br>
      
        - Tools>Board: “..”>Boards Manager
          - Install Arduino SAMD Boards
          - Install Adafruit SAMD _**(use version 1.5.1)**_
      </details>
- Check whether you need to update the WINC1500 WiFi module firmware
  - On the Adafruit M0 WiFi Feather the main FW lives on the SAMD21 "brain" that controls the EmotiBit, but there is also FW on the WINC1500 WiFi slave module that handles the WiFi transmissions. Occasionally there are updates to that FW that fixes a bug or or lowers power consumption or something and it requires a special process to update it.
  - **If you got your Feather shipped with your EmotiBit, it already has the latest FW (currently (FW 19.6.1) on the WINC1500 WiFi module and doesn't require updating**, but if you got your Feather from Adafruit or elsewhere it might require updating to work properly with the high data demands EmotiBit requires.
  - Here are some handy instructions to identify which WINC1500 FW you have and update it if necessary https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/using-the-wifi-module
- Install Libraries via Tools > Library Manager
  - WiFi101
  - SdFat
  - Adafruit SleepyDog
  - ArduinoJson _**(version 5.13.5, not v6.x.x)**_
  - EmotiBit FeatherWing
  - EmotiBit_MAX30101_Library
  - EmotiBit Si7013
  - EmotiBit BMI160
  - EmotiBit MLX90632
  - EmotiBit NCP5632


## Programming the Feather
- Get the latest release of EmotiBit_FW(**EmotiBit FeatherWing** Library downloaded in the Previous step) 
as described above in [setup](#setup)
- In the Arduino program (IDE), open File > Examples > EmotiBit FeatherWing > EmotiBit_Example
  - Alternatively you can double click Arduino/libraries/EmotiBit_FeatherWing/examples/Emotibit_Example/EmotiBit_Example.ino
- Choose Tools > Board > “Adafruit Feather M0”
- Put the Feather in programming mode by double clicking the reset button. You should see the red LED pulsing and the available port(in _Tools > Port_) should change.
- Choose Tools > Port > [the correct port for your board]
- Click “Upload”
- _**NOTE**_: You must [connect to WiFi](#connecting-to-wifi) to begin recording data to the SD card. This is required to maintain high timestamp reliability.

## Ready to go!
- See [`EmotiBit_Getting_Started`](./EmotiBit_Getting_Started.md) to start streaming data from your body!
