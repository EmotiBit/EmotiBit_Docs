# Getting Started with EmotiBit
[comment]: <> ([alt text][SideView])

# Table of Contents
- [Stack, Sense and Stream](#Stack-Sense-and-Stream)
  - [EmotiBit Forum](#EmotiBit-Forum)
  - [Unboxing](#Unboxing)
    - [EmotiBit](#EmotiBit)
    - [Essentials Kit](#Essentials-Kit)
    - [Electrode Kit](#Electrode-Kit)
    - [All-in-one-bundle](#All-in-one-bundle)
  - [Assembling your EmotiBit](#Assembling-your-EmotiBit)
    - [Adding WiFi credentials](#Adding-WiFi-credentials)
    - [Stack your EmotiBit!](#Stack-your-EmotiBit)
  - [Installing EmotiBit Software](#Installing-EmotiBit-Software)
  - [Running EmotiBit Software](#Running-EmotiBit-software)
    - [On Windows](#On-Windows)
    - [On macOS](#On-macOS)
    - [On Linux](#On-Linux)
- [Installing EmotiBit Firmware](#Installing-EmotiBit-Firmware)
  - [Using the EmotiBit Firmware Installer](#Using-the-EmotiBit-Firmware-Installer)
  - [For Linux and Advanced Users](#For-Linux-and-Advanced-Users)
- [EmotiBit Bootup](#EmotiBit-Bootup)
- [Using EmotiBit Oscilloscope](#Using-EmotiBit-Oscilloscope)
- [EmotiBit: LEDs and Buttons](#EmotiBit-LEDs-and-Buttons)
- [Next Steps](#Next-Steps)
- [Troubleshooting](#Troubleshooting)


# Stack, Sense and Stream

<img src="./assets/StackSenseStream.png" width="1000">

- Follow the steps below for more information on downloading EmotiBit software and connecting to WiFi.

## EmotiBit Forum
<img src="./assets/EmotiBit-forum.png" align="right" width="300">

The [EmotiBit forum](http://forum.emotibit.com) is a great place to get answers to all things EmotiBit!<br>
- Find answers to questions you may have about using EmotiBit.
- Share your experience working with EmotiBit or the latest signal processing tools.
- Take a glance at the [EmotiBit FAQ](https://www.reddit.com/r/EmotiBit/collection/27921349-c38f-4df4-b708-99346979039f). *Great minds think alike! If you have a question, the FAQ page probably has an answer.*
- Share your latest publication with the community or start a discussion about the future of biometric sensing!

## Unboxing
The following sections explain the contents of each item available for purchase at the [shop.EmotiBit.com](http://shop.emotibit.com/):

### EmotiBit 

- **1x EmotiBit** with finger loop Emoti-stretch strap
  - Depending on your purchase, you may either have an EmotiBit MD or an EmotiBit EMO
- **1x Emoti-genic barrier** (provides an additional hygienic layer and sweat protection)
- **2x EDA electrodes (Ag/AgCl)** attached to the EmotiBit
- **2x EmotiBit stickers**

<img src="./assets/EmotiBit-box-contents.jpg" width="300">

-------------------------------

### Essentials Kit

The Essentials kit contains everything you will need to get started with EmotiBit! In the box you will find:
- **Adafruit Feather M0 WiFi**
- **400mAh Lithium ion battery**
- **High-speed microSD card**
- **MicroSD card reader**
- **Micro USB cable**
- **3x Emoti-stretch straps** of different lengths to wear EmotiBit nearly anywhere on the body, ranging from a child’s wrist to an adult head
- **Plastic spudger** -- used to easily toggle the hibernate switch and EmotiBit button

<img src="./assets/EmotiBit-EssentialsKit.jpg" width="400">

-------------------------
### Electrode Kit
The electrode kit has been designed for users who use multiple EmotiBits for research and intend to frequently swap out the electrodes. the electrode kit includes
- **10x EDA electrodes (Ag/AgCl)**
- **4x solder-cup snaps** (to add your own EDA leads)
- **5x Emoti-genic barriers** (provides an additional hygienic layer and sweat protection)

<img src="./assets/Electrode-kit.jpg" width="300">

---------------------------
### All-in-one-bundle
If you purchased the All-in-one-bundle, you will receive the [EmotiBit](#EmotiBit), [Essentials Kit](#Essentials-Kit) **and** [Electrode Kit](#Electrode-Kit).

------------------
## Assembling your EmotiBit
### Adding WiFi credentials
<img src="./assets/SD-CardInReader.jpg" align="right" width="250">

- Plug in the USB card reader loaded with the SD-Card into the computer.
- Download the config file from https://www.emotibit.com/files/config.
- Open the config file in any text editor (e.g. Notepad on Windows or text edit on macOS).
- Add your WiFi credentials by changing `myWifiNetwork` to the name of your WiFi network and change `myPassword`to the password for your WiFi network. 
- Save the file onto your microSD card. Eject the SD-Card from your computer. 

**Pro tip**: If you use multiple WiFi networks and want your EmotiBit to automatically connect to whichever one is in range, simply add both networks to the WifiCredentials array in the config file like this:<br> `{"WifiCredentials": [{"ssid": "myWifiNetwork1", "password" : "myPassword1"},{"ssid": "myWifiNetwork2", "password" : "myPassword2"}]}`

**Note: Currently EmotiBit only supports the 2.4GHz band for WiFi and does not support enterprise networks (that require a login/password after connecting).** This is due to HW/FW limitations of the presently supported Adafruit Feather M0 WiFi.

### Stack your EmotiBit!

- On the EmotiBit
  - Insert the SD-Card into the EmotiBit.
  - Make sure the sliding switch (*Hibernate switch*) is set to the active (not HIB) position as shown *(Available on only EmotiBit version V4)*.
    - <img src="./assets/correctHibernateSwitch.jpg" width="250">

- Plug the battery into the Feather (**ensure the connector is firmly pushed all the way into the Feather connector**)
- Stack the Feather with EmotiBit (*12 pin connector goes into the 12 pin socket and the 16 pin connector goes into the 16 pin socket*)

![][EmotiBit-stackup]

## Installing EmotiBit Software

[Download the EmotiBit Oscilloscope](https://github.com/EmotiBit/ofxEmotiBit/releases/latest).
- <details><summary><b>Installation Instructions For Windows Users</b></summary>
 
    - _**Note:** EmotiBit software is supported only for Windows 10+._
    - After you download `EmotiBitSoftware-Windows.zip`, go ahead and extract it.
    - You will find an `.msi` installer inside the extracted folder. Run the installer by double-clicking.
      - If the Windows Defender SmartScreen pops up, click on `More Info`.
      - Then click on `Run Anyway`.
      - <img src="./assets/windows-smart-screen-more-info.png" width="250">
    - Follow through the setup. Click on `Close` once the setup is complete and the EmotiBit Software has been installed.
    - You will notice that shortcuts to `EmotiBit Oscilloscope`, `EmotiBit DataParser` and `EmotiBit FirmwareInstaller` have been created in the start menu and on the desktop.
    - **Note: The EmotiBit Software installation process is sometimes blocked by any anti-virus tool you might have installed on your system. If you face any issues with installation, make sure to check that the appropriate settings are enabled on your anti-virus software to allow a third-party installs. You will likely also need to allow firewall permissions to allow streaming data on your WiFi networks.**
  </details>

- <details><summary><b>Installation Instructions For Mac Users</b></summary>
    
  - Download `EmotiBitSoftware-macOS.zip` from the release page.
  - Move the downloaded zip file to a folder location you desire. Double click on the .zip file to extract it.
  - You will find the Applications in the extracted folder.
  
  > **Note that the Software is currently supported only for macOS-Mojave[version 10.14] and macOS-Catalina[version 10.15]. (Monterey mostly works, but has some issues with the DataParser that we're working on)**
  - <details><summary>Check your Operating System version</summary>
    
    - You can find your macOS version by clicking on the `Apple Logo`(on the top left of your screen) > `About This Mac`.
    
    <img src="./assets/macOS-Catalina-OS_version.png" width="800">
    </details>
  </details> 

- <details><summary><b>Installation Instructions For Linux Users</b></summary>
    
  - Download `EmotiBitSoftware-linux.zip` from the release page.
  - Move the downloaded zip file to a folder location you desire. Extract the zipped download.
  - Follow the instructions in the ReadMe file inside the extracted folder.
  </details>    

## Running EmotiBit software
Based on your operating system, follow the steps below:
### On Windows
You can click on the start menu and search for the name of the application you want to run, e.g.`EmotiBitFirmwareInstaller`. The application should pop up in the search. Double-click on the application to run it!

### On macOS
You can find the EmotiBit applications in the folder you just extracted (*as mentioned in the steps in the previous section*)
- <details><summary>Opening Software in mojave</summary>
        
    - Right click on the application you want to run. Choose **Open**. 
    - If this is the first time you are using this application, a dialog box might appear asking you to `Allow` this application. Click on `Allow`. 
    - You will see the EmotiBit Application start.
  </details>
- <details><summary>Opening Software in Catalina</summary>
  
    - Right click on the application you want to run. Choose **Open**. 
    - A dialog box will appear with options `Move to Trash` or `Cancel`. Click `Cancel`. You will have to allow the application to run in the `Security and Privacy` center. To do so:<br>
            ![][macOs-Catalina-Initial_Oscilloscope_Error]
    - Click on the `Apple Logo` > `Syatem Preferences` > `Security and Privacy`.
            ![][macOS-Catalina-sys_pref]
    - You will find a request from the applicaiton at the bottom of this window. Click on `Open Anyways`. 
            ![][macOS-Catalina-System_pref_Security&options]
    - Click on `Allow` on the dialog box that appears.This will open the application.
            ![][macOS-Catalina-Allow_emotibit]
  </details>

### On Linux
Build the application from source. You can find instructions in the `ReadMe` provided with the zip file downloaded in the previous step..


# Installing EmotiBit Firmware
To start using EmotiBit, you will first need to install the latest EmotiBit firmware on the Feather.
- If you did not order an Essentials-Kit, Basic-Kit (*Kickstarter*) or Research-Kit (*Kickstarter*), you will need to 
get one to start using EmotiBit. You can grab one at [Adafruit.com](https://www.adafruit.com/product/2598).

## Using the EmotiBit Firmware Installer
- You will need the `EmotiBit FirmwareInstaller`, which comes with the EmotiBit software bundle.
  - If you have not done so already, follow [these steps to grab the latest EmotiBit software](#Installing-EmotiBit-Software). 
- Open the `EmotiBit FirmwareInstaller`. 
  - Follow the instructions mentioned in the [section above](#Running-EmotiBit-software) to start using `EmotiBit FirmwareInstaller`
- After you start the application, follow the on-screen instructions to complete installing the firmware.
- <details><summary>Screengrabs from EmotiBitFirmwareInstaller</summary>
        
  - ToDo: add screengrabs
  - [image1]()
  - [image2]()
  - [image3]()
  </details>

## For Linux and Advanced Users
- <details><summary> Installing Emotibit Firmware </summary></details>
  
  - The FirmwareInstaller essentaily performs 3 actions:
    1. Uploads the firmware updater sketch to prep the Feather for WINC updater
    2. Updates the WINC WiFi module FW to version 19.6.1
    3. Uploads the latest EmotiBit FW onto the Feather, after the WINC has been updated
  - We use the [`bossac`](http://manpages.ubuntu.com/manpages/bionic/man1/bossac.1.html) command line tool to upload binary files to the feather.
  - There are 2 requirements to run bossac
    - COM port on which the Feather is detected
    - The bin file (*provided in the software release*)
  - To perform the operations manually, the follow the below listed steps:
    - Navigate to the `data` folder located inside the EmotiBit software directory.
      - On Linux the path to the data folder should look like `EmotiBitSoftware-linux/ofxEmotiBit/EmotiBitFirmwareInstaller/bin/data`
      - On MacOS the path should look like `EmotiBitSoftware-macOS/EmotiBitFirmwareInstaller.app/Contents/Resources`
      - On Windows the path will be `C:\Program Files\EmotiBit\EmotiBit FirmwareInstaller\data`
    - Open a `cmd prompt` window for Windows or `terminal` for Linux/Mac at this location
    - Connect the Feather to the computer using a data-capable USB cable
      - **The Feather should NOT be stacked with EmotiBit** (to enable the programmer mode LED)
    - Double-press the reset button to set the Feather in programmer mode.
      - You should see the RED LED on the Feather pulsating!
        - [ToDo: add gif]
    - **WARNING: DO NOT UNPLUG OR RESET FEATHER WHILE UPLOAD/UPDATE IN PROGRESS. YOU COULD BRICK YOUR FEATHER!**
    - Upload the firmware updater sketch by running the following command (*use .\bossac.exe for windows*)
      - `./bossac -i -d --port=YOUR_FEATHER_COM_PORT -U true -i -e -w -v ./WINC/FirmwareUpdater.ino.feather_m0.bin -R`
    - Update the WINC by running (*use .\FirmwareUploader.exe for windows*)
      - `./WINC/FirmwareUploader -port YOUR_FEATHER_COM_PORT -firmware ./WINC/m2m_aio_3a0.bin`
    - ONLY AFTER the FirmwareUploader command completes, double-press the reset button to set the Feather in programmer mode again
    - Upload the EmotiBit FW using (*use .\bossac.exe for windows*)
      - `./bossac -i -d --port=YOUR_FEATHER_COM_PORT -U true -i -e -w -v EmotiBit_stock_firmware.ino.feather_m0.bin -R`
</details> 

# EmotiBit Bootup
When EmotiBit is booting up, the LEDs are used to indicate the steps in the process. If EmotiBit gets stuck prior to fully connecting to your WiFi, you can use the below table to assess what went wrong and how to fix it.

|LED State|**LED Indicator**|**What to do?**|
|--|--------------|---------|
|Feather RED LED ON|<img src="./assets/EmotiBit-bootup-stage-0.jpg" width="300">|Write a post describing your steps on http://forum.emotibit.com/ |
|Feather RED LED turns ON for a few seconds and then stays OFF|<img src="./assets/EmotiBit-bootup-stage-1.jpg" width="300">|Check if SD-Card is correctly inserted|
|EmotiBit RED LED ON|<img src="./assets/EmotiBit-bootup-stage-2.jpg" width="300">|Check if config file is present on the SD-Card|
|EmotiBit BLUE LED ON|<img src="./assets/EmotiBit-bootup-stage-3.jpg" width="300">|Verify correct WiFi credentials in config file (see [Adding WiFi credentials](https://github.com/EmotiBit/EmotiBit_Docs/blob/fix-documentationUpdate/Getting_Started.md#adding-wifi-credentials))|
|Feather Green LED ON|<img src="./assets/EmotiBit-bootup-stage-4.jpg" width="300">|Huzzah! EmotiBit is connected to your WiFi! Open EmotiBit Oscilloscope to start streaming biometric data!|

# Using EmotiBit Oscilloscope
[Learn more about streaming and recording data using the EmotiBit Oscilloscope](./Working_with_emotibit_data.md/#Real-Time-Streaming)

# EmotiBit: LEDs and Buttons

Learn [More about the LEDs and buttons on EmotiBit](./Learn_more_about_emotibit.md/#LEDs-and-Buttons)


# Next Steps
By this point, you're ready to be an EmotiBit rockstar!! However, we at CFL believe in empowering the user. Below are listed topics, which we feel will help you understand and ultimately **master working with EmotiBit**.
- EmotiBit Oscilloscope
  - [Learn more about streaming and recording data using the EmotiBit Oscilloscope](./Working_with_emotibit_data.md/#Real-Time-Streaming)
- Working with your data
  - [Converting raw data](./Working_with_emotibit_data.md/#Converting-Raw-Data)
  - [Visualizing  Data](./Working_with_emotibit_data.md/#Visualize-Recorded-Data)
- [Keep EmotiBit up to date](./Keep_emotibit_up_to_date.md)
- [Contributing to the EmotiBit Community](./Contributing_to_emotibit_community)
- [Learn more about EmotiBit](./Learn_more_about_emotibit.md)

# Troubleshooting
- Checkout the [EmotiBit FAQ](https://www.reddit.com/r/EmotiBit/collection/27921349-c38f-4df4-b708-99346979039f).
- FAQs did not help out? Post on the [EmotiBit Forum](http://forum.emotibit.com)

[ButtonsAndSwitches]: ./assets/EmotiBit-buttonsAndSwitches.jpg "EmotiBit Buttons and Switches"
[LED]: ./assets/M0_WiFi_LED_Indicators_01.png "Feather LED's"
[macOS-version]: ./assets/macOS-Catalina-OS_version.png "macOS version" 
[oscilloscope-drirectory]: ./assets/macOS-oscilloscope_file_heirarchy.png ""
[macOs-Catalina-Initial_Oscilloscope_Error]: ./assets/macOs-Catalina-Initial_Oscilloscope_Error.png ""
[macOS-Catalina-sys_pref]: ./assets/macOS-Catalina-sys_pref.png "" 
[macOS-Catalina-System_pref_Security&options]: ./assets/macOS-Catalina-System_pref_Security&options.png "" 
[macOS-Catalina-Allow_emotibit]: ./assets/macOS-Catalina-Allow_emotibit.png "" 
[EmotiBit-stackup]: ./assets/EmotiBit_stack_boards.gif ""
[EmotiBit-box-contents]: ./assets/EmotiBit-box-contents.jpg ""
[Electrode Kit]: ./assets/Electrode-Kit.jpg ""
