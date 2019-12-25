## Overview
If you just received your EmotiBit, please checkout our [EmotiBit Getting Started](https://github.com/EmotiBit/EmotiBit_Docs/blob/EmotiBit-V2/Hello_EmotiBit-Introduction_to_EmotiBit/EmotiBit_Getting_Started.md) startup-guide.
This guide describes how to update the firmware on the EmotiBit.
## Table of Contents
- [Setup](#setup)
- [Programming the Feather](#programming-the-feather)
- [Connecting to WiFi](#connecting-to-wifi)

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
  - If you got your Feather shipped with your EmotiBit, it has the latest FW (currently (FW 19.6.1) on the WINC1500 WiFi module and doesn't require updating, but if you got your Feather from Adafruit or elsewhere it might require updating to work properly with the high data demands EmotiBit requires.
  - Here are some handy instructions to identify which WINC1500 FW you have and update it if necessary https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/using-the-wifi-module
- Install Libraries via Tools > Library Manager
  - WiFi101
  - SdFat
  - Adafruit SleepyDog
  - ArduinoJson _**(version 5.13.5, not v6.x.x)**_
  - EmotiBit_MAX30101_Library
  - EmotiBit Si7013
  - EmotiBit BMI160
  - EmotiBit FeatherWing
  - EmotiBit_MLX90632_Digital_Thermopile
  - EmotiBit_NCP5632_Led_Driver


## Programming the Feather
- Get the latest release of EmotiBit_FW as described in [setup](#setup)
- In the Arduino program (IDE), open File > Examples > EmotiBit FeatherWing > EmotiBit_Example
  - Alternatively you can double click Arduino/libraries/EmotiBit_FeatherWing/examples/Emotibit_Example/EmotiBit_Example.ino
- Choose Tools>Board>“Adafruit Feather M0”
- Put the Feather in programming mode by double clicking the reset button. You should see the red LED pulsing and the available port(in _Tools > Port_) should change.
- Choose Tools>Port>[the correct port for your board]
- Click “Upload”
- _**NOTE**_: Currently, EmotiBit will not record data to the SD card unless it [connects to WiFi](#connecting-to-wifi), due to timestamp reliability

## Connecting to WiFi
- To connect to WiFi with an Adafruit Feather M0 Wifi board, you can add the WiFi credentials to a file named “config.txt” on an SD card.
- The SD card must be in the FAT32 format, which can be checked by _right click > properties > file system(_under the **General**_ tab)_ on Windows
  - if the card is not in FAT32 format it can be reformatted by _right click > format > file system_ on Windows
  - Other operating systems, or large SD card capacities may require the use of 3rd party partitioners such as AOMEI
- After you have made sure that the SD-Card is in FAT32 format, you can follow the following steps to Add the Config file to the SD-Card
  - Create a **config.txt** file on the SD-Card.
  - The contents of the file should be in JSON format as shown below:
    - ``{"WifiCredentials": [{"ssid": "Foo", "password" : "Bar"}]}``
    - Copy paste the above line in the **config.txt** file. Replace `Foo` with the `WiFi name` and `Bar` with the `WiFi password`.
- **Multiple WiFi Networks (EmotiBit FeatherWing v0.5.4+)**
  - a JSON list can be used to store up to 12 sets of network credentials in config.txt:
    - ``{"WifiCredentials": [{"ssid": "Foo", "password" : "Bar"},{"ssid": "Fnord", "password" : "Fnord"}]}``
  - In the setup of EmotiBit_Example, all the WiFi networks are tried sequentially, a process that times out at ~1min. If quick connection is desired after programming or reset:
    - Shorten the list
    - Organize the list in order of priority of connection
  - If connection is lost to the original network, EmotiBit will continue to try to reconnect for 5 min before attempting another network. This timeout period can be changed by setting WIFI_BEGIN_SWITCH_CRED in EmotiBit_Example.ino
