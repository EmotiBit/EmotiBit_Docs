# Getting Started with EmotiBit
![alt text][SideView]
![alt text][GUI]

## Table of Contents
- [Overview](#overview)
- [Setup](#setup)
- [Programming the Feather](#programming-the-feather)
- [Connecting To WiFi](#connecting-to-wifi)
- [Adafruit Feather M0 LED Indicators](#adafruit-feather-m0-led-indicators)
- [Switches](#switches)
- [Maintenance](#maintenance)
- [Packet Format](#packet-format)
  - [TypeTag Character Codes](#typetag-character-codes)
    - [Biometric TypeTags](#biometric-typetags)
    - [General TypeTags](#general-typetags)
    - [Computer to EmotiBit TypeTags](#computer-to-emotibit-typetags)
- [Data Recording](#data-recording)
  - [SD Saves](#sd-saves)
  - [GUI Saves](#gui-saves)
- [Developing with Visual Studio + Visual Micro](#developing-with-visual-studio--visual-micro)
- [Repositories](#repositories)

## Sensor Overview

![alt text][Hardware]

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
  - SparkFun_MAX3010x_Pulse_and_Proximity_Sensor_Library
  - EmotiBit Si7013
  - EmotiBit BMI160
  - EmotiBit FeatherWing

## Programming the Feather
- Get the latest release of EmotiBit_FW as described in [setup](#setup)
- in Arduino/libraries/EmotiBit_FeatherWing/examples/Emotibit_Example
  - Double click on the .ino file to open it in Arduino
- Choose Tools->Board->“Adafruit Feather M0”
- Put the Feather in programming mode by double clicking the reset button. You should see the red LED pulsing and the available port should change.
- Choose Tools>Port>[the correct port for your board]
- Click “Upload”

## Connecting to WiFi
- To connect to WiFi with an Adafruit Feather M0 Wifi board, you can add the WiFi credentials to a file named “config.txt” on the SD card.
- If this is done after programming, the Feather should be reset by pressing the reset botton. If it is done before programming, it should connect automatically. SD card reading is done in the setup of EmotiBit_Example.ino
- The contents of the file should be JSON in the following format: 
  - ``{"WifiCredentials": [{"ssid": "SSSS", "password" : "PPPP"}]}``
  
## Adafruit Feather M0 LED Indicators

| EmotiBit State| Indicator LED State | Approx. Freq.  |
| ------------- |:-------------------:| --------------:|
| Hibernating   | Very Slow Blink     | 0.067 Hz       |
| Recording     | Slow Blink          | 5 Hz           |
| Programing    | Fast Blink          | 15 Hz          |
| Not Recording | Slow Pulse          | 2 Hz           |

![alt text][LED]

## Switches
- EmotiBit Switch/Button: adjacent to the SD card
  - Long Press (3 sec) to put EmotiBit into hibernate mode
- Reset switch on the feather resets the board and restarts the code

## Maintenance
- As the SD card fills up, it can slow down data writing to the SD card. To keep the EmotiBit running at peak performance, it’s a good idea to clear files off the SD card periodically.

## Packet Format
- TIMESTAMP,PACKET#,#DATAPOINTS,TYPETAG,VERSION,RELIABILITY,PAYLOAD
  - Timestamp: milliseconds since start of EmotiBit
  - Packet Number: packet count since start of EmotiBit
  - Number of Datapoints: Number of data points in the payload
  - Typetag: type of data being sent
  - Version: version of packet protocol
  - Reliability: data reliability score out of 100, currently always 100
  - Payload: data to send
- Example Packets:

![alt text][Pack]
### TypeTag Character Codes

#### Biometric TypeTags
|Tag    | Description          |
|-------|----------------------|
|EA     |EDA                   |
|EL     |EDL                   |
|ER     |EDR                   |
|PI     |PPG Infrared          |
|PR     |PPG Red               |
|PG     |PPG Green             |
|T0     |Temperature (Si7013)  |
|TH     |Thermistor            |
|H1     |Humidity (Si7013)     |
|AX     |Accelerometer X       |
|AY     |Accelerometer Y       |
|AZ     |Accelerometer Z       |
|GX     |Gyroscope X           |
|GY     |Gyroscope Y           |
|GZ     |Gyroscope Z           |
|MX     |Magnetometer X        |
|MY     |Magnetometer Y        |
|MZ     |Magnetometer Z        |

#### General Typetags

#### Computer to EmotiBit TypeTags

## Data Recording
Recording must be initiated from the [GUI](https://github.com/EmotiBit/ofxEmotiBit/releases), which is also the recommended way to view incoming data streams. The EmotiBit must be connected to the same WiFi as your computer for the GUI to work. No internet connection is neccessary.

##### SD Saves
- CSV: Experimental Data
  - All data is saved to the SD card into a .csv file when recording is initiated from the GUI
  - The file is named with the date-time that the recording started
    -   2019-01-30_11-57-13-492.csv
- JSON: Configuration Settings
  - Information about the configuration of the hardware and firmware are written to a .json file also on the SD card
  - The file is named with the date-time that the recording started
    - 2019-01-30_11-57-13-492_info.json
    
```
[{"info":{"name":"Accelerometer","type":"Accelerometer","typeTags":["AX","AY","AZ"],"channel_count":3,"nominal_srate":60,"channel_format":"float","units":"G/second","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"range":8}}},{"info":{"name":"Gyroscope","type":"Gyroscope","typeTags":["GX","GY","GZ"],"channel_count":3,"nominal_srate":60,"channel_format":"float","units":"degrees/second","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"range":1000}}},{"info":{"name":"Magnetometer","type":"Magnetometer","typeTags":["MX","MY","MZ"],"channel_count":3,"nominal_srate":60,"channel_format":"float","units":"raw samples","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{}}},{"info":{"name":"ElectrodermalActivity","type":"ElectrodermalActivity","typeTags":["EA"],"channel_count":1,"nominal_srate":15,"channel_format":"float","units":"microsiemens","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"adc_bits":12,"voltage_divider_resistance":5000000,"EDR_amplification":20,"low_pass_filter_frequency":"15.91Hz","samples_averaged":4,"oversampling_rate":60}}},{"info":{"name":"Humidity0","type":"Humidity","typeTags":["H0"],"channel_count":1,"nominal_srate":7,"channel_format":"float","units":"Percent","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"resolution":"RESOLUTION_H11_T11","samples_averaged":2,"oversampling_rate":15}}},{"info":{"name":"Temperature0","type":"Temperature","typeTags":["T0"],"channel_count":1,"nominal_srate":7,"channel_format":"float","units":"degrees celcius","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"resolution":"RESOLUTION_H11_T11","samples_averaged":2,"oversampling_rate":15}}},{"info":{"name":"Thermistor","type":"Thermistor","typeTags":["TH"],"channel_count":1,"nominal_srate":7,"channel_format":"float","units":"raw adc units","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"ADC_speed":"ADC_NORMAL","Vin_buffering":"VIN_UNBUFFERED","VREFP":"VREFP_VDDA","voltage_divider_resistance":10000,"thermistor_resistance":10000,"low_pass_filter_frequency":"0.1591Hz","amplification":10,"samples_averaged":2,"oversampling_rate":15}}},{"info":{"name":"PPG","type":"PPG","typeTags":["PI","PR","PG"],"channel_count":3,"nominal_srate":25,"channel_format":"float","units":"raw units","source_id":"EmotiBit FeatherWing","hardware_version":0,"feather_version":"Adafruit Feather M0 WiFi","firmware_version":"0.4.3","created_at":"2019-07-17_14-38-30-914939","setup":{"LED_power_level":47,"samples_averaged":16,"LED_mode":3,"oversampling_rate":400,"pulse_width":215,"ADC_range":4096}}}]
```

##### GUI Saves
- GUI data can be found in EmotiBitOscilloscope\bin\data
- dataLog.txt
  - Contains the experimental data recieved by the GUI
  - Same packet format as the SD save
- consoleLog.txt
  - can be used as a psuedo serial monitor during the recording instead of Serial.print()

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
[Pack]: https://github.com/EmotiBit/EmotiBit_Docs/blob/master/images/PacketExample.png "Example Packets"
