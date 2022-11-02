# About
This is a tamplete project to the
Texas Instruments [TM4C123GLX Launchpad](http://www.ti.com/tool/ek-tm4c123gxl), based on ARM&#xae; Cortex&#xae;-M4F microcontrollers with [FreeRTOS&#x2122;](http://www.freertos.org/) and the [TivaWare&#x2122; Peripheral Driver Library](https://www.ti.com/lit/ug/spmu298e/spmu298e.pdf?ts=1667346399713&ref_url=https%253A%252F%252Fwww.ti.com%252Fproduct%252FTM4C123GH6PM) build with gcc compiler from the [GNU Arm Embedded Toolchain](https://developer.arm.com/downloads/-/gnu-rm)


## Setup the environment

### ARM GCC Compiler

Download tha [ARM Gnu Toochain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads). The next step is to copy to the toochain to the PATH system variable, as you can see below.

```console
foo@bar:~$ export PATH=$PATH:/home/gcc-arm-11.2-2022.02-x86_64-arm-none-eabi/bin
  ```

### TivaWare Driverlib

Download the [TivaWare Driverlib](https://www.ti.com/tool/SW-TM4C).

  ```console
foo@bar:~$ mkdir tivaware
foo@bar:~$ cd tivawarePah
foo@bar:tivaware$ mv <directory_downloaded>/SW-TM4C-2.1.1.71.exe
foo@bar:tivaware$ unzip SW-TM4C-2.1.1.71.exe
foo@bar:tivaware$ rm SW-TM4C-2.1.1.71.exe
foo@bar:tivaware$ export TIVAWARE_DIR=/your/tivaware/path/tivaware
```

### lm4flash

```console
foo@bar:~$ git clone https://github.com/utzig/lm4tools.git
foo@bar:~$ cd lm4tools/lm4ﬂash
foo@bar:lm4ﬂash$ make
foo@bar:lm4ﬂash$ sudo cp lm4flash /usr/local/bin
```

### Clone the repository

```console
foo@bar:~$ https://github.com/NestorDP/tm4c123glx_freertos_tivaware_gcc.git
foo@bar:~$ cd tm4c123glx_freertos_tivaware
foo@bar:tm4c123glx_freertos_tivaware$ git submodule init
Submodule 'FreeRTOS/Source' (https://github.com/FreeRTOS/FreeRTOS-Kernel.git) registered for path 'FreeRTOS/Source'
foo@bar:tm4c123glx_freertos_tivaware$ git submodule update
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
