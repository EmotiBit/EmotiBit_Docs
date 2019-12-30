# Overview
- The [Arduino IDE](https://www.arduino.cc/en/main/software) is a perfectly good tool for making small changes to the 
    EmotiBit Firmware. If you are not going to introduce any breaking changes to the Code, we recommend you stick to Arduino IDE.
- **For the Programmers out there**, we also know how hard it can be to program using the Arduino IDE for large projects. 
    Therefore, we also want to make you aware of the fact that Visual Studio has  Plug-In for Pprogramming  Microcontrollers,
    called the Visual Micro.
  - It has a dependency on Arduino IDE, so it is essential to have Arduino IDE installed, before you can use Visual Micro, 
    but it is a much better platform to create large projects. 
## Table of Contents
- [Developing with Visual Studio + Visual Micro](#developing-with-visual-studio--visual-micro)

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
