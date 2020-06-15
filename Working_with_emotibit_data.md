# Working with EmotiBit Data
We at Connected Future Labs created EmotiBit keeping **Data** at the core of development. We realize that Data is the most important aspect of working with EmotiBit and therefore, we have developed
some essential tools which we think will help our users interact better with the EmotiBit.
On this page we will talk about:
- **EmotiBit Oscilloscope**: An intuitive and powerful tool to live stream data from any EmotiBit active on the Network. You would also use this tool to initiate
recording, add User-Notes to data being recorded and an array of other useful features
- **EmotiBit DataParser**: The raw data collected by the EmotiBit is hard to parse using human eyes. It is also hard to make intuitive sense of the raw data collected by the EmotiBIt. We have therefore created a parser, which goes through the raw data and creates data files that are easy to read and interpret by humans or other visualization software.
- **Data Visualization**: Being able to visualize data helps in making intuitive sense of the data collected. We suggest some tools which we have found to be very useful in analyzing data and also introduce a tool we have created in python to visualize all data streams on one screen.

## Real-Time Streaming
The ability to stream data in real-time from the EmotiBit to a computer is incredible. The EmotiBit Oscilloscope offers this capability along with an array of other functionalities.

### Get the oscilloscope
- If you have not already, get the [latest release of EmotiBit Oscilloscope](https://github.com/EmotiBit/ofxEmotiBit/releases/latest)
You can follow the installation instruction on the [getting started](./Getting_Started.md/#Get-the-Software) page.

### EmotiBit Oscilloscope user guide
- The Oscilloscope offers the following functionalities:
  - <details>
    <summary>Track All EmotiBits on the N/W</summary>
    <br>

    - All active EmotiBits on the same network as the host computer show up on the Oscilloscope.  
    - The EmotiBit you are connected to appears with an `X` in front of the IP address of that EmotiBit.  
    - All other EmotiBits, if present are grouped as a list. You can have several Oscilloscopes open on the same computer with an EmotiBit connected to each Oscilloscope. DO remember, however, that one Oscilloscope can be connected only to one EmotiBit at a time. And, if an EmotiBit is already connected to an Oscilloscope, it appears **greyed out** to all other oscilloscopes on the network.
    </details>

  - <details>
    <summary>Stream real-time Data</summary>
    <br>

    - The Moment you connect to an EmotiBit, the EmotiBIt Ocsilloscope will begin to display the data being transmitted by the EmotiBit. You can switch between available EmotiBits in the list and the data streams will update automatically.
    </details>
  
  - <details>
    <summary>Recording Data</summary>
    <br>
    
    - This is one of the most important features offered by the EmotiBit Oscilloscope. 
    - By clicking on the Record button, you can initiate a record session on the Selected EmotiBit. When a record session is initiated, the EmotiBit will start recording the data on the onboard SD-Card as well as stream it on the Oscilloscope.
    - The Important thing to note is that a recording session can be initiated only from an EmotiBit Oscilloscope window.
    - The EmotiBit uses this connection with an Oscilloscope to generate time syncing information essential for data integrity. We, therefore, recommend using the EmotiBit in-network as much as possible, connected to the Oscilloscope.
    - Once the Recording has been Initiated, you will notice the `red recording`a indicator led flashing on the EmotiBit. You are also free to move in/out of the network, close the Oscilloscope, or connect to a new Oscilloscope.
    </details>
    
  - <details>
    <summary>DC/DO counter</summary>
    <br>
    Data Clipping and Data Overflow are metric that are used to determine data integrity. Each metric is explained here:
    
    - Data Clipping: A clipping event occurs when the data recorded by any sensor goes out of the predefined bounds. The user should interpret the        occurrence of a clipping event as a point in time where the captured data does not represent the actual physical phenomenon.
    - Data Overflow: An overflow event occurs when the internal data buffers are filled and no new data being generated can be recorded. This leads to    "blanks" in the data time series. An overflow event should be taken more seriously, as the EmotiBit has been designed to avoid such scenarios.
    </details>
    
  - <details>
    <summary>Adding User Notes(labeling data)</summary>
    <br>
    
    - The ability to add User Notes was recognized as essential for the user experience by our development team. 
    The Oscilloscope offers the feature to label/tag the real-time data being recorded the EmotiBit.
    Note, that the User Note feature is available only when a recording session has been initiated by the user.
    </details> 

  - <details>
    <summary>Battery Level Indication</summary>
    <br>
  
    - The Battery Level indicator, as is suggestive from the name, displays the charge available in the battery as a percentage. We recommend not letting the battery fall below 20% as it might begin to interfere with the sensors.
    </details>
  - <details>
    <summary>Power Modes</summary>
    <br>
    
    The EmotiBit has 4 power modes it can work in. All modes can be accessed using the EmotiBit Oscilloscope.
    - **Normal Mode**: In normal mode, the EmotiBit works with complete functionality, being able to record and transmit data.
    - **Low Power Mode**: In Low power mode, the EmotiBit can record but cannot transmit data in real-time. It, however, continues to get the time-sync pulses.
    - **WiFi Off**: This mode causes the EmotiBit to shut down the onboard WiFi shield. This saves power and enables long recording sessions. However, since the WiFi shield is Off, the EmotiBit cannot get time-sync pulses, which can lead to less accurate time stamping od data.  The EmotiBit can be toggled between normal mode and WiFi off mode by performing a `long press` the onboard button. If using the EmotiBit in `WiFi off` mode, we recommend leaving the EmotiBit running for a couple of minutes after going back to normal mode. This can potentially help with time-syncing issues.
    - **Hibernate**: In hibernate mode, EmotiBit stops any task it is performing and goes to sleep. We recommend using this mode instead of un-plugging the EmotiBit battery when not in use.
    </details>

### Next Steps: Converting raw recorded data
Being able to stream and record data is a great enabler but often, tools are required to help in analysing the data acquired. In the next sections, you will find additional tools that you might find useful. 

## Converting Raw Data
Data integrity and precise time stamping have been given paramount importance while designing the EmotiBit. Hence, the raw data collected by the EmotiBit is less intuitively understood by human eyes. The `EmotiBit data parser` is a tool that converts this **raw** data into individual files that represent each channel of data acquired.
 
### What you should have at this point
- [Get the data parser](https://github.com/EmotiBit/ofxEmotiBit/releases/latest)
- Data recorded using the EmotiBit. 
  - EmotiBit records data in a single csv file on the onboard SD_Card. To use the parser, you will need to transfer the data file(csv) onto the computer. 
  - You can do so by removing the SD-Card from the EmotiBit and transfer the `.csv` and `.json` file onto the system using the SD-Card USB reader provided in the box.[ToDo: find a place to explain the contents of json file]
### User Guide
[ToDo: Add data parser image]
- <details>
  <summary><b>EmotiBit data parser sections</b></summary>
  <br>
  
  - `Status Bar`: The Status bar on the EmotiBit data parser displays the state of the parser. It can either be `IDLE` or `PROCESSING`. The data parser is in the `PROCESSING` state when it is performing the conversion of a file. It is `IDLE` otherwise
  - `Process File Button`: Click on the button to load a file to process.
  - `Activity monitor`: This section displays data from the file which is being parsed. When the EmotiBit data parser is `IDLE` this section is blank.
  </details>
  
- <details>
  <summary><b>Using the EmotiBit data parser</b></summary>
  <br>
  
  - Open the EmotiBit data parser. 
  - Click on the `Process file button`. A file browser opens up. Navigate to the `csv` file which you want to process and select that file.
  - You can see the lines in the data file being displayed on the `Activity monitor` as the parser goes through the file.
  - When EmotiBit data parser has finished processing the file, it will exit automatically. 
  - You will notice the folder that contained the original `csv` file will now contain additional `csv` files. Each additional `csv` file has the name of the sensor channel it represents appended to base file name.
  - For example, if the base file was named `2019-08-22_14-10-33-300661.csv`, you will get, among other files, a file named `2019-08-22_14-10-33-300661_AX.csv` which represents the data for the accelerometer X-axis channel.[ToDo: Add an image for the folder containing parsed files]
  </details>
### Next Steps: Visualize recorded data
Once you have the individual files representing data from the array of sensors on EmotiBit, the possibilities to use that data are limitless. A great way to understand what the data represents is to visualize it. Read on to discover cool ways to visualize data.
## Visualize Recorded Data
Visualization tools can often help answer some immediate questions and hence, can be very useful when working with time series data. Below we have outlined a number of tools which we think can be very successful.
### Visualization Tools
- Text Editors
  - Notepad++(on Windows)
  - Text Edit(on mac)
- Spreadsheet softwares
  - Microsoft Excel
  - Google Sheets 
- [EmotiBit python data viewer](https://github.com/EmotiBit/EmotiBit_Biometric_Lib/tree/master/py/examples/dataviewer_example)

