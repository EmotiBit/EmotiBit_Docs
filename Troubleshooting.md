# EmotiBit troubleshooting Guide
This guide provides curated answers and solutions for common EmotiBit issues based on community discussions and support posts.

# Typical EmotiBit Getting started flow

- Note: The getting started steps are sequencial. The sequential nature of the steps makes it imposible to get stuck an a step if the previous step has not been successfully completed. For example, EmotiBit cannot be stuck on trying to connect to a WiFi network, is step 1 of Firmware installation was not completed.

## Issue Missing Package Contents
- Affected customers should resch out to us via email. Please provide the order number in the email.
   - If you placed the order on the OpenBCI website, please reach out at support@opencbci.com.
   - If you placed the order on the EmotiBit wensite, please reach out at support@emotibit.com.
---
## Issue Getting Started  Config Txt

**Definition:** Issues related to configuring the `config.txt` file for EmotiBit setup.

### FAQs

1. **[How do I add my WiFi credentials to connect to a network?](https://www.reddit.com/r/EmotiBit/comments/tsiu7j/how_do_i_add_my_wifi_credentials_to_connect_to_a/)**

2. **[Where can I find the WiFi config file to copy onto my SD card?](https://www.reddit.com/r/EmotiBit/comments/tt3cnv/where_can_i_find_the_wifi_config_file_to_copy/)**

---

## Issue Getting Started  Firmware Installation

**Definition:**
This category highlights various problems users face when attempting to install firmware on EmotiBit devices.

### Indication of this Error
- Error messages stating "Feather not detected" or "Firmware installation failed".
  - If the firmware installation has failed, you may see a blinking red LED on the Feather board (**NOT THE RED EMOTIBIT RECORDING LED**) on the Feather ESP32 Huzzah. This is because the Feather is shipped with that default program and it persists if new firmware was not programmed on the Feather.

### Solution Steps
1. **Check USB cable**: Ensure you are using a data-capable USB cable. Charge-only cables will lead to detection failures.
2. **Verify HIB Switch Position**: Confirm that the HIB switch on the Feather board is set to "On" (not in HIB).
3. **Install Correct Drivers**:
  - Make sure the SiLabs USB drivers are installed. See our [documentation](https://github.com/EmotiBit/EmotiBit_Docs/blob/master/Getting_Started.md#prerequisites).
4. **Retry Firmware Installation**: Follow the installation instructions again after confirming all checks above. Repeat the process a couple of times if necessary.
5. **Community Engagement**: If problems persist, document and share detailed errors with the community on the support [forum](https://forum.emotibit.com), as collaborative troubleshooting can yield results.

### Additional Notes
- For Mac users, be cautious of security prompts blocking the installation of the firmware installer. See this [relevant post](https://www.reddit.com/r/EmotiBit/comments/1iy7i2q/macos_firmware_installer_not_working/) on the forum.

### FAQs
1. **[Why is the Firmware Installer failing to install EmotiBit firmware?](https://www.reddit.com/r/EmotiBit/comments/1d3enx3/why_is_the_firmware_installer_failing_to_install/)**

---

## Emotibit Bootup Fail: SD Card Not Found

**Definition:** This category highlights the issue of EmotiBit not being able to detect the SD Card.

### Indication of this Error:
   - The red LED turning ON and then OFF during startup, indicating SD card failure. **A blinking RED LED does not fall under this category**. See documentation for EmotiBit LEDs.

### How to confirm this error**
   - "Setup failed: SD-Card not detected" message logged on the Arduino IDE Serial Monitor. See this [FAQ](https://www.reddit.com/r/EmotiBit/comments/vmtz6w/how_i_use_the_arduino_serial_monitor_with_emotibit/) for more information on using the Arduino Serial monitor.

### Solutions or Troubleshooting Steps Provided:
- **Verify Hardware Connections:** Ensure that the pins of the Feather board and EmotiBit are properly aligned and seated (no floating pins). Users may clean contact points to improve connection quality.
- **Battery Checks:** Confirm that the battery is connected and properly charged. **SD Card will not get detected if the battery is not plugged in.**
- **Replace or Test SD Cards:** Trying different branded or sized SD cards (32GB recommended).
- **Verify SD Card Format:** Ensure that the SD card is formatted as FAT32. *If you received the SD Card as a part of the EmotiBit All-in-one bundle or the Essentials Kit, then it is already in the correct format.*
- **Check Firmware Version (Only for users who programmed the feather using Arduino or PlatformIO):** Ensure the Adafruit SAMD Boards are at version 1.5.1 and confirm the [SD-Fat library version](https://github.com/EmotiBit/EmotiBit_Docs/blob/master/Keep_emotibit_up_to_date.md#install-firmware-libraries).

### FAQs
- [My EmotiBit is not detecting the SD-Card. What are my next steps?](https://www.reddit.com/r/EmotiBit/comments/1jgn44l/my_emotibit_is_not_detecting_the_sdcard_what_are/)
---

## EmotiBit Bootup Fail: Config File Parse

**Definition:** This category highlights the issue of EmotiBit failing to parse the contents of the SD Card.

### Indication of this error:
- Presence of a **solid red LED** on EmotiBit (indicating either the config file is missing or cannot be parsed). **A blinking RED LED does not fall under this issue.**


### How to confirm this error
- Serial monitor logs showing the following error: **"Failed to parse Config file contents."** See this [FAQ](https://www.reddit.com/r/EmotiBit/comments/vmtz6w/how_i_use_the_arduino_serial_monitor_with_emotibit/) for more information on using the Arduino Serial monitor.

### Solutions/Troubleshooting Steps Provided:
- **Check Configuration File:**
  - Confirm if the config file is present on the SD Card.
- **SD Card Compatibility:**
  - Recommendations to use a **32GB SD card** formatted to FAT32, as larger cards are not supported.
- For troubleshooting the config.txt file:
   - Ensure JSON formatting is correct; avoid trailing commas and validate JSON structure to prevent errors. You can even use an [online JSON format checker](https://jsonlint.com/) to validate your config file is in the correct format.

### FAQs
- ToDo: Consider adding FAQs for this issue.
---

## Emotibit Bootup Fail: Not Connecting To Wifi

**Definition:** This category highlights the issue of EmotiBit failing to parse the contents of the SD Card.

### Indication of this error
- A **solid blue LED** indicates the EmotiBit is trying to connect to the designated Wi-Fi but is unsuccessful.

### How to confirm this error
- The serial monitor will show repeated un-successful attempts, trying to connect to the WiFi network(s) listed in the config file. See this [FAQ](https://www.reddit.com/r/EmotiBit/comments/vmtz6w/how_i_use_the_arduino_serial_monitor_with_emotibit/) for more information on using the Arduino Serial monitor.

### Solutions or Troubleshooting Steps Provided:
- **Verify Wi-Fi Credentials:** Check that the SSID and password in the `config.txt` file on the SD card are correct. 
- **Network Checks:** Check that router is set to a single band (2.4GHz) for compatibility.
- **Testing Environment:** Test with a known good network (e.g., mobile hotspot) to isolate the problem.
- **Check for network restrictions:** Proactively check for any network restrictions or requirements that may prevent connection attempts, such as MAC filtering or captive portals.
- **Caution against Enterprise networks:** If you are using an Enterprise network, try connecting to a home network to verify EmotiBit functionality. If it works on a home network, then the issue may be with the Enterprise network.

### FAQs

1. **[Why isn't my EmotiBit connecting to my phone's WiFi hotspot?](https://www.reddit.com/r/EmotiBit/comments/t4hchv/why_isnt_my_emotibit_connecting_to_my_phones_wifi/)**
2. **[Help! I'm having trouble connecting to EmotiBit!](https://www.reddit.com/r/EmotiBit/comments/11hbme1/help_im_having_trouble_connecting_to_emotibit/)**
3. **[What are the available network options to use with EmotiBit?](https://www.reddit.com/r/EmotiBit/comments/11hjv49/what_are_the_available_network_options_to_use/)**

---

## EmotiBit Oscilloscope Not Detecting Emotibit

**Definition:** 
You can be stuck here **ONLY IF**
1. You have installed the EmotiBit firmware successfully.
2. The EmotiBit has successfully completed the bootup.
3. EmotiBit is connected to the network, as indicated by the blinking blue LED.
**IF YOU DO NOT SEE A BLINKING BLUE LED, PLEASE REFER THE ISSUES ABOVE.**

Once the EmotiBit has completed setup and connected to the WiFi, as confirmed by the BLUE LED blinking, the EmotiBit Oscillosocpe should be able to detect it. If the Oscillosocpe fails to detect the EmotiBit, even when the EmotiBit is connected to the WiFi, it falls in this category.

### Indication of this error
- EmotiBit hasa blinking BLUE led, but is not visible on the EmotiBit Oscilloscope.

### How to confirm this error
- ToDo: Add a positive confirmation for this isseue.
### Solutions or Troubleshooting Steps Provided:

1. **Confirm Network Compatibility**:
   - Ensure that both EmotiBit and Oscilloscope are on the **same WiFi network**, a 2.4GHz band.
   - Consider using a simple hotspot for testing purposes to rule out complex network issues.

2. **Check Firewall and Security Settings**:
   - Verify that firewall and antivirus software permissions allow communication with the EmotiBit. Disable them temporarily if necessary for testing.
   - Adjust router settings to ensure that no settings are inadvertently blocking traffic from the EmotiBit.

3. **Conduct Serial Monitor Diagnostics**:
   - Use the Arduino Serial Monitor to view live logs during connection attempts to gather data on errors or disconnection reasons.

4. **Adjust Broadcast Settings**:
   - Switch between unicast and broadcast settings in the `emotibitCommSettings.json` file, based on the network configuration that yields better connectivity.


### FAQs
1. **[Help! I'm having trouble connecting to EmotiBit!](https://www.reddit.com/r/EmotiBit/comments/11hbme1/help_im_having_trouble_connecting_to_emotibit/)**

2. **[EmotiBit Oscilloscope is not detecting EmotiBits connected to the WiFi network!](https://www.reddit.com/r/EmotiBit/comments/v75gsq/emotibit_oscilloscope_is_not_detecting_emotibits/)**

### Engaged activities
- Use EmotiBit IP Address to ping the EmotiBit
- Using Arduino Serial monitor to check logs. An `HE` (Hello EmotiBit) message is printed on the Serial.

---

## Issue Compile From Source

**Definition:** Problems encountered when compiling EmotiBit firmware from source code.

### Common Symptoms
- Missing files or libraries resulting in compilation errors (e.g., `fatal error: String.h: No such file or directory`).
  - SD card detection failures preventing successful firmware installations or uploads.
- Users trying to upload the compiled binary for the wrong MCU.

### Solution Steps
1. **Issue: Missing Package Contents**
   - Ensure all required libraries are installed through the Library Manager (e.g., `EmotiBit_ArduinoFilters` for `Filters.h`).
   - Check for specific versions of libraries mentioned in the documentation, updating where necessary. Check out [documentation](https://github.com/EmotiBit/EmotiBit_Docs/blob/master/Keep_emotibit_up_to_date.md#update-firmware-using-arduino-ide) for details.

### FAQs
1. **[Is it possible to modify the sampling rate of data streams on EmotiBit?](https://www.reddit.com/r/EmotiBit/comments/1crpxah/is_it_possible_to_modify_the_sampling_rate_of/)**

2. **[Why can I not see the Feather port on Arduino IDE to use the Serial Monitor?](https://www.reddit.com/r/EmotiBit/comments/1d3edjz/why_can_i_not_see_the_feather_port_on_arduino_ide/)**

3. **[How to increase PPG sampling rate to 100 Hz on EmotiBit (looking for .ino firmware for Arduino IDE)](https://www.reddit.com/r/EmotiBit/comments/1m17trk/how_to_increase_ppg_sampling_rate_to_100_hz_on/)**