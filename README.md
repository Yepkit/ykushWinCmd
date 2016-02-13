# ykushWinCmd


Control utility for Yepkit YKUSH Switchable USB Hub board.


Description
===========

The *ykushWinCmd* is a console application developed to illustrate the programmatic control of YKUSH capabilities.
It executes one command per run being appropriate to be executed as a console command.
But it can be easily adapted to execute a work-flow with multiple commands and we encourage you to alter it to best fit your needs.

The core of the application is consolidated in two source code files, the *commandParser.cpp* and the *usbcom.cpp*.
The first contains the work-flow control and the second the communication functions.

This implementation makes use of hidapi open-source library which is portable across several operating systems.
We included a Visual Studio solution file for building in Windows. For Linux we included a Makefile for building the application.
Note that hidapi is not included in the source code and has to be obtained beforehand.


Licensing
=========

The *ykushWinCmd* source code is licensed under MIT license. 
Refer to [LICENSE](LICENSE.md) file.


Building
========

Before building the application we need to get the [hidapi library](http://www.signal11.us/oss/hidapi/) and build it.
Follow the instructions in the hidapi documentation for building the library in the several systems. 

After building the hidapi library we need to include the relevant hidapi files to our *ykushWinCmd* project. 
Once this is done the *ykushWinCmd* application can be built.

The steps for Windows and Linux are detailed bellow.

Windows
-------
Copy to `ykushWinCmd\ykushWinCmd\windows\` the following hidapi library files:
- hidapi.dll
- hidapi.exp
- hidapi.lib

also copy the *hidapi.dll* to `ykushWinCmd\bin\`.

Open the `ykushWinCmd\ykushWinCmd.sln` with Microsoft Visual Studio and build the solution.
If the build process is successful the executable file will be created in the`ykushWinCmd\bin\` folder.

The next step is to make the dynamically linked library accessible to executable.
We can install the hidapi.dll in the system or ensure that a copy of the file is in the same folder than the ykush.exe.


Linux
-----
Copy to `ykushWinCmd/ykushWinCmd/linux/` the *libhidapi-hidraw.so* or the *libhidapi-libusb.so*, depending if the hidraw or the libusb back-end is to be used.

Next, in the `ykushWinCmd/ykushWinCmd/`, run `make` to build the application.
If the build process is successful the ykush executable will bi in the `ykushWinCmd/bin/` folder.

The next step is to make the shared library accessible to executable.
We can install the *libhidapi-hidraw.so* or the *libhidapi-libusb.so*, depending if the hidraw or the libusb back-end is to be used, in a system folder (e.g., /usr/lib/) or set the environment variable *LD_LIBRARY_PATH* with the path to the library file.


Using it
========

Windows
-------
Navigate to the `ykushWinCmd\bin\` folder and run `ykush.exe -h` to print all the available command options a syntax.

Let's look at some command examples.

Assuming that just one YKUSH board is connected to our host, if we wanted to turn **OFF** the downstream port 1 we would issue the following command.
```
ykush.exe -d 1
```

Similarly, if we wanted to turn the downstream 1 back **ON** we would issue the following command.
```
ykush.exe -u 1
```

Assuming that two YKUSH boards are connected to our host and we wanted to turn **OFF** the downstream port 1 of one specific board. 
To accomplish this we need to address the command by the YKUSH board **serial number**. 
To find out the boards serial number we can issue the following command.
```
ykush.exe -l
```
This will print the serial number of all YKUSH boards attached to the host.
Assuming the our board had the serial number YK1234567, we would issue the following command.
```
ykush.exe -s YK1234567 -d 1
```
This would turn **OFF** the downstream port 1 of the board with the serial number YK12345.


Linux
-----
For Linux the command options and syntax are the same with the slight difference that the executable file does not have the `.exe` extension.
Also depending of your user permissions you may need to precede the command with the *sudo* directive (e.g, `sudo ykush -d 1`).


For more information and resources for the YKUSH board please visit the [yepkit website ykush page](https://wwww.yepkit.com/ykush).









