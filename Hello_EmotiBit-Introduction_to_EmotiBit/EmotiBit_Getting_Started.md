# Getting Started with EmotiBit
![alt text][SideView]
![alt text][GUI]

## Table of Contents
- [Overview](#overview)
- [If you just received your EmotiBit](#If-you-just-received-your-EmotiBit)
- [Connecting To WiFi](#connecting-to-wifi)
- [LED Indicators](#LED-Indicators)
- [Switches](#switches)
- [Maintenance](#maintenance)
- [Data Recording](#data-recording)
  - [SD Saves](#sd-saves)
  - [Data AutoSave](#Data-AutoSave)
- [Developing with Visual Studio + Visual Micro](#developing-with-visual-studio--visual-micro)
- [Debugging](#debugging)
- [Repositories](#repositories)

## Overview

![alt text][Hardware]

## If you just received your EmotiBit
- Welcome to the World of EmotiBit. If you just received your EmotiBit, In the box you will find:
  - EmotiBit
  - Adafruit feather M0 WiFi, programmed and ready to use
  - Micro-SD-Card
  - Micro SD-Card USB reader
  - 3.7V battery
- To get started, follow the instructions below([connecting to WiFi](#connecting-to-wifi)) to set-up your SD-Card, so that the EmotiBit can connect to Wifi
- After your SD-Card is setup and ready for use, insert it into the EmotiBit SD-Card slot. At this Point, your EmotiBit is ready to use!
- To start using teh EmotiBit, you will also need the Oscilloscope designed for the EmotiBit. Click [here](https://github.com/EmotiBit/ofxEmotiBit/releases) to get the Oscilloscope installed.
  - Download the precompiled binaries for the EmotiBit Oscilloscope(`EmotiBitOscilloscope.zip`) and the dataParser(`EmotiBitDataParser.zip`).
  - Extract the .zip files downloaded. You will find a `EmotiBitOscilloscope.exe` in the `bin` folder.
  - You are GOOD TO GO!
- Plug in the 3.7V battery provided with the EmotiBit. We recommend that you plug in the Micro-USB cable too, as this will begin recharging the battery, which will be indicated by the YELLOW light on the Adafruit Feather.
- Wait for the EmotiBit to run through the setup.
- Double click on the `EmotiBitOscilloscope.exe`, downloaded in the previous step.
- You should see the Data start to stream on the Oscilloscope!
- You do not see anything on the Oscilloscope? Click [here](guide-to-trouble-shooting) to check out our guide for trouble Shooting

### Connecting to WiFi
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

## LED Indicators

- **LED's on the EmotiBit:** As shown in the Images above, The EmotiBit has 3 LED's(Users should look at these when Determining the EmotiBit state)
      
| Event | Indicator LED State | Approx. Freq.  |
| ------------- |:-------------------:| --------------:|
| Recording     | RED - Slow Blink    | 1 Hz           |
| Active - Not Recording | BLUE - Steady blink | 15 Hz          |
| Low Battery   | YELLOW - Blinking   | 2 Hz           |

<details>
<summary>LED's on the Adafruit Feather M0 WiFi:</summary>
<br>

![alt text][LED]

- **LED's on the Adafruit Feather M0 WiFi:** As shown in the Images above, The Feather has 4 LED's(Users should not look into these LED's unless debugging a problem)
  - RED: Is the I2C CLK Line. Under regular Operation, it should be always ON
  - ORANGE: This is the Charging indicator, which glows if a battery is connected to the feather and is being charged by the USB connection
  - GREEN: This is the WiFi indicator. If the EmotiBit is Connected to Wifi, there should be a constant glow.
  - YELLOW: It blinks whenever the EmotiBit receives data from the computer.
</details>

## Switches
- EmotiBit Switch/Button: _adjacent to the SD card_
  - Long Press (3 sec) to put EmotiBit into hibernate mode
  - Short Press- Switch between WiFi modes. In future will support mapping to different functionality.
- Reset switch on the feather resets the board and restarts the code

## Maintenance
- As the SD card fills up, it can slow down data writing to the SD card. To keep the EmotiBit running at peak performance, it’s a good idea to clear files off the SD card periodically.

## For Advanced Users(If you want to dive into the inner workings of EmotiBit)
- We have designed the EmotiBit to be built on an Open Source Architecture. 
- The Following links will guide you to the internal workings of the EmotiBit
  - [Packet Architecture](Link to the Documentation of the inner workings)
  - [Networking Architecture](Link to the Netwroking Architecture) 


## Data Recording
Recording must be initiated from the [GUI](https://github.com/EmotiBit/ofxEmotiBit/releases), which is also the recommended way to view incoming data streams. The EmotiBit must be connected to the same WiFi as your computer for the GUI to work. No internet connection is neccessary.

##### SD Saves
- CSV: Experimental Data
  - All data is saved to the SD card into a .csv file when recording is initiated from the GUI
  - The file is named with the date-time that the recording started
    -   An example file name can be `2019-01-30_11-57-13-492.csv`
- JSON: Configuration Settings
  - Information about the configuration of the hardware and firmware are written to a .json file also on the SD card
  - The file is named with the date-time that the recording started
    - 2019-01-30_11-57-13-492_info.json
    
```
[{"info":{"name":"Accelerometer","type":"Accelerometer","typeTags":["AX","AY","AZ"],"channel_count":3,"nominal_srate":60,"channel_format":"float","units":"G/second","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"range":8}}},{"info":{"name":"Gyroscope","type":"Gyroscope","typeTags":["GX","GY","GZ"],"channel_count":3,"nominal_srate":60,"channel_format":"float","units":"degrees/second","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"range":1000}}},{"info":{"name":"Magnetometer","type":"Magnetometer","typeTags":["MX","MY","MZ"],"channel_count":3,"nominal_srate":60,"channel_format":"float","units":"raw samples","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{}}},{"info":{"name":"ElectrodermalActivity","type":"ElectrodermalActivity","typeTags":["EA"],"channel_count":1,"nominal_srate":15,"channel_format":"float","units":"microsiemens","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"adc_bits":12,"voltage_divider_resistance":5000000,"EDR_amplification":20,"low_pass_filter_frequency":"15.91Hz","samples_averaged":4,"oversampling_rate":60}}},{"info":{"name":"Humidity0","type":"Humidity","typeTags":["H0"],"channel_count":1,"nominal_srate":7,"channel_format":"float","units":"Percent","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"resolution":"RESOLUTION_H11_T11","samples_averaged":2,"oversampling_rate":15}}},{"info":{"name":"Temperature0","type":"Temperature","typeTags":["T0"],"channel_count":1,"nominal_srate":7,"channel_format":"float","units":"degrees celcius","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"resolution":"RESOLUTION_H11_T11","samples_averaged":2,"oversampling_rate":15}}},{"info":{"name":"Thermistor","type":"Thermistor","typeTags":["TH"],"channel_count":1,"nominal_srate":7,"channel_format":"float","units":"raw adc units","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"ADC_speed":"ADC_NORMAL","Vin_buffering":"VIN_UNBUFFERED","VREFP":"VREFP_VDDA","voltage_divider_resistance":10000,"thermistor_resistance":10000,"low_pass_filter_frequency":"0.1591Hz","amplification":10,"samples_averaged":2,"oversampling_rate":15}}},{"info":{"name":"PPG","type":"PPG","typeTags":["PI","PR","PG"],"channel_count":3,"nominal_srate":25,"channel_format":"float","units":"raw units","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"LED_power_level":47,"samples_averaged":16,"LED_mode":3,"oversampling_rate":400,"pulse_width":215,"ADC_range":4096}}}]
```

##### Data AutoSave
- Even if the EmotiBit is not recording, the data received by the Oscilloscope is saving the data on the system as described below.
- GUI data can be found in EmotiBitOscilloscope\bin\data
  - dataLog.txt
    - Contains the experimental data recieved by the GUI
    - Same packet format as the SD save
  - consoleLog.txt
    - can be used as a psuedo serial monitor during the recording instead of Serial.print()
- **NOTE: wWe recommend not editing any files(except the `dataLog.txt` and `consoleLog.txt`) in the `EmotiBitOscilloscope\bin\data` folder. These files are necessary for the functioning of the Oscilloscope.**

## Developing with Visual Studio + Visual Micro
- Follow instructions in [Setup](#setup) to get the Arduino IDE and libraries
- [Install Visual Studio 2017 Community](https://drive.google.com/open?id=1sWMwa3cjDe1rPv4zH8XExWo41-AKcl3G)
- Install the [Visual Micro extension for Visual Studio](https://www.visualmicro.com/page/Arduino-Visual-Studio-Downloads.aspx)
- Manually add the link for additional board links given in the Setup
  - https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
- Manually add the Adafruit SAMD libraries and the Arduino SAMD libraries via:
  - vMicro->Add Library->Download and Install Arduino Library->Manage Boards
- Follow instructions in Programming the Feather 
  - Select proper board and port
  - Rapid double click reset button on the feather to put it into programming mode
  - Compile and run
  - Open Serial monitor or Oscilloscope to view data stream

## Debugging
- [LED's](#adafruit-feather-m0-led-indicators) and the serial monitor can be useful tools for debugging
- if the green _WiFi Connected_ LED is on, the feather is connected to WiFi
- if the yellow _Network Traffic_ LED flashes at all, it suggests that the EmotiBit is exchanging packets with ofxEmotiBit
- **The following 3 points have to be redefined for Beta boards**
- if the red LED goes on after uploading code and remains on indefinitely without the green  _WiFi Connected_ LED, then the code is stuck in setup() before WiFi.begin() is ever called
  - Serial monitor should show which part of the board is failing to initialize
  - Differences in where the code gets stuck upon repeated uploads suggests that the boards have faulty connections
- if the red LED goes on after uploading the code and _**all LEDS**_ are off after 30-60 seconds, it is hibernating because it cannot connect to WiFi
  - Check the config.txt to make sure that the proper credentials were input
  - Check that your WiFi does not do MAC address filtering
  - Check that your feather has the [latest version of the firmware](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/updating-firmware)
  - Check that your network supports device connections in this manner; many Universities and public work spaces disallow it
- If the red light significantly deviates from the patterns shown in the [above section](#adafruit-feather-m0-led-indicators), including getting stuck on or off for a large period of time during recording, there is a firmware error that is causing _loop()_ to delay. Check any changes that you made to the release code. Remove any while loops that take more than 15ms.

## Repositories
- Parent Github
  - https://github.com/EmotiBit/
- Android App
  - https://github.com/EmotiBit/EmotiBit_Android_App/
- Firmware
  - https://github.com/EmotiBit/EmotiBit_FW_FeatherWing
  - Latest release: https://github.com/EmotiBit/EmotiBit_FW_FeatherWing/releases
- OpenFrameworks GUI
  - https://github.com/EmotiBit/ofxEmotiBit
  - Latest release: https://github.com/EmotiBit/ofxEmotiBit/releases

[GUI]: https://github.com/EmotiBit/EmotiBit_Docs/blob/master/images/ofxEmotiBit.png "ofxEmotiBit GUI"
[Hardware]: https://github.com/EmotiBit/EmotiBit_Docs/blob/master/images/hardwarewithback.png "EmotiBit Hardware"
[SideView]: https://github.com/EmotiBit/EmotiBit_Docs/blob/master/images/EmotiBitSideView.jpg "EmotiBit Side View"
[LED]: https://github.com/EmotiBit/EmotiBit_Docs/blob/master/images/LightIndicators.png "Feather LED's"

