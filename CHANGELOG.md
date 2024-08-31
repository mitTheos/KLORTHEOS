# CHANGELOG
28/08/2024
-  While playing with QMK I have noticed that the original 1.3 design carried a wiring flaw on the minijack footprint and PCB traces. The RX/TX are symetrical between the two sides which makes it impossible to define the transmission protocol in QMK as serial full duplex with RP2040 ProMicro boards if you don't specify a pin swap command. By default the stock firmware uses bitbang driver on a single pin which is not optimal and made the use of a TRRS link unnecessary as 3 pins cable would suffice. If you use these boards you should set the following in the config.h for QMK if using RP2040 ProMicro boards.
      
                  //Full Duplex communication
                  #define SERIAL_USART_TX_PIN GP4     // USART TX pin
                  #define SERIAL_USART_RX_PIN GP1     // USART RX pin
                  #define SERIAL_USART_FULL_DUPLEX
                  #define SERIAL_USART_PIN_SWAP

-  In case your MCU can only use a single pin for communications, it is recommended to use half duplex serial instead of bitbang.
      
                  //Half Duplex communication
                  //#define SERIAL_USART_TX_PIN GP4     // USART TX pin
       
-  More about this matter [here](https://docs.qmk.fm/drivers/serial)

27/08/2024
-  Validation of the alternative haptic module. You may now add it to your existing board. It is working great
-  Did some minimal tracks cleanup on all versions with Kicad cleanup tools. It was mainly some unmerged tracks.
-  Moved all files to Kicad 8 version. Please upgrade your version if required.
-  At the request of some users of the community I have made an initial "special" low profile version for KS33/V2 Gateron switches with south facing LED. Beware that this version is untested yet in terms of production validation. It will most likely be fabricated by JLCPB as it clears DRC, but I haven't assembled one yet. Also keep in mind the following points :

    - There will be some interferences with the haptic module as there is no way I can move it up sufficiently on the existing PCB cutout. I would have to redesign the top corner which would impact enclosure compatibility. Haptic module can be mounted but it will have to be a little bit spaced from the back of the PCB to clear the switch socket.
    - I have moved the puck mounting holes up a little bit. It now sits in between the 1.3 and 1.4 positions
    - Because the KS33 hotswaps have a very diferent pinout compared with standard Cherry, they don't play as well with the recto-verso design of the KLOR. In particular you may find to lack a little bit of soldering surface on the right pad. It should be just enough to solder the pad. This is due to the pad interfering with the other side hole. Nothing I can do here apart from duplicating the design for right and left sides.
    - Obviously you will need some Gateron low profile V2 hotswap sockets for this version (compatible with Gateron KS33/V2 low profile type switches). These are easilly obtainable on Aliexpress I use them for another project.Only Gateron low profile V2 sockets can be used. No other brands will work on this design.

23/08/2024
-  Upddated FIRMWARE directory with working config files for QMK for RP2040 and ZMK for NiceNanoV2. These are not perfect but both firmware compile without errors and have the maximum functionalities enabled by default.
-  Added precompiled [qmk](https://github.com/Lefuneste83/KLOR/tree/main/FIRMWARE/Ready-to-flash/qmk-RP2040) and [zmk](https://github.com/Lefuneste83/KLOR/tree/main/FIRMWARE/Ready-to-flash/zmk-NiceNanoV2) firmware
-  Added link for a [full polydactyl layout](http://www.keyboard-layout-editor.com/#/gists/49ff09e68b46feb39760467424a4601a) on the layout editor website

09/08/2024
- Correction of a 0.45 mm interference between hot swap socket and bottom of haptic buzz module. The module has been moved upwards by 0.6 mm to clear the interference for those willing to install the stock haptic module.
- An alternative design for a DIY haptic module is included if you can get a DRV2605LDGSR driver chip and a ELV1411A linear motor. Hot air/plate soldering is required. This module is 0.8 mm shorter so there will definitely be no interference whatever version of PCB you have. Attachment hole placment is unchanged relative to motor and pins locations in order to preserve mechanical compatibility. I recommend a thinner PCB (1.2 mm) for this module.

07/08/2024
-  Production validation of the new design. Full build completed and tested. Current Paste Layers are functionnal for those willing to order stencils.

25/07/2024
-  Initial commit with refactored PCB design for SK6812 Mini-E South facing ARGB LEDs

30/07/2024
-  Correction to SMD footprints for Paste Layers for diodes, reset switch and speaker.
-  ZMK Firmware modifications in order to be able to set per rotation pulses for each encoder. Both encoders work as expected. RGB light has been enabled by default as well.

--> If you intend to generate your own gerbers instead of the ones provided, make sure to process drill files AND flag the "Substract soldermask layer from copper pads" option (otherwise the KLOR Logo will superimpose on some of the SMD pads rendering soldering impossible without manual scratching of the covered pads). Guess how I know...
