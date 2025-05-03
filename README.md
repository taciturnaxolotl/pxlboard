# PxlBoard

<img src="https://cachet.dunkirk.sh/emojis/SK6812RGBW/r" width="150" align="right">

> ### More deets coming never 😊
> **Y**et **A**nother **G**eneric **N**eopixel **G**rid (**YAGNG**) except this one is mine so don't you dare dis it :kirby-gun:

## BOM

| Part | Quantity | Price | Link | Description | Notes |
| --- | --- | --- | --- | --- | --- |
| PCB (OSHPark) | 1 | $44.05 | [OSHPark](https://oshpark.com) | Custom PCB - Purple | Most expensive option but also looks gorgeous |
| PCB (JLCPCB) | 1 | $24.82 | [JLCPCB](https://jlcpcb.com) | Custom PCB - Green | Mid-range price |
| PCB (PCBWay) | 1 | $12.80 | [PCBWay](https://pcbway.com) | Custom PCB - Various colors | Most affordable option (kinda suprisingly?) |
| Seeed XIAO RP2040 | 1 | $3.99 | [Seeed Studio](https://www.seeedstudio.com/XIAO-RP2040-v1-0-p-5026.html) | Microcontroller board | Brain of the operation |
| SK6812 LEDs | 65 | $6.40 | [LCSC](https://www.lcsc.com/product-detail/RGB-LEDs-Built-in-IC_OPSCO-Optoelectronics-SKC6812RGBW-WS-B_C5380879.html?s_z=n_rgbw) | RGB addressable LEDs | $0.0985 each, forms the 8x8 grid |
| LIS3DHTR Accelerometer | 1 | $0.60 | [LCSC](https://www.lcsc.com/product-detail/Accelerometers_STMicroelectronics-LIS3DHTR_C15134.html?s_z=n_LIS3DHTR) | 3-axis accelerometer | For motion detection |
| Capacitor 100nF - ceramic | 20 (min size) | $0.29 | [LCSC](https://www.lcsc.com/product-detail/Multilayer-Ceramic-Capacitors-MLCC-SMD-SMT_Samsung-Electro-Mechanics-CL31B104KBCNNNC_C24497.html?s_z=n_1206%2520100nf) | 1206 package | Decoupling capacitor |
| Capacitor 10nF - electrolytic | 100 (min size) | $0.13 | [LCSC](https://www.lcsc.com/product-detail/Multilayer-Ceramic-Capacitors-MLCC-SMD-SMT_Samsung-Electro-Mechanics-CL05B103KB5NNNC_C15195.html?s_z=n_10nf%25200402) | 0402 package | Decoupling capacitor |

Total (with pcbway): ~$24.21

## Schematics

> coming soon but in the meantime take a look at my keyboard blueprint :yay: or I suppose if you are really impatient you can use [kicanvas](https://kicanvas.org/?github=https%3A%2F%2Fgithub.com%2Ftaciturnaxolotl%2Fpxlboard%2Fblob%2Fmain%2Fkicad%2Fpxlboard.kicad_pro)

![schematic](https://raw.githubusercontent.com/taciturnaxolotl/thyme/main/.github/images/blueprint.svg)

## Build Notes

Nothing yet

## Pinout & Wiring Diagram

### XIAO RP2040 Connections

| XIAO Pin | Connected To | Description |
| --- | --- | --- |
| D0/GPIO26/A0 | - | Unused |
| D1/GPIO27/A1 | - | Unused |
| D2/GPIO28/A2 | - | Unused |
| D3/GPIO29/A3 | - | Unused |
| D4/GPIO6/SDA | LIS3DHTR SDA | I2C Data Line |
| D5/GPIO7/SCL | LIS3DHTR SCL | I2C Clock Line |
| D6/GPIO0/TX | - | Unused |
| D7/GPIO1/RX | NEOPIXEL_SIG | LED Data In |
| D8/GPIO2/SCK | - | Unused |
| D9/GPIO4/MISO | - | Unused |
| D10/GPIO3/MOSI | - | Unused |
| 3V3 | LIS3DHTR VDD_IO | 3.3V Power |
| GND | LIS3DHTR GND, LEDs GND | Ground |
| 5V | LEDs VDD | 5V Power |

### LIS3DHTR Accelerometer

| LIS3DHTR Pin | Connected To | Description |
| --- | --- | --- |
| VDD | 3.3V | Power Supply |
| VDD_IO | 3.3V | Interface Power |
| GND | GND | Ground |
| SDA | XIAO D4 | I2C Data |
| SCL | XIAO D5 | I2C Clock |
| INT1 | - | Interrupt (not used) |
| INT2 | - | Interrupt (not used) |

### Wiring Diagram

```mermaid
graph TD
    XIAO[XIAO RP2040] -- SDA --> LIS3D[LIS3DHTR Accelerometer]
    XIAO -- SCL --> LIS3D
    XIAO -- 3.3V --> LIS3D
    XIAO -- GND --> LIS3D

    XIAO -- 5V --> LEDS[SK6812 LED Grid]
    XIAO -- GND --> LEDS
    XIAO -- D7/GPIO1 --> LEDS

    LEDS -- Data chain --> LED1[LED #1]
    LED1 --> LED2[LED #2]
    LED2 --> LED3[LED #3]
    LED3 --> DOT["..."]
    DOT --> LED64[LED #64]

    classDef mcu fill:#f96,stroke:#333,stroke-width:2px;
    classDef sensor fill:#bbf,stroke:#33f,stroke-width:1px;
    classDef led fill:#9f9,stroke:#3a3,stroke-width:1px;

    class XIAO mcu;
    class LIS3D sensor;
    class LEDS,LED1,LED2,LED3,LED64 led;
```

### Capacitor Placement

- 100nF ceramic capacitor between VDD and GND of LIS3DHTR
- 10nF ceramic capacitors for each SK6812 LED (placed close to power pins)

<p align="center">
	<img src="https://raw.githubusercontent.com/taciturnaxolotl/carriage/master/.github/images/line-break.svg" />
</p>

<p align="center">
	<i><code>&copy 2025-present <a href="https://github.com/taciturnaxolotl">Kieran Klukas</a></code></i>
</p>

<p align="center">
	<a href="https://github.com/taciturnaxolotl/pxlboard/blob/master/LICENSE.md"><img src="https://img.shields.io/static/v1.svg?style=for-the-badge&label=License&message=MIT&logoColor=d9e0ee&colorA=363a4f&colorB=b7bdf8"/></a>
</p>
