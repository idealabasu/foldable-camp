---
title: ESP32 Installation and Setup
published: True
author: Dan Aukes
tags:
  - esp32
  - python
  - micropython
  - thonny
weight: 20
---


## Install Miniconda and packages

You need to use Python on your PC to program the ESP32.

1. install [miniconda](https://docs.conda.io/en/latest/miniconda.html) ([win64 quick link](https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe)).  Follow this [tutorial](/installing-anaconda-python/) for detailed instructions.

1. **Installing Thonny and other Packages:** Open up powershell (win+x, i) and 
    1. type ```conda install -c conda-forge wrapt```
    1. type ```pip install esptool thonny```

        **Note:** on Mac, open up terminal or xterm and type ```pip3 install esptool thonny```

## Install Device Drivers

The device drivers will help your computer recognize the ESP32 as a USB Device

1. Install [Silabs cp210x driver](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers) ([windows download](https://www.silabs.com/documents/public/software/CP210x_Universal_Windows_Driver.zip))

    _This step is required if the device is not recognized as a virtual COM port._
    
    ![Open Device Manager and Select Update Driver](00.png)

    ![Browse specific directories](01.png)

    ![Select the directory](02.png)

    ![Let it Install](04.png)

    ![Done](05.png)


## Flashing the ESP32 Firmware for MicroPython

1. download [firmware](https://micropython.org/download/esp32/) (I don't recommend v1.18, use the nightly build as it contains several more recent fixes to PWM)

1. open cmd and type ```thonny```

    ![Start Thonny](10.png)
    
1. open up tools-->options, select the "interpreter" tab and ensure that "Micropython (ESP32)" is selected.  Select the "Silicon Labs CP210X USB to UART Bridge Com(XY)" down below.

    ![Open Tools-->Options](20.png)
    
    ![Select Interpreter Tab, then the ESP32 Interpreter](30.png)
    
    ![Select the Port](40.png)
    
    ![Selection Made](50.png)

1. Before selecting ok, in the bottom right hand corner select "install or update firmware".  select the right port corresponding to the "Silicon Labs CP210X USB to UART Bridge Com(XY)"

    ![Install or Update Firmware](60.png)

1. select the firmware you downloaded, (e.g. "esp32-20220117-v1.18.bin") and hit "install".

    ![Select Firmware File](70.png)
    
    ![Hit install](80.png)

1. wait for the install to finish

    ![Done](90.png)

1. Look at the interpreter window.  You should see:

    ```
    MicroPython v1.18 on 2022-01-17; ESP32 module with ESP32
    
    Type "help()" for more information.
    >>> 
    ```

    ![Blank](100.png)
    
    
1. type ```print('hello, world!')``` into the shell and that's it!  You should have a working python interpreter loaded on your ESP32!
    
    ![Hello World!](101.png)
    

## Mac Specific Suggestions:

* use terminal or xterm if you have it as Macs do not have powershell
* use ```pip3 install ...``` instead of ```pip install ...``` with the most recent flavors of MacOS
* make sure ```pip``` or ```pip3```(Mac) is updated to avoid installation errors

    ```bash
    python3 -m pip install --upgrade pip
    ```

* Mac doesn't do COM, but can list USB devices.  In your terminal, type:

    ```bash
    ls -al /dev/tty.
    ```
    
    then unplug your ESP32 and run the previous command again to see which name for the device is the ESP32
    
* when selecting the port, there may be two Silicon Labs CP210X USB to UART Bridge (ESP device name here) devices.  Watch the messages in the terminal to determine the correct selection (obviously, don't use the one that says error/cannot find/etc.)
* when running the program you may need to press ctrl + c twice within thonny

----

## Issues

If you install on a computer where you don't have administrative access, it is still possible to install  but you have to remember a couple things:

After instlling anaconda, you must add it to your path every time you want to run it.  

1. Start --> "cmd"
 
    ```set PATH=C:\Users\<MYUSERNAME>\Miniconda3;C:\Users\<MYUSERNAME>\Miniconda3\Library\mingw-w64\bin;C:\Users\<MYUSERNAME>\Miniconda3\Library\usr\bin;C:\Users\<MYUSERNAME>\Miniconda3\Library\bin;C:\Users\daukes\Miniconda3\Scripts;%PATH%```
    
    * Replace <MYUSERNAME> with your username; confirm the path exists.
    * This step is required every time you load thonny if you installed "just for me" or are on an administratively locked pc.
    
