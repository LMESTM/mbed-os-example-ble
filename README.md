# BLE Examples running on STM32WB55RG - development branch

This branch is a temporary branch of the mbed-os-example-ble to make early
trails with NUCLEO_WB55RG before NUCLEO_WB55RG is officially merged and
released in mbed-os.

# Modifications:

Selection of mbed-os dev_NUCLEO_WB55RG branch in mbed-os.lib files.

# WB55RG Pre-requisite

You need a NUCLEO_WB55RG board, officially named  [p-nucleo-wb55](https://www.st.com/content/st_com/en/products/evaluation-tools/product-evaluation-tools/stm32-nucleo-expansion-boards/p-nucleo-wb55.html)

<span> Please upgrade STlink firmware to the latest version. Visit https://www.st.com/en/development-tools/stsw-link007.html

Also See mbed-os [pre-requisites](https://github.com/LMESTM/mbed-os-example-ble#pre-requisites).

# Running examples

__To build an example:__

1. Clone the repository containing the collection of examples:

	```
	$ git clone https://github.com/ARMmbed/mbed-os-example-ble.git
	```

	**Tip:** If need to have git installed

1. Using a command-line tool, select this STM32_WB55RG development branch:
	$ cd mbed-os-example-ble
    $ git remote add wb55rg https://github.com/LMESTM/mbed-os-example-ble
    $ git fetch wb55rg
    $ git checkout wb55rg/dev_NUCLEO_WB55RG


1. Then navigate to any of the example directories, like BLE_Beacon:

	```
	$ cd BLE_Beacon
	```

1. Update the source tree:

	```
	$ mbed deploy
	```

1. Compile with your favorite toolchain:

	```
	$ mbed compile -t ARM -m NUCLEO_WB55RG
    $ mbed compile -t GCC_ARM -m NUCLEO_WB55RG
	```

1. Copy the binary to the Mas Storage corresponding to the NUCLEO board (check
   the drive name on your computer, D:/ in the example here)

    ```
	$ cp ".\BUILD\NUCLEO_WB55RG\ARM\BLE_BatteryLevel.bin" /D/
	```

1. Check the example readme.md to understand how the example works.


# Test results

* BLE_BatteryLevel/
    When connecting to the device, the connection will fail or the Generic
    Attribute will show "Service Changed" instead of the expected attributes.

    This can work fine with earlier version of the mbed-os-example.

* BLE_Button/
Could not Scan the device.

* BLE_Beacon/

* BLE_GAPButton/
Not tested yet.
* BLE_GattServer/
Not tested yet.
* BLE_LED/
Not tested yet.
* BLE_PeriodicAdvertising/
Not tested yet.
* BLE_SM/
Not tested yet.
* BLE_Beacon/
Not tested yet.
* BLE_GAP/
Not tested yet.
* BLE_GattClient/
Not tested yet.
* BLE_HeartRate/
Not tested yet.
* BLE_LEDBlinker/
Not tested yet.
* BLE_Privacy/
Not tested yet.
* BLE_Thermometer/


# BLE Examples
This repo contains a collection of BLE example applications based on
mbed OS and built with [mbed-cli](https://github.com/ARMmbed/mbed-cli). Each example subdirectory contains a separate mbed-cli module meant for building an executable.

Please browse to subdirectories for specific documentation.

# End of temperary NUCLEO_WB55RG documentation


Getting Started
===============


Pre-Requisites
--------------

To build these examples, you need to have a computer with software installed as described [here](https://os.mbed.com/docs/latest/tools/index.html).

In order to use BLE in mbed OS you need one of the following hardware combinations:

* A STM32WB-based board such as [NUCLE_WB55RG](https://os.mbed.com/platforms/ST-Nucleo-WB55RG/)
* A Nordic nRF51-based board such as [nrf51dk](https://www.nordicsemi.com/eng/Products/nRF51-DK) or [mkit](https://www.nordicsemi.com/eng/Products/Bluetooth-R-low-energy/nRF51822-mKIT).
* A Nordic nRF52-based board such as [nrf52DK](https://os.mbed.com/platforms/Nordic-nRF52-DK/)
* A supported target, such as the [NUCLEO-F401RE](http://www.st.com/en/evaluation-tools/nucleo-f401re.html), with a BLE shield or an external BLE peripheral, such as an [ST shield](http://www.st.com/web/catalog/tools/FM116/SC1075/PF260517).
* A [DISCO_L475VG_IOT01A (ref B-L475E-IOT01A)](http://www.st.com/en/evaluation-tools/b-l475e-iot01a.html) board.


The [BLE documentation](https://os.mbed.com/docs/latest/reference/bluetooth.html) describes the BLE APIs on mbed OS.

Targets for BLE
---------------

The following targets have been tested and work with these examples:

* Nordic:
	* NRF51_DK
	* NRF52_DK

* Boards with an ST shield plugged in:
	* K64F
	* NUCLEO_F401RE

* STMicroelectronics:
    * NCULEO_WB55RG 
	* DISCO_L475VG_IOT01A (ref B-L475E-IOT01A)

	<span> **Important:** if an ST shield is used with the K64F board, an hardware is patch required. Check out https://developer.mbed.org/teams/ST/code/X_NUCLEO_IDB0XA1/ for more information.</span>

### Using ST Nucleo shield on other targets

It is possible to use the ST Nucleo shield on boards not directly supported by these examples as long as the board has an Arduino UNO R3 connector.

To makes the board compatible with the ST shield three things are required:
* Add the BLE feature to your target.
* Add the BLE implementation for the ST shield to the list of modules which have to be compiled.
* Indicate to the BLE implementation that your board use an Arduino connector.

All these operations can be done in the file `mbed_app.json` present in every example.

In the section `target_overrides` add a new object named after your target.
In this object two fields are required:
* `"target.features_add": ["BLE"]` Add the BLE feature to the target.
* `"target.extra_labels_add": ["CORDIO", "CORDIO_BLUENRG"]`: Add the BLE implementation of the ST shield to the list of the application modules.

As an example, this is the JSON bit which has to be added in the `target_overrides` section of `mbed_app.json` for a `NUCLEO_F411RE` board.

```json
        "NUCLEO_F411RE": {
            "target.features_add": ["BLE"],
            "target.extra_labels_add": ["CORDIO", "CORDIO_BLUENRG"]
        },
```

<span> **Note:** You can get more information about the configuration system in the [documentation](https://os.mbed.com/docs/latest/reference/configuration.html)</span>

<span> **Important:** It is required to apply an hardware patch to the ST shield if it is used on a board with an Arduino connector. Check out https://developer.mbed.org/teams/ST/code/X_NUCLEO_IDB0XA1/ for more information.</span>


Building and testing the examples
---------------------------------

__To build an example:__

1. Clone the repository containing the collection of examples:

	```
	$ git clone https://github.com/ARMmbed/mbed-os-example-ble.git
	```


	**Tip:** If you don't have GitHub installed, you can [download a zip file](https://github.com/ARMmbed/mbed-os-example-ble/archive/master.zip) of the repository.

1. Using a command-line tool, navigate to any of the example directories, like BLE_Beacon:

	```
	$ cd mbed-os-example-ble
	$ cd BLE_Beacon
	```

1. Update the source tree:

	```
	mbed deploy
	```

1. Run the build:

	```mbed compile -t <ARM | GCC_ARM> -m <YOUR_TARGET>```

__To run the application on your board:__

1. Connect your mbed board to your computer over USB. It appears as removable storage.

1. When you run the ``mbed compile`` command, as you did above, mbed cli creates a BIN or an HEX file in a ```BUILD/<target-name>/<toolchain>``` directory under the example's directory. Drag and drop the file to the removable storage.


Exactly which executables are generated depends on the target that you have
chosen. For Nordic Semiconductor targets, the following .hex files will be present:

 * `<module_name>.hex` is the one which can be flashed to the target.
 * `<module_name>.elf` is an ELF binary containing symbols (useful for debugging).

**Note:** Depending on the build process, the file which has to be flashed on a Nordic target can also be named `<module_name>-combined.hex`. If `<module_name>-combined.hex` and `<module_name>.hex` are present in the build directory, flash `<module_name>-combined.hex.

**Note:** On non Nordic targets, the file to flash can also be named `<module_name>.bin`. Refer to mbed-cli, mbed-os and your board vendor documentation for more informations.


Known issues
============

* [NUCLEO_F411RE]: Some BLE examples doesn't work with the X-NUCLEO BLE shield. See [#40](https://github.com/ARMmbed/mbed-os-example-ble/issues/40)
* [NRF5] Impossible to debug or flash the examples with IAR: See [#39](https://github.com/ARMmbed/mbed-os-example-ble/issues/39)

### License and contributions

The software is provided under Apache-2.0 license. Contributions to this project are accepted under the same license. Please see contributing.md for more info.

This project contains code from other projects. The original license text is included in those source files. They must comply with our license guide
