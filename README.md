# nicenano_vesc

BLE-UART bridge for VESC using nice!nano board.

This is a fork of https://github.com/vedderb/nrf52_vesc

No major changes, the code is cleaned, compilation errors were fixed, some improvements were added
for ease of use.

## Supported board

`nice!nano v2` compatible chinese clone also can be found as `ProMicro nRF52840` or `SuperMini nRF52840`.
It's cheap, small and easy to flash - just copy firmware to USB storage, no additional tools needed.

* Buy it from [Aliexpress](https://www.aliexpress.com/w/wholesale-nice-nano-v2-nfr52840-board.html)
* Exact board is described [here](https://kriscables.com/supermini-nrf52840/)
* Board [wiki](https://github.com/joric/nrfmicro/wiki/Alternatives#supermini-nrf52840)
* Original nice!nano v2 [schematic](https://nicekeyboards.com/docs/nice-nano/pinout-schematic)

## Build

Only x86 Linux is supported as build platform for now (tested on Artix).

### Software requirements

* Nordic [nRF5 SDK v17.1.0](https://www.nordicsemi.com/Products/Development-software/nRF5-SDK/Download)
* ARM GCC toolchain, install `arm-none-eabi-gcc`, `arm-none-eabi-binutils` with your package manager

### Configure

* Set `NRF_SDK` environment variable to your nRF5 SDK path or set it in the `Makefile`

```
NRF_SDK=$HOME/.local/opt/nRF5_SDK_17.1.0_ddde560
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

Connect nice!nano to USB, quickly short RST pin to GND twice (for DFU mode, red LED should be ON) and:

```
make flash
```

Wait untill /mnt is unmounted by bootloader and red LED is OFF.

## Connect to VESC

Disconnect from USB if you power nice!nano from VESC or in other case disconnect VCC/3.3V pin

| nice!nano  | VESC
|------------|-----------
| GND        | GND
| P0.11 (RX) | TX
| P0.8 (TX)  | RX
| VCC/3.3V   | 3.3V
