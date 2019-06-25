# Getting Started with EmotiBit

## Setup
- Download and install the Arduino IDE - https://www.arduino.cc/en/main/software
- Follow these instructions to install the correct board libraries 
  - https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/setup
    - Preferences -> Additional Board Manager URLs
      - https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
  - https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/using-with-arduino-ide
    - Tools>Board: “..”>Boards Manager
      - Install Arduino SAMD Boards
      - Install Adafruit SAMD
- Follow instructions to set up the Adafruit M0 WiFi Feather https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/using-the-wifi-module
- Install Libraries via Tools -> Library Manager
  - WiFi101
  - SdFat
  - Adafruit SleepyDog
  - ArduinoJson _**(version 5.13.5, not v6.x.x)**_
  - EmotiBit Si7013
  - SparkFun_MAX3010x_Pulse_and_Proximity_Sensor_Library
- Manually download or clone into Arduino/libraries
  - BMI160-Arduino
    - https://github.com/EmotiBit/BMI160-Arduino
  - EmotiBit_FW
    - https://github.com/EmotiBit/EmotiBit_FW

## Programming the Feather
- Get the latest release from
  - https://github.com/EmotiBit/EmotiBit_FW/releases
- Unzip the folder
- Double click on the .ino file to open it in Arduino
- Choose Tools->Board->“Adafruit Feather M0”
- Put the Feather in programming mode by double clicking the reset button. You should see the red LED pulsing and the available port should change.
- Choose Tools>Port>[the correct port for your board]
- Click “Upload”

## Connecting to WiFi
- To connect to WiFi with an Adafruit Feather M0 Wifi board, you can add the WiFi credentials to a file named “config.txt” on the SD card. The contents of the file should be JSON in the following format: 
  - ``{"WifiCredentials": [{"ssid": "SSSS", "password" : "PPPP"}]}``

## Repositories
- Parent Github
  - https://github.com/EmotiBit/
- Android App
  - https://github.com/EmotiBit/EmotiBit_Android_App/
- Firmware
  - https://github.com/EmotiBit/EmotiBit_FW
  - Latest release: https://github.com/EmotiBit/EmotiBit_FW/releases
- OpenFrameworks
  - https://github.com/connectedfuturelabs/CFL_SW_BiosensorModule/
  - Latest release: https://github.com/connectedfuturelabs/CFL_SW_BiosensorModule/releases/


