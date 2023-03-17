# Keeping EmotiBit up-to date

## Overview
If you just received your EmotiBit, please checkout our [EmotiBit Getting Started](./Getting_Started.md) startup-guide.

Trying to update EmotiBit Firmware? You are at the right place! **Lets get started!!!**

## Table of Contents
- [Update firmware using EmotiBit FirmwareInstaller](#Update-firmware-using-EmotiBit-FirmwareInstaller)
- [Update firmware using Arduino IDE](#Update-firmware-using-Arduino-IDE)
  - [Setup](#setup)
  - [Programming the Feather](#programming-the-feather)
  - [About the WiFi shield](#About-the-WiFi-shield)
- [Building firmware using PlatformIO](#Building-firmware-using-PlatformIO)
  - [Requirements](#Requirements)
  - [Steps to build from source](#Steps-to-build-from-source)
    - [Get the correct board version for Feather M0](#Get-the-correct-board-version-for-Feather-M0)
    - [Download required dependencies](#Download-required-dependencies)
    - [Building the project](#Building-the-project)

## Update firmware using EmotiBit FirmwareInstaller
Using the `EmotiBit FirmwareInstaller` is the easiest way to update EmotiBit firmware.
Just follow the steps listed in the [Installing EmotiBit Firmware](./Getting_Started.md/#Installing-EmotiBit-Firmware) section on the **Getting Started** page.
<br>
If you want to build EmotiBit firmware from source, check out the section below.
## Update firmware using Arduino IDE
Setting up and using the Arduino IDE is recommended if you want to build EmotiBit firmware from source. 
Follow the steps below to get started!
### Setup
#### Download and install the Arduino IDE
  - https://www.arduino.cc/en/main/software#download
#### Add Adafruit Feather boards to Arduino IDE

- For Feather ESP32 huzzah boards
  - <details><summary><b>Add URL for ESP boards</b></summary>
    
    - `File > Preferences > [Settings Tab]`
    - Copy-Paste the following link into `Additional Board Manager URLs:`. Note: Use `,` to separate a list of URLs
      - https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
    - [See Espressif's page for detailed instructions ](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html)
    </details>
  
  - <details><summary><b>Add support for ESP boards</b></summary>
    <br>
    
    - `Tools > Board: [...] > Boards Manager...`
    - Search for `ESP32`
      - Install `esp32` *by Espressif Systems* **version 2.0.3**
    </details>

- For Feather M0 WiFi boards
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
    
#### Install firmware libraries
  - Open the Arduino IDE and go to `Tools > Manage Libraries...`
  - Search for and install the following Libraries.
```diff
-- Be sure to install the correct version when specified for any library below --
```
  - <details>
    <summary><b>Library List</b></summary>
    <br>
    
    - WiFi101 *by Arduino*
    - SdFat *by Bill Greiman*
    - ArduinoJson _**(version 5.13.5, not v6.x.x)**_
    - Arduino Low Power
    - RTCZero
    - Adafruit_GFX_Library
    - Adafruit_IS31FL3731_Library
    - EmotiBit FeatherWing
      - It will automatically install the following EmotiBit dependencies
        - EmotiBit BMI160
        - EmotiBit MAX30101
        - EmotiBit MLX90632
        - EmotiBit NCP5632
        - EmotiBit SI7013
        - EmotiBit External EEPROM 
        - EmotiBit ADS1X15
        - EmotiBit XPlat Utils
        - EmotiBit EmojiLib
    </details>
    
#### Close and re-open Arduino IDE
  - After installing boards or libraries you should close and re-open the Arduino Application to make sure the changes take effect.

### Programming the Feather
- In the Arduino program (IDE), open `File > Examples > EmotiBit FeatherWing > EmotiBit Example`
  - <img src="./assets/arduino-choose_emotibit_example.png" width="450">
  - Alternatively you can double click the `EmotiBit_Example.ino` file presenst at the location:`Documents/Arduino/libraries/EmotiBit_FeatherWing/EmotiBit_stock_firmware/EmotiBit_stock_firmware.ino` 
- Put the Feather in programming mode by double clicking the reset button. You should see the red LED pulsing.*(Please note that the LED pulsates only in EmotiBit V2 and not V3. You can find your EmotiBit version printed near the board edge on the front top right corner)*
- In the `Emotibit_Example` Arduino window that opens, Choose the board you will be programming
  - For Feather M0 WiFi: `Tools > Board > Adafruit SAMD (32-bits ARM Cortex-M0+ and Cortex-M4) Boards > Adafruit Feather M0`
  - For feather ESP32 Huzzah: `Tools > Board > ESP32 Arduino > Adafruit ESP32 Feather`
- Choose `Tools > Port > [the correct port for your board]`
  - <img src="./assets/arduino-uploading_FW.png" width="450">

- Click “Upload” button.
  - <img src="./assets/Arduino_upload_button.png" width="350">

### Ready to go!
- Once your feather is successfully uploaded, you are ready to go! [Start working with your data](./Working_with_emotibit_data.md/#Real-Time-Streaming)

### About the WiFi shield
- Adafruit feather M0 works with the `ATWINC1500` for wireless communication. The `ATWINC` exists as a independent submodule to the feather
and might get updates which require a different set of instructions to be followed. 
  - If you are using the feather you received with the EmotiBit, everything is upto data. If you are using 
  a feather purchased independently, check out the documentation on the [Adafruit website](https://learn.adafruit.com/adafruit-winc1500-wifi-shield-for-arduino/updating-firmware).

## [WIP] Building firmware using PlatformIO
Note: This section is for advanced users who have experience with programming for
embedded environemts. Using platformIO as a build tool is still being tested and this section will be imrpoved as
we create our structure to use platformIO. <br>

### Requirements
To start using PlatformIO, you will need:
1. PlatformIO development environment
    - Get the platformIO development environment using instructions available on their [website](https://platformio.org/platformio-ide).
    - We have tested this build process with `PlatformIO`+`VScode`.
2. A platformIO `.ini` project file
    - A `platformIO.ini` file has been included inside the firmware variant directory (see directory structure below).

### Steps to build from source

#### [WIP] Get the correct board version for Feather M0
- The latest firmware on EmotiBit uses an older `Adafruit SAMD board package (v1.5.1)`
  - A history of all versions can be found [here](https://github.com/adafruit/ArduinoCore-samd/releases)
- To get an environment set up in platformIO, we need to specify the `board`, `platform` and the `framework` in the `.ini` file.
- For our code, that looks something like
```
[env:adafruit_feather_m0]
platform = atmelsam @3.8.1
board = adafruit_feather_m0 
framework = arduino
```
- We need to explicitely specify the `atmelsam` version as `v3.8.1` because as per the release notes, that platformio version is parity 
for adafruit samd board package v1.5.1. You can check this in the release notes for [`v3.8.0`](https://github.com/platformio/platform-atmelsam/releases/tag/v3.8.0)
- But, this version of the `platform` is only compatible with an earlier version of the `framework`([v4.3.0](https://github.com/platformio/platformio-pkg-framework-arduinosam)) which unfortunately has been marked as obsolete. As a consequence, when platformio is compiled with the enviroment set as above, the required framework is unable to be installed automatically.
- To solve this, you need to manually add this framework to the PIO core. 
  - Download the zip from the [link](https://github.com/platformio/platformio-pkg-framework-arduinosam/releases/tag/v4.3.190711).
  - Unzip the archive and place the unzipped folder in  your platformIO core folder. The location should be equivalent to  `C:\Users\<user_name>\.platformio\packages` path on windows.
  - After downloading and adding the extracted flder, the `packages` folder should look something like 
    - ![image](https://user-images.githubusercontent.com/31810812/213038179-a7ab0464-981e-430b-8a27-dcd52884b578.png)
- Once the framework is added, you should be able to build from source using platformIO!

- ESP board should be downloaded automatically when building the project for the first time.
  - [ToDo]: Set the board version we are recommending to use.


#### Download required dependencies
1. You should download all the required libraries using the steps [mentioned above](#install-firmware-libraries)
(using Arduino IDE).
2. All the libraries should be added to the `Documents/Arduino/libraries` folder.

**Note**: Make sure that after the libraies have been downloaded, the following directory structure is maintained.
```
Arduino/libraries
    |-- EmotiBit Feather Wing
    |   |-- EmotiBit_stock_firmware
    |       |-- EmotiBit_stock_firmware.ino
    |       |-- platformio.ini
    |   |-- EmotiBit_stock_firmware_100Hz_PPG
    |       |-- platformio.ini
    |-- EmotiBit MAX30101
    |-- EmotiBit XPlat Utils
    |-- EmotiBit BMI160
    |-- [dependency_library1]
    |-- [dependency_library2]
```

#### Building the project
- For detailed instructions, check out the [platformIO website](https://docs.platformio.org/en/latest/home/index.html) to open the PIO extension in VS-Code.
- Brief instructions:
  - Open Visual Studio Code and navigate to the PlatformIO home page.
  - On the hokme page, click on `Open Project`.
    - <img src="./assets/platformio_open_project.png" width="1000">
  - Navigate to the platformIO ini file.
    - `Documents/Arduino/libraries/EmotiBit_FeatherWing/EmotiBit_FeatherWing/EmotiBit_stock_firmware/platformio.ini `

```diff
-- Note: Do not close or try to open the project immediately after opening it the first time. Opening the project takes some time.
Trying to re-open a project before the first attempt is finished creates build issues leater on.
Unfortunately, PIO does not show a "progress screen" while initializing the project.
As a hack, you can try to switch between the PIO panes (on the left. `Project`, `Inspect`, `Libraries` etc.)
If the initialization is complete, returning to `Projects` pane will show the new project you just started.
```
- Once the project is loaded in PIO, you can open it in your workspace.
- The project has already been setup for use, so you can simply click on the build button to create the firmware binary.
  - Check out the [platformIO documentation](https://docs.platformio.org/en/latest/tutorials/espressif32/arduino_debugging_unit_testing.html#compiling-and-uploading-the-firmware) to learning more about build/upload/debug options. 



[comment]: <> (Add links to images below)

[arduino_chooseExample]: ./assets/arduino-choose_emotibit_example.png
[arduino_choosePort]: ./assets/arduino-uploading_FW.png
[arduino_upload_button]: ./assets/Arduino_upload_button.png
