## Overview
If you just received your EmotiBit, please checkout our [EmotiBit Getting Started](./EmotiBit_Getting_Started.md) startup-guide.
Trying to update EmotiBit Firmware? You are at the right place! **Lets get started!!!**

## Table of Contents
- [Setup](#setup)
- [Programming the Feather](#programming-the-feather)

## Setup
- Updating the EmotiBit firmware requires you to have Arduino Installed on your computer. If you do not have Arduino already installed:
    - Download and install the Arduino IDE - https://www.arduino.cc/en/main/software
- Arduino come pre-installed with files required to work with Arduino boards. To Work with the Adafruit Feather M0 WiFi(which comes with the EmotiBit), we are going to install additional libraries using Arduino. Follow these instructions to install the correct board libraries 
  
  - [Adding Feather in additional board managers](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/setup)
    - <details>
      <summary>Click here to check a summary of the above link</summary>
      <br>
      
        - Preferences > Additional Board Manager URLs
        - Copy-Paste the link: https:<span></span>//adafruit.github.io/arduino-board-index/package_adafruit_index.json
      </details>
  
  - **Adding support for SAMD boards**
    - Please be careful of the following: 
        - Only follow the instructions on the link bellow till the section `Install Adafruit SAMD`
        - Under `Install Adafruit SAMD` section, _**(use version 1.5.1)**_
    - [Guide to add support for SAMD Boards](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/using-with-arduino-ide)
      - <details>
        <summary>Click here to check a summary of the above link</summary>
        <br>
      
          - Tools>Board: “..”>Boards Manager
            - Install Arduino SAMD Boards
            - Install Adafruit SAMD _**(use version 1.5.1)**_
        </details>
- If you are using a Feather not provided by us, you might have to update the WiFi shield. [Click here](./Updating_WiFi_Shield.md) to update the WiFi shield.
- Along with the main FW(Firmware), you will also need to grab some other Libraries fo reprogram the EmotiBit.
- Open Arduino IDE is not already open.
- Go to `Tools` > `Library Manager`. Enter the names of the following Libraries in the search box. When the search results show the required library,hover your mouse over the option displayed, click on `install` button that appears. For any Library listed with a particular version, make sure you choose the appropriate version in the dropdown for that library, and install that.
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
- After you have installed the libraries, you can verify the libraries have been downloaded, by checking the `Documents > Arduino > libraries` folder in your system.
- You should close and re-open the Arduino Application to make sure the changes take effect.
- **Note: Make sure you followed any version requirements listed in the above list**

## Programming the Feather
- In the Arduino program (IDE), `open File > Examples > EmotiBit FeatherWing > EmotiBit_Example`
  - Alternatively you can double click the `EmotiBit_Example.ino` file presenst at the location:`Documents/Arduino/libraries/EmotiBit_FeatherWing/examples/Emotibit_Example/` 
  ![][arduino_chooseExample]
- In the open arduino windows, Choose Tools > Board > “Adafruit Feather M0”
- Put the Feather in programming mode by double clicking the reset button. You should see the red LED pulsing and the available port(in _Tools > Port_) should change.
- Choose Tools > Port > `[the correct port for your board]`
![][arduino_choosePort]
- Click “Upload” button.

## Ready to go!
- Once your feather is successfully uploaded, you are ready to go! Grab the [EmotiBit Oscilloscope](https://github.com/emotibit/ofxemotibit/releases/latest), if you have not already got it!

[comment]: <> (Add links to images below)

[arduino_chooseExample]: ../assets/arduino-choose_emotibit_example.png
[arduino_choosePort]: ../assets/arduino-uploading_FW.png