# About
This is a tamplete project to the
Texas Instruments [TM4C123GLX Launchpad](http://www.ti.com/tool/ek-tm4c123gxl), based on ARM&#xae; Cortex&#xae;-M4F microcontrollers with [FreeRTOS&#x2122;](http://www.freertos.org/) and the [TivaWare&#x2122; Peripheral Driver Library](https://www.ti.com/lit/ug/spmu298e/spmu298e.pdf?ts=1667346399713&ref_url=https%253A%252F%252Fwww.ti.com%252Fproduct%252FTM4C123GH6PM) build with gcc compiler from the [Arm GNU Embedded Toolchain](https://developer.arm.com/downloads/-/gnu-rm)


## Setup the environment

### GCC Compiler

Download tha [Arm GNU Toochain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads). The next step is to copy to the toochain to the PATH system variable, as you can see below.

```console
foo@bar:~$ export PATH=$PATH:/home/gcc-arm-11.2-2022.02-x86_64-arm-none-eabi/bin
  ```

If you have
### TivaWare Driverlib

Download the [TivaWare Driverlib](https://www.ti.com/tool/SW-TM4C).

  ```console
foo@bar:~$ mkdir tivaware
foo@bar:~$ cd tivaware
foo@bar:tivaware$ mv <directory_downloaded>/SW-TM4C-2.1.1.71.exe
foo@bar:tivaware$ unzip SW-TM4C-2.1.1.71.exe
foo@bar:tivaware$ rm SW-TM4C-2.1.1.71.exe
foo@bar:tivaware$ export TIVAWARE_DIR=/your/tivaware/path/tivaware
```

### udev rules

```console
foo@bar:~$ echo 'ATTRS{idVendor}=="1cbe", ATTRS{idProduct}=="00fd", GROUP="users", MODE="0660"' | sudo tee /etc/udev/rules.d/99-stellaris-launchpad.rules
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
foo@bar:~$ cd ttm4c123glx_freertos_tivaware_gcc
foo@bar:tm4c123glx_freertos_tivaware_gcc$ git submodule init
Submodule 'FreeRTOS/Source' (https://github.com/FreeRTOS/FreeRTOS-Kernel.git) registered for path 'FreeRTOS/Source'
foo@bar:tm4c123glx_freertos_tivaware_gcc$ git submodule update
Cloning into '/home/nestor/tm4c123glx_freertos_tivaware_gcc/FreeRTOS/Source'...
Submodule path 'FreeRTOS/Source': checked out '44e02bff3103d7522358905f0bad8023c17a784b'
```

## Run code example

## Debug with GDB+OpenOCD in VSCode
Install [OpenOCD](https://sourceforge.net/p/openocd/code/ci/master/tree/)

```console
foo@bar:~$ git clone https://git.code.sf.net/p/openocd/code openocd-code
foo@bar:~$ cd openocd-code
foo@bar:openocd-code$ ./bootstrap
foo@bar:openocd-code$ ./configure
foo@bar:openocd-code$ make
foo@bar:openocd-code$ sudo make install
```

Install the ARM Cortex-M Debugger suport for VSCode [Cortex-Debug](https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug)


Compile the project with debug flag:
```console
foo@bar:tm4c123glx_freertos_tivaware_gcc$ make debug
```


 JSON file to debug configuration in VScode.
```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
"version": "0.2.0",
  "configurations": [
      {
        "cwd": "${workspaceRoot}",
        "executable": "${workspaceRoot}/image.elf",
        "name": "Debug Microcontroller",
        "request": "launch",
        "type": "cortex-debug",
        "servertype": "openocd",
        "serverpath": "openocd",
        "configFiles": ["/usr/local/share/openocd/scripts/board/ti_ek-tm4c123gxl.cfg"],
        "gdbTarget": "localhost:3333",
        "rtos": "FreeRTOS",
        // "device": "",
        // "interface": "",
        "showDevDebugOutput": "raw",
        "runToMain": true
      }
  ]
}

```

![VSCode debug](https://user-images.githubusercontent.com/37759765/209450878-1e33e944-96c7-45b6-9cda-cbb19d3441e6.png)
