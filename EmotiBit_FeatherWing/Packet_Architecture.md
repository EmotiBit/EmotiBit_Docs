This document shows an in-depth view of the EmotiBit packet Architecture and Data Type Tags.
## Table of Contents
- [Packet Format](#packet-format)
  - [TypeTag Character Codes](#typetag-character-codes)
    - [Biometric TypeTags](#biometric-typetags)
    - [General TypeTags](#general-typetags)
    - [Computer to EmotiBit TypeTags](#computer-to-emotibit-typetags)

## Packet Format
- `TIMESTAMP`-`PACKET#`-`#DATAPOINTS`-`TYPETAG`-`VERSION`-`RELIABILITY`-`PAYLOAD`
  - **Timestamp:** milliseconds since start of EmotiBit
  - **Packet Number:** packet count since start of EmotiBit
  - **Number of Datapoints:** Number of data points in the payload
  - **Typetag:** type of data being sent
  - **Version:** version of packet protocol
  - **Reliability:** data reliability score out of 100, currently always 100
  - **Payload:** data to send
- Example Packets:

![alt text][Pack]
### TypeTag Character Codes

#### Biometric TypeTags
|Tag    | Description          |
|:-----:|----------------------|
|EA     |EDA                   |
|EL     |EDL                   |
|ER     |EDR                   |
|PI     |PPG Infrared          |
|PR     |PPG Red               |
|PG     |PPG Green             |
|T0     |Temperature (Si7013)  |
|TH     |Thermopile(ML90632)            |
|H0     |Humidity (Si7013)     |
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

|Tag    | Description                       |
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

#### Computer to EmotiBit TypeTags

|Tag    | Description                       |
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

[GPS]: https://developer.android.com/reference/android/location/Location
[Pack]: ../assets/PacketExample.png "Example Packets"