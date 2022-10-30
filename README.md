## About
[FreeRTOS](http://www.freertos.org/), ported to the
[Texas Instruments TM4C123GLX Launchpad](http://www.ti.com/tool/ek-tm4c123gxl), 
i.e. an evaluation board with the 
[TI TM4C123GH6PM](http://www.ti.com/lit/ds/symlink/tm4c123gh6pm.pdf)
microcontroller, based on ARM&#xae; Cortex-M4F.

The current version is based on FreeRTOS 10.4.0. The port will be regularly
updated with newer versions of FreeRTOS when they are released.

The port is still at an early development stage and includes only very basic
demo tasks. More complex tasks will be included in the future.


## Prerequisites
* _Tiva&#x2122; C series TM4C123GLX Launchpad_
* A _Micro-B USB cable_, usually shipped with a Launchpad
* _[GNU Arm Embedded Toolchain](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads)_,
based on GCC. See comments in _setenv.sh_ for more details about download and installation.
* _GNU Make_
* _[LM4Tools](https://github.com/utzig/lm4tools)_ or 
_[TI LMFlash Programmer](http://www.ti.com/tool/lmflashprogrammer)_ 
to upload images to the Launchpad
* Optionally _[OpenOCD](http://openocd.sourceforge.net/)_ for debugging.
See comments in _start\_openocd.sh_ for more details about installation.
* Optionally a _FTDI or PL2303HX cable supporting +3.3V based TTL level UART signals_

## Build

To build the image with the test application, just run `make` or `make rebuild`.
If the build process is successful, the image file _image.bin_ will be ready to
upload to the Launchpad.

## Run



## Application


## License
All source and header files are licensed under
the [MIT license](https://www.freertos.org/a00114.html).

For the avoidance of any doubt refer to the comment included at the top of each source and
header file for license and copyright information.
