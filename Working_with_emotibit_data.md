# Working with EmotiBit Data

# Table of Contents
- [Overview](#Overview)
- [EmotiBit Oscilloscope](#EmotiBit-Oscilloscope)
  - [Opening EmotiBit Oscilloscope](#Opening-EmotiBit-Oscilloscope)
  - [Using EmotiBit Oscilloscope](#Using-EmotiBit-Oscilloscope)
- [EmotiBit DataParser](#EmotiBit-DataParser)
  - [EmotiBit file types](#EmotiBit-file-types)
  - [EmotiBit data types](#EmotiBit-data-types)  
  - [Opening EmotiBit dataParser](#Opening-EmotiBit-dataParser)
  - [Using EmotiBit DataParser](#Using-EmotiBit-DataParser)
    - [Sampling rates](#Sampling-rates)
- [Visualize Recorded Data](#Visualize-Recorded-Data)
  - [Opening EmotiBit DataViewer](#Opening-EmotiBit-DataViewer)
  - [Visualization Tools](#Visualization-Tools)

# Overview
On this page we will talk about:
- [**EmotiBit Oscilloscope**](#Real-Time-Streaming): An intuitive and powerful tool to **live stream data** from any EmotiBit active on the Network. 
 You will also use this tool to initiate recording, Log Notes and access some other useful functions.
- [**EmotiBit DataParser**](#Next-Steps-Converting-Raw-Data): Reads the raw file(created with every record session) and create individual data files for each `dataType`.
- [**Data Visualization**](#Next-Steps-Visualize-Recorded-Data): Being able to visualize data helps in making intuitive sense of the data collected. We suggest some tools which we have found to be very useful in analyzing data and also introduce a tool we have created in python to visualize all data streams on one screen.

# EmotiBit Oscilloscope
EmotiBit Oscilloscope offers the ability to stream data in real-time from EmotiBit to your computer along with an array of other features.

## Opening EmotiBit Oscilloscope
Follow the [steps on the Getting Started](./Getting_Started.md#Running-EmotiBit-software) page to run EmotiBit Oscilloscope.

## Using EmotiBit Oscilloscope
- The Oscilloscope offers the following features:
![][EmotiBit-Oscilloscope]

[ToDo:Update the Gif above to represent the new oscilloscope]
  - <details><summary>Connecting to EmotiBit</summary>

    - The Oscilloscope displays all available EmotiBits on the network in a list.  
    - You can click on any EmotiBit in the list to connect to it. 
    </details>

  - <details><summary>Streaming real-time Data</summary>

    - The moment you connect to an EmotiBit, the EmotiBit Ocsilloscope will display the data being transmitted by the EmotiBit.
    </details>
  
  - <details><summary>Recording Data</summary>
    
    - Select an EmotiBit from the list of available EmotiBits.
    - You can initiate a record session by clicking on the record button. When a record session is initiated, the EmotiBit will start recording the data on the onboard SD-Card as well as stream it on the Oscilloscope.
    - Once the Recording has been Initiated, you will notice the `red recording` indicator led flashing on the EmotiBit. You are also free to move in/out of the network, close the Oscilloscope, or connect to a new Oscilloscope.
    -  We recommend using the EmotiBit in-network as much as possible, connected to the Oscilloscope. This helps in generating more time-syncs which improves timestamp accuracy.
    </details>
  
  - <details><summary>Log note(labeling data)</summary>
    
    - Users can annotate data by adding labels/notes in real time. 
    - Type in the Note in the `Log Note` text box and click on the `Log Note` button to add notes to the data being recorded.
    </details> 
    
  - <details><summary>Power Modes</summary>
    
    The EmotiBit has 4 power modes. All modes can be accessed using the EmotiBit Oscilloscope.
    - **Normal Mode**: In normal mode, the EmotiBit works with complete functionality, being able to record and transmit data.
    - **Low Power Mode**: In Low power mode, the EmotiBit can record but cannot transmit data in real-time. It, however, continues to get the time-sync pulses.
    - **WiFi Off**: This mode causes the EmotiBit to shut down the onboard WiFi shield. This saves power and enables long recording sessions. However, since the WiFi shield is Off, the EmotiBit cannot get time-sync pulses, which can lead to less accurate time stamping. A `long press` of the EmotiBit button toggles `normal mode` and `WiFi off mode`. If using the EmotiBit in `WiFi off` mode, we recommend leaving the EmotiBit running for a couple of minutes towards the end of the record session in `normal mode`. This can potentially help with time-syncing issues.
    - **Sleep**: In sleep mode, EmotiBit stops any tasks it is performing and goes to sleep. We recommend switching the EmotiBit into `Sleep mode` instead of un-plugging the EmotiBit battery when not in use for short periods. If the EmotiBit is being left un-used for a long duration, it is best to flip the Hibernate Switch located at the bottom to `HIB`. 
    </details>
  
  - <details><summary>DC/DO counter</summary>

    `Data Clipping` and `Data Overflow` are metrics that are used to determine data integrity.
    
    - `Data Clipping`: A clipping event occurs when the data recorded by any sensor goes out of the predefined bounds. 
    - `Data Overflow`: An overflow event occurs when the internal data buffers overflow, which results in loss of data samples.
    </details>

  - <details><summary>Battery Level Indicator</summary>
  
    - The Battery Level indicator displays the charge available in the battery as a percentage. 
    - We recommend not letting the battery fall below 10% as it might begin to interfere with the sensor data acquisition.
    </details>

  - <details><summary>Output List</summary>

    The output list shows the options available to transmit the data out of the EmotiBit Oscilloscope.
    - <details><summary>OSC</summary>

      - **EmotiBit Oscilloscope v1.2.0 and up** support the ability to transmit incoming data from an EmotiBit to a user-defined output channel using the OSC protocol.
      - To enable OSC, just click on the `Output List` dropdown in the EmotiBit Oscilloscope and enable `OSC`.
      - The EmotiBit Oscilloscope reads in and transmits out the data according to the specifications provided in the `oscOutputSettings.xml` file.
        - This file is located in the EmotiBit Oscilloscope folder in the C: - `C:\Program Files\EmotiBit\EmotiBit Oscilloscope\data`.
      - You can modify the contents of this file to control the behavior of the OSC output stream.
      - A snippet of the default contents are shared below
      ```
      <patchboard>
	      <settings>
		      <input>
			      <type>EmotiBit</type>
		      </input>
		      <output>
			      <type>OSC</type>
			      <ipAddress>localhost</ipAddress>
			      <port>12345</port>
		      </output>
	      </settings>
	      <patchcords>
		      <patch>
			      <input>PR</input>
			      <output>/EmotiBit/0/PPG:RED</output>
		      </patch>		
              <patch>
			      <input>PI</input>
			      <output>/EmotiBit/0/PPG:IR</output>
		      </patch>	
		      <patch>
			      <input>PG</input>
			      <output>/EmotiBit/0/PPG:GRN</output>
		      </patch>
	      </patchcords>
      </patchboard>	
      ```
      - As you can see, the `input` is set to an EmotiBit, which is streaming data to the oscilloscope.
      - The Oscilloscope takes this data and relays it over the IP-Address and Port specified. 
      - A `patch` connects an input stream to an output stream. 
        - As an example, the input `PR` (PPG Red channel) stream is patched to the output stream called `/EmotiBit/0/PPG:IR`. 
      - When using the OSC protocol, at the receiver, you must use the same IP-Address, Port number, and label name you used as the output label here. To get started, check out this example of [OSC Oscilloscope as a receiver](https://github.com/produceconsumerobot/ofxOscilloscope/tree/master/oscOscilloscopeExample). If you have enabled OSC data transmission on the Emotibit Oscilloscope, you can run the example in the above link to plot the data being relayed by the EmotiBit oscilloscope.
    </details>
  </details>

# EmotiBit DataParser
The DataParser is used to convert the un-processed recorded data into processed data type files.

## EmotiBit file types
There are 3 types of files associated with EmotiBit
- Un-processed data file(**csv**)
  - Every recording sessions generates 1 un-processed data file.
  - This file is named with the start time of the recording session. Ex: `2019-01-30_11-57-13-492.csv`
- Information file(**json**)
  - Contains information like sampling rates and other important settings for each sensor/stream.
  - It shares the name of the un-processed file. For example, the `info` file for the above un-processed file will be named `2019-01-30_11-57-13-492_info.json`
- Processed data file(**csv**)
  - the un-processed file is converted to processed files by running the DataParser.
  - Each processed file contains data for a specific data type.
  - The name for each processed file is created by joining the `TypeTag` of the data type to the un-processed file name.
    - Ex: After running the data parser on `2019-01-30_11-57-13-492.csv`, the processed data file containing the data for `PPG IR channel` 
    will be called `2019-01-30_11-57-13-492_PI.csv`
    - For more details on data types, see [EmotiBit Data Types](./Working_with_emotibit_data.md#emotibit-data-types) (below).

## EmotiBit data types
Each data type represents a unique signal captured by EmotiBit and is represented by a unique `TypeTag`. The most up-to-date list of TypeTags can be found in https://github.com/EmotiBit/EmotiBit_XPlat_Utils/blob/master/src/EmotiBitPacket.cpp

For a quick look at the available data types, you can check out the table below. We periodically update this table as the EmotiBit firmware grows.

- <details open><summary><b>Biometric TypeTags</b></summary>

  |TypeTag    | Description          |
  |:-----:|----------------------|
  |EA     |EDA- Electrodermal Activity  |
  |EL     |EDL- Electrodermal Level     |
  |ER     |EDR- Electrodermal Response  |
  |PI     |PPG Infrared          |
  |PR     |PPG Red               |
  |PG     |PPG Green             |
  |T0     |Temperature          |
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
  |SA     |Skin Conductance Response Amplitude        |
  |SR     |Skin Conductance Response Rise Time |
  |SF     |Skin Conductance Response Frequency |
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

## Opening EmotiBit DataParser
Follow the [steps on the Getting Started](./Getting_Started.md#Running-EmotiBit-software) page to run EmotiBit DataParser.

## Using EmotiBit DataParser
![][EmotiBit-DataParser]
- **Understanding the DataParser**
  - `Status Bar`
    - It can either be `IDLE` or `PROCESSING`. The data parser is in the `PROCESSING` state when it is performing the conversion of a file. It is `IDLE` otherwise
  - `Load file` button
    - Click on the button to load a file to parse.
  - `Activity monitor`
    - This section displays data from the file which is being parsed. When `IDLE`, this section is blank.

- **Parsing  the recorded data:**
  - Click on the `Load file` button. A file browser opens up. Navigate to the `csv` file which you want to process and select that file.
  - The parser will show the "percentage completed" as it parses the data.
  - The parser will quite once the data has been processed.
  - The parsed data files are created in the same directory as the original **raw** file
  

### EmotiBit data sampling rates
The most up to date list of sampling rates for each data stream can be found in the `_info.json`. 
The sampling rates for all the sensors can alse be found [here](./Learn_more_about_emotibit.md#Sampling-rates).


# Visualize Recorded Data
Visualization tools can often help answer some immediate questions and hence, can be very useful when working with time-series data. Below we have outlined a number of tools that we think can be very successful.
## Visualization Tools
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
