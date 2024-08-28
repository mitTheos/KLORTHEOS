# FIRMWARE
My version of ZMK firmware  with Github Actions pipeline is located here:
https://github.com/Lefuneste83/zmk-config-klor
It has both encoders working, precise pulse per rotation adjustments and RGB enabled by default.

Config files for both QMK and ZMK can be found here:
https://github.com/Lefuneste83/KLOR/tree/main/FIRMWARE

For extra convienence if you intend to modify your firmware for a smaller layout, I have created a link to a [polydactyl layout](http://www.keyboard-layout-editor.com/#/gists/49ff09e68b46feb39760467424a4601a) on the layout editor website.

****

BREAKING CHANGE! While playing with QMK I have noticed that the original 1.3 design carried a wiring flaw on the minijack footprint and PCB traces. The RX/TX are symetrical between the two sides which makes it impossible to define the transmission protocol in QMK as serial full duplex with RP2040 ProMicro boards. By default the stock firmware uses bitbang driver on a single pin which is not optimal. Also this made the use of a TRRS link unnecessary as 3 pins cable would suffice. So I definitely think this is an overlook of the original design. Maybe this was necessary for use of Atmel MCU and even though I doubt it. Anyways this has been corrected on the PCB of 1.4 and 1.4 LP KS33 but NOT on the 1.3 design provided on this fork. So from now on if you use these boards you will need to make sure you have set the following in the config.h in case you use RP2040 which is the recommended board for QMK:

                 #define SERIAL_USART_FULL_DUPLEX    // Enable full duplex operation mode.
                 #define SERIAL_USART_TX_PIN GP1     // USART TX pin
                 #define SERIAL_USART_RX_PIN GP4     // USART RX pin
As this breaking change forces me to break the wiring symetry for these pins you need to make sure you solder the minijack accordingly.You should solder them both on top or both on the bottom but both sides must be the same top or bottom. This makes sure your TX1 goes to RX2 and RX1 goes to TX2. Otherwise you'll end up with a symetrical pinout again which is not deadly by any means but requires the use of half duplex or stock bitbang protocols.

Older commits of the 1.4 version can use the following to enable half duplex serial communication which is not optimal but better than stock bitbang. you also have to disable reference to #define SOFT_SERIAL_PIN which defines the bitbang mode. Bitbang driver is not desirable as it brings some CPU overhead.

                 #define SERIAL_USART_TX_PIN GP1     // USART TX pin
I have differentiated the uf2 firmware images. This does not impact ZMK which uses BLE for split keyboards communication.

More about this matter [here](https://docs.qmk.fm/drivers/serial)
