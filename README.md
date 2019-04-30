HFS 4011s PCB Design Files
=====
# Development Guide
### Software
PCB design software (EAGLE) can be downloaded [here](https://www.autodesk.com/education/free-software/eagle).

Tutorials:

[Schematic design tutorial](https://learn.sparkfun.com/tutorials/using-eagle-schematic/all)

[Creating device footprints](https://learn.sparkfun.com/tutorials/designing-pcbs-smd-footprints)

[Advanced layout](https://learn.sparkfun.com/tutorials/designing-pcbs-advanced-smd)

### Useful links
The ESP32 and USB design follows the same format as the
[HUZZAH32 ESP32 Feather](https://github.com/adafruit/Adafruit-HUZZAH32-ESP32-Feather-PCB),
so check out their [documentation](https://learn.adafruit.com/adafruit-huzzah32-esp32-feather/overview)
for programming the board using the Arduino IDE.

The battery charge design follows the same format as the [PowerBoost 500](https://github.com/adafruit/Adafruit-PowerBoost-500-Charger-PCB).
An overview can be found [here](https://learn.adafruit.com/adafruit-powerboost-500-plus-charger/overview).

# Usage
This board is meant to interface with an FPAA board developed at the Georgia
Institute of Technology and serves as part of an overall noise cancellation
pipeline meant to showcase the versatility of this technology. Our board handles
sending music and measured noise over to the FPAA, and the FPAA incorporates
our noise cancellation algorithm and sends its output to connected speakers.

This board, denoted as the HFS-4011s mainboard, includes circuitry for regulating
the battery supply voltage to 5V and 3.3V, handles charging the battery from a
micro-USB connector, and handles programming the onboard ESP32 via micro-USB.

The ESP32 is set up to connect to buttons for controlling the ANC state. A 5V
logic level SPI interface is set up and is meant to interface with LEDs to show
headphone status. The mainboard also contains a 16-bit DAC for converting the
received music to an analog signal to send over to an FPAA or speakers.

There are also a few onboard LEDs for debugging and status verification.

* LED1 is green if the battery is fully charged
* LED2 is orange if the battery is currently charging
* PWR is a power indicator LED and is blue if 5V is output from the regulator.
* LBO is a battery status indicator LED and is red if the battery is discharged.
* D2 is a red LED connected to GPIO13 meant for debugging.

Even with solder paste, this board can be hard to assemble by hand. We ran into
a lot of problems regarding unintended shorts from the reflow process. If removing
the USB-UART bridge is necessary, the ESP32 can be programmed normally through
pins 34 and 35 (u0RXD and u0TXD respectively), but when you get to the
`Connecting...` stage, make sure the following protocol is followed:

* Short GPIO2 and GPIO0 to ground.
* Press the RESET button (SW1), which is connected to the ESP32 EN pin, to
momentarily reset the microcontroller. Pressing SW1 shorts the EN pin to ground,
so this can be done manually as well.

After a couple of moments, the ESP32 should be flashed. The RESET button needs
to be pressed again to cycle the ESP32, and the flashed program should now run.
