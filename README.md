# YKUSH Command Application


Control application for Yepkit YKUSH Switchable USB Hub boards.


Description
===========

Console application developed to illustrate the programmatic control of YKUSH family boards capabilities.
It executes one command per run, being appropriate to be executed as a console command.
But it can be easily adapted to execute a work-flow with multiple commands and we encourage you to alter it to best fit your needs.

The implementation makes use of libusb for Linux builds and hidapi for Windows.
For Linux we include a build and installation script, `build.sh` and `install.sh` respectively, for building and installing the application.


Boards Supported
================
- [YKUSH](https://www.yepkit.com/products/ykush)
- [YKUSHXS](https://www.yepkit.com/product/300115/YKUSHXS)
- [YKUSH3](https://www.yepkit.com/product/300110/YKUSH3)


Licensing
=========

The source code is licensed Apache License, Version 2.0.
Refer to [LICENSE](LICENSE.md) file.


Building
========

The steps for building on Linux and Windows are detailed bellow.


Linux
-----

For Linux `libusb-1.0` must be installed. For Debian based systems run the following.
```
sudo apt-get install libusb-1.0-0 libusb-1.0-0-dev
```
With these dependencies installed, build the application the running the following script.
```
./build.sh
```

After a successful build process you can install the ykush command in the system. To do so, run:
```
sudo ./install.sh
```

After install, the `ykushcmd` command is ready for use.



Windows
-------

To build using MinGW run the following command.

For 32bit:
```
make -f Makefile_win32
```

For 64bit:
```
make -f Makefile_win64
```

After a successful build process the executable file will be created in the `bin\Win32` or `bin\Win64` folder depending if it was the 32 or 64 bit build.



Using it
========

For details on using YKUSHCMD please refer to the [YKUSHCMD Reference Manual](https://www.learn.yepkit.com/reference/ykushcmd-reference-ykush/1/2).

```bash
# List devices connected and their serial numbers
sudo ykushcmd ykush3 -l
```

ykushcmd ykush3 [-s serial_number] [OPTION]

Where:

| cmd | detail |
| --- | --- |
-s serial_number | Board serial number to which the command is addressed. When multiple YKUSH boards are connected to a host, this option should be used to specify the board. If more than one board is connected and this option is not provided the command will be sent to the first board in the USB enumeration list. |
-l | List attached YKUSH3 boards. The serial number of each board attached to the host will be displayed.|
-d 1/2/3/a | Power Down/Off downstream port with the number provided. If a is provided as the port number then all ports will be switched.|
-u 1/2/3/a | Power Up/On downstream port with the number provided. If a is provided as the port number then all ports will be switched.|
-g 1/2/a | Get port state.|
-on	 |Switch On the 5V output power port.|
-off	|Switch Off the 5V output power port.|
-c <port-number> <config-value>	| Configure the default state of a downstream port (port-number=1/2/3/e) at power-on. The port number <e> refers to external 5V port. The default states are off (config-value=0), on (config-value=1) and persistent (config-value=2).|
-r 1/2/3	| Read GPIO with the number provided (1, 2 or 3).|
-w 1/2/3 0/1	|Write to the GPIO with the number provided (1, 2 or 3). Writing a value of 1 or 0 will drive the GPIO to logical high or low, respectively.
--reset	|Resets (reboot) the YKUSH3 board.|
--gpio enable/disable	| Enables/disables downstream port control through GPIO interface. Becomes active following a reset/re-boot.|
--bootloader-version| Prints the bootloader version number.|
--firmware-version	|Prints the board application firmware version number.|
--boot| Bring up board into bootloader mode for firmware update.|
-h |Prints help for YKUSH3 commands.|
