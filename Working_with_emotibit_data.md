# Working with EmotiBit Data

# Table of Contents
- [Overview](#Overview)
- [EmotiBit Oscilloscope](#EmotiBit-Oscilloscope)
  - [Using EmotiBit Oscilloscope to Record Data](#Using-EmotiBit-Oscilloscope-to-Record-Data)
    - [Active recording session indicator](#Active-recording-session-indicator)
  - [EmotiBit Oscilloscope features](#EmotiBit-Oscilloscope-features)
  - [Settings files location](#Settings-files-location)
  - [EmotiBit Oscilloscope network settings](#EmotiBit-Oscilloscope-network-settings)
  - [Using LSL with EmotiBit Oscilloscope](#Using-LSL-with-EmotiBit-Oscilloscope)
    - [LSL output](#LSL-output)
    - [Timesync with LSL using marker stream](#Timesync-with-LSL-using-marker-stream)
  - [EmotiBit Oscilloscope display settings](#EmotiBit-Oscilloscope-display-settings)
- [EmotiBit DataParser](#EmotiBit-DataParser)
  - [Parse raw data using EmotiBit DataParser](#Parse-raw-data-using-EmotiBit-DataParser)
    - [Transfer file from SD-Card to computer](#Transfer-file-from-SD-Card-to-computer)
    - [Parse raw data file](#Parse-raw-data-file)
    - [Raw data format](#Raw-data-format)
    - [Parsed data file format](#Parsed-data-file-format)
    - [Parsing EmotiBit timestamps to LSL time](#Parsing-EmotiBit-timestamps-to-LSL-time)
    - [Batch Parsing](#Batch-parsing)
    - [A note on Timesyncs](#A-note-on-Timesyncs)
  - [EmotiBit file types](#EmotiBit-file-types)
  - [EmotiBit data types](#EmotiBit-data-types) 
    - [Data type sampling rates](#Data-type-sampling-rates)
- [Visualize parsed data](#Visualize-parsed-data)
  - [Visualization tools](#Visualization-tools)
- [Next steps](#Next-steps)

> [!IMPORTANT]
> If you are reading this page, it means you have already successfully streamed data from your EmotiBit hardware to the EmotiBit Oscilloscope. 
If you have not yet successfully streamed data or if you need help with the initial setup, please head back to the [**Getting Started**](./Getting_Started.md) page before proceeding with this document.

# How to Use EmotiBit

Getting reliable biometric data depends heavily on how the EmotiBit is positioned and secured.

### Placement on the Body

For optimal data collection, position the EmotiBit on the body according to these guidelines:
* Check out this blog post: https://www.emotibit.com/sensing-bio-metrics-from-anywhere-on-the-body/
* **Securing the Device:** Use the provided strap to secure the device. It should be snug enough to prevent shifting during movement, but not so tight that it restricts blood flow or causes discomfort.

> [!TIP]
> The EmotiBit has slots for straps on all 4 sides. This enables you to strap the EmotiBit in both orientations.

### How to Verify a Good Placement

Once the EmotiBit is secured, look at the live stream in the EmotiBit Oscilloscope to verify that the placement is correct and yielding high-quality data.

# The Data Ecosystem

Understanding the relationship between the physical sensors, the signals they generate, and how they are structured is key to successfully analyzing EmotiBit data.

## Sensors and Signals

Each data type represents a unique signal captured by EmotiBit and is represented by a unique `TypeTag`. The most up-to-date list of TypeTags can always be found in the [EmotiBit Packet Repository](https://github.com/EmotiBit/EmotiBit_XPlat_Utils/blob/master/src/EmotiBitPacket.cpp).

Below is a quick reference guide for the available data types. This table is updated periodically as the EmotiBit firmware grows. 

> [!TIP]
>  Additional details about the data stream (*such as units, sampling rate, data format, and averaging*) can be found in the `_info.json` file created automatically with each recording session.

| TypeTag | Signal & Description | How a Good Signal Looks | How a Bad Signal Looks |
| :---: | :--- | :--- | :--- |
| **EA** | **EDA** - Electrodermal Activity | | |
| **PI**<br>**PR**<br>**PG** | **PPG Infrared**<br>**PPG Red**<br>**PPG Green** | | |
| **T1** | **Temperature** | | |
| **TH** | **Temperature via Medical-grade Thermopile** *(EmotiBit MD only)* | | |
| **AX, AY, AZ** | **Accelerometer** (X, Y, Z axes) | | |
| **GX, GY, GZ** | **Gyroscope** (X, Y, Z axes) | | |
| **MX, MY, MZ** | **Magnetometer** (X, Y, Z axes) | | |
| **SA**<br>**SR**<br>**SF** | **SCR Amplitude** (Skin Conductance Response)<br>**SCR Rise Time**<br>**SCR Frequency** | | |
| **HR**<br>**BI** | **Heart Rate**<br>**Heart Inter-beat Interval** | | |

## Data type sampling rates
The following table shows the sampling rates at which the sensors operate with the stock EmotiBit firmware. You can also find a link to each sensor datasheet.

| Function |Data Type| Sensor IC | Sampling Rate (samples per second)|
|----------|---------|-----------|--------------|
| Motion   |`AX` `AY` `AZ` `GX` `GY` `GZ` `MX` `MY` `MZ`|[BMI160](https://www.bosch-sensortec.com/products/motion-sensors/imus/bmi160/)+[BMI150](https://www.bosch-sensortec.com/products/motion-sensors/magnetometers/bmm150/)|25|
|PPG |`PI` `PG` `PR`| [MAX30101](https://www.analog.com/en/products/max30101.html)|25|
|Temperature |`T0` / `TH`|[MAX30101](https://www.analog.com/en/products/max30101.html) / [MLX90632](https://www.melexis.com/en/product/MLX90632/Miniature-SMD-Infrared-Thermometer-IC) |7.5|
|EDA|`EA` `EL` `ER`|[ADS1114](https://www.ti.com/product/ADS1114)|15|

## Expected Data Format

### Local SD Card data format
> [!IMPORTANT]
> You need to start a recording session using the EmotiBit Oscilloscope to record data and store it locally on the SD Card.
```
531386,17296,1,RB,1,100,2024-09-18_22-59-45-827135
531388,17297,4,EM,1,100,RS,RB,2024-09-18_22-59-45-827135.csv,PS,MN
531473,17298,3,PI,1,100,112870,112866,112867
531473,17299,3,PR,1,100,26870,26855,26857
531473,17300,3,PG,1,100,3720,3704,3717
```
`EMOTIBIT_TIMESTAMP`,`PACKET#`,`NUM_DATAPOINTS`,`TYPETAG`,`VERSION`,`RELIABILITY`,`PAYLOAD`
- `EMOTIBIT_TIMESTAMP`: milliseconds since EmotiBit bootup
- `PACKET#`: sequentially increasing packet count
- `NUM_DATAPOINTS`: Number of data points in the payload
- `TYPETAG`: [type of data](#sensors-and-signals) being sent
- `VERSION`: packet protocol version
- `RELIABILITY`: data reliability score out of 100 (for future use)
- `PAYLOAD`: data points

<details><summary><b>Sample raw data file</b></summary>
    
    ```
    531386,17296,1,RB,1,100,2024-09-18_22-59-45-827135
    531388,17297,4,EM,1,100,RS,RB,2024-09-18_22-59-45-827135.csv,PS,MN
    531473,17298,3,PI,1,100,112870,112866,112867
    531473,17299,3,PR,1,100,26870,26855,26857
    531473,17300,3,PG,1,100,3720,3704,3717
    531459,17301,2,EA,1,100,0.030269,0.030269
    531459,17302,2,EL,1,100,26425.000000,26425.000000
    531452,17303,1,T1,1,100,33.037
    531467,17304,1,TH,1,100,29.770
    531473,17305,3,AX,1,100,-0.436,-0.434,-0.433
    531473,17306,3,AY,1,100,-0.015,-0.015,-0.015
    531473,17307,3,AZ,1,100,0.967,0.968,0.970
    531473,17308,3,GX,1,100,-0.275,-0.244,-0.275
    531473,17309,3,GY,1,100,0.732,0.793,0.732
    531473,17310,3,GZ,1,100,-0.061,-0.061,-0.092
    531473,17311,3,MX,1,100,37,38,37
    531473,17312,3,MY,1,100,-56,-57,-56
    531473,17313,3,MZ,1,100,-56,-56,-57
    ```
</details>

### Parsed Data File Format
> [!IMPORTANT]
> You need to run the EmotiBit Data Parser to convert raw data recordings into parsed files. See the DataParser section to learn more about how to use the EmotiBit Data Parser.
```
LocalTimestamp,EmotiBitTimestamp,PacketNumber,DataLength,TypeTag,ProtocolVersion,DataReliability,PI
1781122022.609306,565464.000,24431,3,PI,1,100,169093
1781122022.609306,565464.000,24431,3,PI,1,100,169120
1781122022.609306,565464.000,24431,3,PI,1,100,169140
1781122022.649304,565504.000,24448,3,PI,1,100,169136
```
* `LocalTimestamp`: Epoch time in seconds
* `EmotiBitTimestamp`: EmotiBit time in milli-seconds (emotibit time resets everytime emotibit is rebooted)
* `PacketNumber`: Packet number the data point was extracted from (sequentially increases)
* `DataLength`: Number of data points in the packet
* `TypeTag`: TypeTag of the data (see table above)
* `ProtocolVersion`: Reserved for future extensibility
* `DataReliability`: Reserved for future extensibility
* `Data`: Sinlge data-point

# Accessing EmotiBit Data
EmotiBit offers two distinct methodologies to capture your data.
Both methods utilize the **EmotiBit Oscilloscope** application as a core tool. Therefore, this is the perfect spot to briefly introduce how to interact with the Oscilloscope before setting up your first recording session.

### EmotiBit Oscilloscope: The Basics

The EmotiBit Oscilloscope is your central hub for monitoring data quality and device status in real-time.

1. <details><summary>Connecting to EmotiBit</summary>

      - The Oscilloscope displays all available EmotiBits on the network in the `EmotiBit Device List`.  
      - You can click on any EmotiBit in the list to connect to it. 
   </details>

2. <details><summary>Streaming real-time Data</summary>

      - The moment you connect to an EmotiBit, the EmotiBit Ocsilloscope will display the data being transmitted by the EmotiBit.
      - Once a connection between the Oscilloscope and EmotiBit has been established, the EmotiBit Blue LED turns ON.
        - The EmotiBit Blue LED stays on as long as the EmotiBit is connected to an Oscilloscope. 
   </details>

3. <details><summary>Recording Data</summary>

      - Select an EmotiBit from the list of available EmotiBits.
      - You can initiate a record session by clicking on the record button. When a record session is initiated, the EmotiBit will start recording the data on the onboard SD-Card as well as stream it on the Oscilloscope.
        - The EmotiBit Red LED starts blinking once a recording session has been initiated.
      - You are free to move in/out of the network, close the Oscilloscope, or connect to a new Oscilloscope.
      - We recommend using the EmotiBit in-network as much as possible, connected to the Oscilloscope. This helps in generating more time-syncs which improves timestamp accuracy.
   </details>

### 1. Record data on the SD-Card

To start a record session, follow these steps:
- Select the EmotiBit from the `EmotiBit Device List`.
  - If you have multiple EmotiBits on the network, select the EmotiBit you want to record data from.
- Once an EmotiBit is selected, the Oscilloscope starts streaming data.
- Click on the `Record Button` on the top console on the Oscillscope.
- Once a recording session has been started, the `Record Button` section becomes red.
- To end a recording, toggle the Recording button by clicking on it again.

> [!TIP]
> **Active recording session indicator:** You can check if a recording session is currently active by either checking the EmotiBit or the EmotiBit Oscilloscope.<br>
> - **Indication on the EmotiBit**
>   - You will notice that the EmotiBit RED LED starts blinking if a recording session is active.
>   - The EmotiBit RED LED will continue to blink till the active recording session has been stopped using the EmotiBit Oscillosocpe.
> - **Indication on the EmotiBit Oscilloscope**
>   - When you open the Oscilloscope, all available EmotiBits on the network will be listed under the `device list`. Select the EmotiBit you are interested in from the device list.
>   - If a recording session is currently active, the name of the file being recorded appears below the `Record Button`. This name indicates the time when the recording was started. The Record button and the file name appear with a red background.


### 2. Stream data to another location (Using Output List)

- The output list shows the options available to transmit the data out of the EmotiBit Oscilloscope.
- Each output protocol uses settings specified in the unique file name.
- The available output options are
  - OSC
  - UDP
  - LSL

***************************OLD DOCUMENT STARTS HERE
---



# EmotiBit file types
There are 3 types of files associated with EmotiBit
- Raw data file(**csv**)
  - Every recording sessions generates 1 raw data file.
  - This file is named with the start time of the recording session. Ex: `2019-01-30_11-57-13-492.csv`
- Information file(**json**)
  - Along with the raw data file, each recording session generates 1 `info` file.
  - It contains information like sampling rates and other important settings for each sensor/stream.
  - It shares the name of the raw file. For example, the `info` file for the above raw file will be named `2019-01-30_11-57-13-492_info.json`
  - <details><summary>sample _info.json file</summary>

    ```
    [{
    "info": {
        "name": "EmotiBitData",
        "type": "Multimodal",
        "source_id": "EmotiBit FeatherWing",
        "hardware_version": "V05c",
        "sku": "MD",
        "device_id": "MD-V5-0000410",
        "feather_version": "Adafruit Feather HUZZAH32",
        "feather_wifi_mac_addr": "54:66:cc:7e:dc:0c",
        "firmware_version": "1.12.1",
        "firmware_variant": "EmotiBit_stock_firmware",
        "created_at": "2024-11-14_11-54-36-135729"
    }
    }, {
    "info": {
        "name": "Accelerometer",
        "type": "Accelerometer",
        "typeTags": ["AX", "AY", "AZ"],
        "channel_count": 3,
        "nominal_srate": 25,
        "channel_format": "float",
        "units": "g",
        "setup": {
            "range": 8,
            "acc_bwp": 2,
            "acc_us": 2
        }
    }
    }, {
    "info": {
        "name": "Gyroscope",
        "type": "Gyroscope",
        "typeTags": ["GX", "GY", "GZ"],
        "channel_count": 3,
        "nominal_srate": 25,
        "channel_format": "float",
        "units": "degrees/second",
        "setup": {
            "range": 1000,
            "gyr_bwp": 2,
            "gyr_us": 2
        }
    }
    }, {
    "info": {
        "name": "Magnetometer",
        "type": "Magnetometer",
        "typeTags": ["MX", "MY", "MZ"],
        "channel_count": 3,
        "nominal_srate": 25,
        "channel_format": "float",
        "units": "microhenries",
        "setup": {}
    }
    }, {
    "info": {
        "name": "ElectrodermalActivity",
        "type": "ElectrodermalActivity",
        "typeTags": ["EA"],
        "channel_count": 1,
        "nominal_srate": 15,
        "channel_format": "float",
        "units": "microsiemens",
        "setup": {
            "eda_series_resistance": 0,
            "adc_bits": 16,
            "enable_digital_filter": false,
            "samples_averaged": 5,
            "oversampling_rate": 75,
            "eda_transform_slope": 722.0528564,
            "eda_transform_intercept": 1.4121972e7
        }
    }
    }, {
    "info": {
        "name": "SkinConductanceResponseAmplitude",
        "type": "ElectrodermalActivity",
        "typeTags": ["SA"],
        "channel_count": 1,
        "channel_format": "float",
        "units": "microsiemens"
    }
    }, {
    "info": {
        "name": "SkinConductanceResponseFrequency",
        "type": "ElectrodermalActivity",
        "typeTags": ["SF"],
        "channel_count": 1,
        "nominal_srate": 3,
        "channel_format": "float",
        "units": "count/min"
    }
    }, {
    "info": {
        "name": "SkinConductanceResponseRiseTime",
        "type": "ElectrodermalActivity",
        "typeTags": ["SR"],
        "channel_count": 1,
        "channel_format": "float",
        "units": "secs"
    }
    }, {
    "info": {
        "name": "Temperature1",
        "type": "Temperature",
        "typeTags": ["T1"],
        "channel_count": 1,
        "nominal_srate": 7.5,
        "channel_format": "float",
        "units": "degrees celcius",
        "sensor_part_number": "MAX30101",
        "setup": {
            "samples_averaged": 1,
            "oversampling_rate": 7.5
        }
    }
    }, {
    "info": {
        "name": "Thermopile",
        "type": "Temperature",
        "typeTags": ["TH"],
        "channel_count": 1,
        "nominal_srate": 7.5,
        "channel_format": "float",
        "units": "degrees celcius",
        "setup": {
            "samples_averaged": 1,
            "oversampling_rate": 7.5
        }
    }
    }, {
    "info": {
        "name": "PPG",
        "type": "PPG",
        "typeTags": ["PI", "PR", "PG"],
        "channel_count": 3,
        "nominal_srate": 25,
        "channel_format": "float",
        "units": "raw units",
        "setup": {
            "LED_power_level": 47,
            "samples_averaged": 16,
            "LED_mode": 3,
            "oversampling_rate": 400,
            "pulse_width": 215,
            "ADC_range": 4096
        }
    }
    }, {
    "info": {
        "name": "HeartRate",
        "type": "PPG",
        "typeTags": ["HR"],
        "channel_count": 1,
        "channel_format": "int",
        "units": "bpm"
    }
    }, {
    "info": {
        "name": "InterBeatInterval",
        "type": "PPG",
        "typeTags": ["BI"],
        "channel_count": 1,
        "channel_format": "float",
        "units": "mS"
    }
    }]
    ```
    </details>
	
- Parsed data files(**csv**)
  - the raw file is converted to parsed files by running the DataParser.
  - Each parsed file contains data for a specific data type.
  - The name for each parsed file is created by joining the `TypeTag` of the data type to the raw file name.
    - Ex: After running the data parser on `2019-01-30_11-57-13-492.csv`, the parsed data file containing the data for `PPG IR channel` 
    will be called `2019-01-30_11-57-13-492_PI.csv`
    - For more details on data types, see [EmotiBit Data Types](#emotibit-data-types) (below).

![][EmotiBit-File-Types]


# EmotiBit data types
Each data type represents a unique signal captured by EmotiBit and is represented by a unique `TypeTag`. The most up-to-date list of TypeTags can be found in https://github.com/EmotiBit/EmotiBit_XPlat_Utils/blob/master/src/EmotiBitPacket.cpp

For a quick look at the available data types, you can check out the table below. We periodically update this table as the EmotiBit firmware grows. **Additional details about the data stream (*units, sampling rate, data format, averaging etc*) can be found in the `_info.json` file created with each recording session.**

- <details open><summary><b>Biometric TypeTags</b></summary>

  |TypeTag    | Description          |
  |:-----:|----------------------|
  |EA     |EDA- Electrodermal Activity  |
  |EL     |EDL- Electrodermal Level     |
  |ER     |EDR- Electrodermal Response (EmotiBit V4+ combines ER into EA signal)  |
  |PI     |PPG Infrared          |
  |PR     |PPG Red               |
  |PG     |PPG Green             |
  |T0     |Temperature (only on EmotiBit Alpha/Beta V1, V2, V3)         |
  |T1     |Temperature          |
  |TH     |Temperature via Medical-grade Thermopile (only on EmotiBit MD)   |
  |AX     |Accelerometer X       |
  |AY     |Accelerometer Y       |
  |AZ     |Accelerometer Z       |
  |GX     |Gyroscope X           |
  |GY     |Gyroscope Y           |
  |GZ     |Gyroscope Z           |
  |MX     |Magnetometer X        |
  |MY     |Magnetometer Y        |
  |MZ     |Magnetometer Z        |
  |SA     |Skin Conductance Response (SCR) Amplitude        |
  |SR     |Skin Conductance Response (SCR) Rise Time |
  |SF     |Skin Conductance Response (SCR) Frequency |
  |HR     |Heart Rate        |
  |BI     |Heart Inter-beat Interval        |
  |H0     |Humidity (only on EmotiBit Alpha/Beta V1, V2, V3)     |

  </details>

- <details><summary><b>General Typetags</b></summary>

  |TypeTag    | Description                       |
  |:-----:|:----------------------------------|
  |EI     |EmotiBit Info Json                 |
  |DC     |Data Clipping, TypeTag in Payload  |
  |DO     |Data Overflow, TypeTag in Payload  |
  |B%     |Battery Percentage Remaining       |
  |BV     |Battery Voltage                    |
  |D%     |SD card percent capacity filled    |
  |RD     |Request Data, TypeTag in Payload   |
  |PI     |Ping                               |
  |PO     |Pong                               |
  |RS     |Reset                              |

  </details>

- <details><summary><b>Computer to EmotiBit TypeTags</b></summary>

  |TypeTag    | Description                       |
  |:-----:|:----------------------------------|
  |GL     |[GPS latitude and Longitude][GPS]  |
  |GS     |[GPS Speed][GPS]                   |
  |GB     |[GPS Bearing][GPS]                 |
  |GA     |[GPS Altitude][GPS]                |
  |TL     |Local Computer Timestamp           |
  |TU     |UTC Timestamp                      |
  |TX     |Crosstime, used for timestamp comparison   |
  |LM     |LSL Marker/message                 |
  |RB     |Record begin (Include timestamp in Data)   |
  |RE     |Record End                         |
  |UN     |User Note                          |
  |MH     |Mode Hibernate                     |
  |HE     |Hello EmotiBit, used to establish communication  |

  </details>

- <details><summary><b>Payload labels</b></summary>

  |TypeTag    | Description                       |
  |:-----:|:----------------------------------|
  |LM     |LSL_MARKER_SRC_TIMESTAMP - The LSL time in the marker generator system |
  |LR     |LSL_MARKER_RX_TIMESTAMP - The LSL time in the receiver system. This is a calculated value derived from LM and time correction (a constant created by the LSL architecture)  |
  |LD     |LSL_MARKER_DATA - the data stored by the LSL marker|
  |LC     |LSL_LOCAL_CLOCK_TIMESTAMP - The LSL time on the local computer the EmotiBit Oscilloscope is running on|

  </details>

# Visualize parsed data
Visualization tools can often help answer some immediate questions and hence, can be very useful when working with time-series data. Below we have outlined a number of tools that we think can be very successful.
## Visualization tools
- Text Editors
  - Notepad++(on Windows)
  - Text Edit(on mac)
- Spreadsheet softwares
  - Microsoft Excel
  - Google Sheets 
- [EmotiBit python data viewer](https://github.com/EmotiBit/EmotiBit_Biometric_Lib/tree/master/py/examples/dataviewer_example)
  - A tool created for visualizing all data channels in one window. 
  - ![][EmotiBit-PythonDataViewer]


[EmotiBit-Oscilloscope]: ./assets/Visualizer_green_800px.gif "EmotiBit-Oscilloscope"
[EmotiBit-File-Types]: ./assets/EmotiBit_File_Types.png "EmotiBit-File-Types"
[EmotiBit-DataParser]: ./assets/DataParser.png "EmotiBit-Dataparser"
[EmotiBit-PythonDataViewer]: ./assets/PythonDataViewer.jpg "EmotiBit-PythonDataViewer"
