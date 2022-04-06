# Working with EmotiBit Data

# Table of Contents
- Overview
- EmotiBit Oscilloscope
  - Opening EmotiBit Oscilloscope
  - Using EmotiBit Oscilloscope
- EmotiBit DataParser
  - Opening EmotiBit dataParser
  - Using EmotiBit DataParser
- EmotiBit DataViewer
  - Opening EmotiBit DataViewer
  - Using EmotiBit DataViewer

# Overview
We at Connected Future Labs created EmotiBit keeping **data** at the core of development. We realize that Data is the most important aspect of working with EmotiBit and therefore, we have developed
some essential tools which we think will help our users interact better with the EmotiBit.
On this page we will talk about:
- [**EmotiBit Oscilloscope**](#Real-Time-Streaming): An intuitive and powerful tool to **live stream data** from any EmotiBit active on the Network. You would also use this tool to initiate
recording, add User-Notes and an array of other useful features
- [**EmotiBit DataParser**](#Next-Steps-Converting-Raw-Data): It is hard to parse and make intuitive sense of the raw data collected by the EmotiBit. We have therefore created a parser, which goes through the raw data and creates data files that are easy to read and interpret by humans or other visualization software.
- [**Data Visualization**](#Next-Steps-Visualize-Recorded-Data): Being able to visualize data helps in making intuitive sense of the data collected. We suggest some tools which we have found to be very useful in analyzing data and also introduce a tool we have created in python to visualize all data streams on one screen.

# EmotiBit Oscilloscope
EmotiBit Oscilloscope offers the ability to stream data in real-time from EmotiBit to your computer along with an array of other features.

## Opening EmotiBit Oscillosocpe
Follow this guide to open EmotiBit Oscillosopce.

## Using EmotiBit Oscilloscope
- The Oscilloscope offers the following features:
![][EmotiBit-Oscilloscope]

[ToDo:Update the Gif above to represent the new oscilloscope]
  - <details><summary>Track All EmotiBits on the N/W</summary>

    - All active EmotiBits on the same network as the host computer show up on the Oscilloscope.  
    - The EmotiBit you are connected to appears with an `X` in front of the IP address of that EmotiBit.  
    - All other EmotiBits, if present are grouped as a list. You can have several Oscilloscopes open on the same computer with an EmotiBit connected to each Oscilloscope. **However**, one Oscilloscope can be connected only to one EmotiBit at a time. If an EmotiBit is already connected to an Oscilloscope, it appears **greyed out** to all other oscilloscopes on the network.
    </details>

  - <details><summary>Stream real-time Data</summary>

    - The Moment you connect to an EmotiBit, the EmotiBIt Ocsilloscope will begin to display the data being transmitted by the EmotiBit. You can switch between available EmotiBits in the list and the data streams will update automatically.
    </details>
  
  - <details><summary>Recording Data</summary>
    
    - This is one of the most important features offered by the EmotiBit Oscilloscope. 
    - By clicking on the Record button, you can initiate a record session on the Selected EmotiBit. When a record session is initiated, the EmotiBit will start recording the data on the onboard SD-Card as well as stream it on the Oscilloscope.
    - The Important thing to note is that a recording session can be initiated only from an EmotiBit Oscilloscope window.
    - The EmotiBit uses this connection with an Oscilloscope to generate time syncing information essential for data integrity. We, therefore, recommend using the EmotiBit in-network as much as possible, connected to the Oscilloscope.
    - Once the Recording has been Initiated, you will notice the `red recording` indicator led flashing on the EmotiBit. You are also free to move in/out of the network, close the Oscilloscope, or connect to a new Oscilloscope.

    </details>
  
  - <details><summary>Log note(labeling data)</summary>
    
    - The ability to add User Notes was recognized as **essential for the user experience** by our development team. 
    The EmotiBit Oscilloscope can be used to label/tag the data being recorded by the EmotiBit in real-time.
    Note that the User Note feature is available only when a recording session has been initiated by the user.
    </details> 
    
  - <details><summary>Power Modes</summary>
    
    The EmotiBit has 4 power modes it can work in. All modes can be accessed using the EmotiBit Oscilloscope.
    - **Normal Mode**: In normal mode, the EmotiBit works with complete functionality, being able to record and transmit data.
    - **Low Power Mode**: In Low power mode, the EmotiBit can record but cannot transmit data in real-time. It, however, continues to get the time-sync pulses.
    - **WiFi Off**: This mode causes the EmotiBit to shut down the onboard WiFi shield. This saves power and enables long recording sessions. However, since the WiFi shield is Off, the EmotiBit cannot get time-sync pulses, which can lead to less accurate time stamping. A `long press` of the EmotiBit button toggles `normal mode` and `WiFi off mode`. If using the EmotiBit in `WiFi off` mode, we recommend leaving the EmotiBit running for a couple of minutes towards the end of the record session in `normal mode`. This can potentially help with time-syncing issues.
    - **Sleep**: In sleep mode, EmotiBit stops any tasks it is performing and goes to sleep. We recommend switching the EmotiBit into `Sleep mode` instead of un-plugging the EmotiBit battery when not in use for short periods. If the EmotiBit is being left un-used for a long duration, it is best to flip the Hibernate Switch located at the bottom to `HIB`. 
    </details>
  
  - <details><summary>DC/DO counter</summary>

    Data Clipping and Data Overflow are metrics that are used to determine data integrity. Each metric is explained here:
    
    - Data Clipping: A clipping event occurs when the data recorded by any sensor goes out of the predefined bounds. The user should interpret the occurrence of a clipping event as a point in time where the captured data does not represent the actual physical phenomenon.
    - Data Overflow: An overflow event occurs when the internal data buffers are filled and no new data being generated can be recorded. This leads to    "blanks" in the data time series. An overflow event should be taken more seriously, as the EmotiBit has been designed to avoid such scenarios.
    </details>

  - <details><summary>Battery Level Indicator</summary>
  
    - The Battery Level indicator displays the charge available in the battery as a percentage. We recommend not letting the battery fall below 10% as it might begin to interfere with the sensor data acquisition.
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
The DataParser is used to convert the recorded data into individual files, where each file represents a typetag.

## Opening EmotiBit DataParser
Follow this guide to open EmotiBit DataParser.

## Using EmotiBit Data Parser
![][EmotiBit-DataParser]

- **Understnading the DataParser**
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

## EmotiBit Typetags

For more details on the EmotiBit data types, check out the [EmotiBit Packet Architecture](./Learn_more_about_emotibit.md/#TypeTag-Character-Codes)


## Next Steps: Visualize Recorded Data
Visualization tools can often help answer some immediate questions and hence, can be very useful when working with time-series data. Below we have outlined a number of tools that we think can be very successful.
### Visualization Tools
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
