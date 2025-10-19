# XIAO nRF52840

BLE-UART bridge for VESC using XIAO nRF52840 board.

This is a fork of https://github.com/nick133/nicenano_vesc

No major changes, made compatible with XIAO nRF52840 Tx and Rx pins (D6 (1, 11) and D7 (1, 12)).
The XIAO uses a Seeed/Adafruit-style UF2 bootloader; the Seeed builds typically bundle S140 v7.x.
This app uses S140 v6.1.1. I tried to edit the code to make it work but I did not manage to make it work.
A workaround is to d flash S140 v6.1.1 then flash the app.


## Supported board

`XIAO nRF52840`

## Build

Only x86 Linux is supported as build platform for now (tested on Ubuntu).

### Software requirements

* Nordic [nRF5 SDK v17.1.0](https://www.nordicsemi.com/Products/Development-software/nRF5-SDK/Download)
* ARM GCC toolchain, install `arm-none-eabi-gcc`, `arm-none-eabi-binutils` with your package manager

### Configure

* Set SDK_ROOT variable in Makefile to actual nRF5 SDK path, i.e.

```
SDK_ROOT := $(HOME)/.local/opt/nRF5_SDK_17.1.0_ddde560
```

* Copy nRF5 SDK toolchain configuration `Makefile.posix` to your installed SDK

```
cp -f tools/Makefile.posix $NRF_SDK/components/toolchain/gcc
```

### Compile

```
make -j8
```

## Flash

Connect XIAO nRF52840 to USB, quickly press RST button twice (for DFU mode) and:

!!!IMPORTATNT!!!

Copy s140v6.uf2 to XIAO.

Wait untill /mnt is unmounted by bootloader and quickly press RST button twice (for DFU mode) and:

```
copy nrf52840_xxaa.uf2 to XIAO.

or

make flash 
```

Wait untill /mnt is unmounted by bootloader and blinks yellow every 3.5 seconds.

## Connect to VESC

Disconnect from USB if you power nice!nano from VESC or in other case disconnect VCC/3.3V pin

| XIAO 52840 | VESC
|------------|-----------
| GND        | GND
| D7 (RX)    | TX
| D6 (TX)    | RX
| VCC/3.3V   | 3.3V
