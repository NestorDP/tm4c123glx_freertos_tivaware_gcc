# About
[FreeRTOS](http://www.freertos.org/), ported to the
[Texas Instruments TM4C123GLX Launchpad](http://www.ti.com/tool/ek-tm4c123gxl), 
i.e. an evaluation board with the 
[TI TM4C123GH6PM](http://www.ti.com/lit/ds/symlink/tm4c123gh6pm.pdf)
microcontroller, based on ARM&#xae; Cortex-M4F.

The current version is based on FreeRTOS 10.4.0. The port will be regularly
updated with newer versions of FreeRTOS when they are released.

The port is still at an early development stage and includes only very basic
demo tasks. More complex tasks will be included in the future.

git
## Setup the environment
<!-- * _Tiva&#x2122; C series TM4C123GLX Launchpad_
* A _Micro-B USB cable_, usually shipped with a Launchpad
* _[GNU Arm Embedded Toolchain](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads)_,
based on GCC. See comments in _setenv.sh_ for more details about download and installation.
* _GNU Make_
* _[LM4Tools](https://github.com/utzig/lm4tools)_ or 
_[TI LMFlash Programmer](http://www.ti.com/tool/lmflashprogrammer)_ 
to upload images to the Launchpad
* Opt  -->

### ARM GCC Compiler

Download tha [ARM Gnu Toochain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads). The next step is to copy to the toochain to the PATH system variable, as you can see below.

```console
~$ export PATH=$PATH:/home/nestor/Documents/littlebot/firmware/gcc-arm-11.2-2022.02-x86_64-arm-none-eabi/bin
  ```


### TivaWare Driverlib

  ```console
~$ mkdir <TivaWarePah>
~$ cd <TivaWarePah>
~$ mv <directory_downloaded>/SW-TM4C-2.1.1.71.exe
~$ unzip SW-TM4C-2.1.1.71.exe
~$ rm SW-TM4C-2.1.1.71.exe
~$ export TIVAWARE_PATH=/your/tivaware/path
```

### lm4flash

```console
~$ git clone https://github.com/utzig/lm4tools.git
~$ cd lm4tools/lm4ﬂash
~$ make
~$ sudo cp lm4flash /usr/local/bin
```

### Clone the repository

```console
~$ https://github.com/NestorDP/tm4c123glx_freertos_tivaware_gcc.git
~$ cd tm4c123glx_freertos_tivaware
~$ git submodule init
~$ git submodule update
```

## Run code example

## Debug

## References
