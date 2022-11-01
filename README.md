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
foo@bar:~$ export PATH=$PATH:/home/nestor/Documents/littlebot/firmware/gcc-arm-11.2-2022.02-x86_64-arm-none-eabi/bin
  ```

### TivaWare Driverlib

Download the [TivaWare Driverlib](https://www.ti.com/tool/SW-TM4C).

  ```console
foo@bar:~$ mkdir tivaware
foo@bar:~$ cd tivawarePah
foo@bar:~$ mv <directory_downloaded>/SW-TM4C-2.1.1.71.exe
foo@bar:~$ unzip SW-TM4C-2.1.1.71.exe
foo@bar:~$ rm SW-TM4C-2.1.1.71.exe
foo@bar:~$ export TIVAWARE_PATH=/your/tivaware/path/tivaware
```

### lm4flash

```console
foo@bar:~$ git clone https://github.com/utzig/lm4tools.git
foo@bar:~$ cd lm4tools/lm4ﬂash
foo@bar:~$ make
foo@bar:~$ sudo cp lm4flash /usr/local/bin
```

### Clone the repository

```console
foo@bar:~$ https://github.com/NestorDP/tm4c123glx_freertos_tivaware_gcc.git
foo@bar:~$ cd tm4c123glx_freertos_tivaware
foo@bar:~$ git submodule init
Submodule 'FreeRTOS/Source' (https://github.com/FreeRTOS/FreeRTOS-Kernel.git) registered for path 'FreeRTOS/Source'
foo@bar:~$ git submodule update
Cloning into '/home/nestor/tm4c123glx_freertos_tivaware_gcc/FreeRTOS/Source'...
Submodule path 'FreeRTOS/Source': checked out '44e02bff3103d7522358905f0bad8023c17a784b'
```

## Run code example

## Debug
Install [OpenOCD](https://openocd.org/pages/getting-openocd.html)

Compile the project with debug flag:
```console
foo@bar:tm4c123glx_freertos_gcc$ make debug
```

Run OCD server:
```console
foo@bar:~$ openocd -f /usr/local/share/openocd/scripts/board/ek-tm4c123gxl.cfg
Open On-Chip Debugger 0.12.0-rc2+dev-00962-g12ce17094 (2022-10-27-21:06)
Licensed under GNU GPL v2
For bug reports, read
	http://openocd.org/doc/doxygen/bugs.html
WARNING: board/ek-tm4c123gxl.cfg is deprecated, please switch to board/ti_ek-tm4c123gxl.cfg
Info : The selected transport took over low-level target control. The results might differ compared to plain JTAG/SWD
Info : Listening on port 6666 for tcl connections
Info : Listening on port 4444 for telnet connections
Info : clock speed 21845 kHz
Info : ICDI Firmware version: 9270
Error: SRST error
Info : [tm4c123gh6pm.cpu] Cortex-M4 r0p1 processor detected
Info : [tm4c123gh6pm.cpu] target has 6 breakpoints, 4 watchpoints
Info : starting gdb server for tm4c123gh6pm.cpu on 3333
Info : Listening on port 3333 for gdb connections
```

 JSON file to debug configuration in VScode.
```json
{
"version": "0.2.0",
  "configurations": [
      {
          "name": "Launch gdb-multiarch",
          "type": "cppdbg",
          "request": "launch",
          "miDebuggerPath": "arm-none-eabi-gdb",
          "miDebuggerArgs": "-ex",
          "MIMode": "gdb",
          "program": "${workspaceFolder}/image.elf",
            "setupCommands": [
              {"text": "target remote localhost:3333"},
              {"text": "file 'image.elf'"},
              {"text": "load"},
              {"text": "break main","ignoreFailures": true}
          ],
          "launchCompleteCommand": "None",
          "externalConsole": false,
          "cwd": "${workspaceFolder}"
      }
  ]
}
```

## References
