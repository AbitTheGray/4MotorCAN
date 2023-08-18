# 3D Printer 4-Motor Board (CAN-bus Device)

This is a hobby project to create 3D Printer board to allow either control of all 4 motors (XYZ + Extruder) or 4 motors per axis.

The brain is [RP2040](https://www.raspberrypi.com/products/rp2040/) (can be flashed using USB-C connector) and has [TMC5160](https://www.trinamic.com/products/integrated-circuits/details/tmc5160/) as its muscle.
All the power and commands are provided by [CAN bus](https://en.wikipedia.org/wiki/CAN_bus) [Molex Micro-Fit 3.0 connector](https://www.molex.com/en-us/products/connectors/wire-to-board-connectors/micro-fit-connectors).
If you do not want to use CAN bus, you must provide 24V and GND on the connector and connect USB-C to your controller.

This project was not yet tested. Use at your own risk.

## Features

- [CAN bus](https://en.wikipedia.org/wiki/CAN_bus) with power (24V + 48V passthrough)
- 4x [TMC5160](https://www.trinamic.com/products/integrated-circuits/details/tmc5160/) to control motors (with build-in encoder)
- 4x SPI header for external motor encoder
- 4x Limit Switch
- RGB header
- 3x 2pin Temperature sensor (resistor)
- 4x 2pin Fan control (5V / 12V / 24V)
- Heating enable ("trigger", cannot power the heating)

Due to [JST XH connectors](https://www.jst.com/products/crimp-style-connectors-wire-to-board-type/xh-connector/) used almost everywhere, you should not esceed 3A.

[Molex Micro-Fit 3.0 connector](https://www.molex.com/en-us/products/connectors/wire-to-board-connectors/micro-fit-connectors) is limited to 8.5A (24V = 204W) which is not limited by consumption of this board but anything following it.
Make sure your whole CAN bus "network" does not exceed this value (or lower based on other passthrough boards).

You should not power any heating through CAN bus as power consumption can exceed safe limits for those connectors (and wires).
Keep in mind those limits can be lower for higher-temperature environments (like fully boxed 3D printer).

## Limits and Power Consumption

| Component                | Expected Max Current | Max Temperature |
|--------------------------|----------------------|-----------------|
| RP2040 (microcontroller) | 50 mA                | 85 °C           |
| W25Q128JVS (flash)       | 4 mA                 | 85 °C (105 °C)  |
| TMC5160 (motor driver)   |                      | 125 °C          |
| Si4532DY (MOSFET)        | 3.9 A                | 150 °C          |
