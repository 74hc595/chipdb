# Semiconductor Packages
and how the data has to be structured in the `yaml`-file.

If a package you refer to is not listed below please add it here before using inside of a `yaml`-file.

## Available Packages


### Diode

_Not yet supported_


### Transistor

_Not yet supported_


### Single row

+ Single In-line Package (SIP or SIPP)

### Dual row

+ Dual Flat No-leads Package (DFN)
+ Dual In-line Package (DIP, DIL, DIPP, CERDIP, CDIP, PDIP, SPDIP, SDIP, EDIP)
+ Flatpack (FP)
+ Small Outline Integrated Circuit (SOIC, SO, MSOIC, SOJ, SOP, SSOP, TSOP, TSSOP)
+ Zig-zag In-line Package (ZIP)

### Quad row

+ Leadless Chip Carrier (LCC, PLCC or CLCC)
+ Quad Flat No-leads Package (QFN, QFP, MLF)
+ Quad In-line Package (QIP, QIL, QUIP or QUIL)


### Grid array

+ Ball Grid Array (BGA)
+ Embedded Wafer Level Ball Grid Array (eWLB) - _Not yet supported_
+ Land Grid Array (LGA) - _Not yet supported_
+ Pin Grid Array (PGA) - _Not yet supported_


### Wafer

_Not yet supported_


## Supported data structure

**General:**

If a pin is present but not connected or 'do not connect' use `NC`.
If a pin isn't present use `NOT_PRESENT` instead.


### Single- / Dual- / Quad row

All pins can be numbered counter clockwise (SIP and ZIP from left to right) started from the marking (little dot).
Data is an array of pins starting with pin 1.

May a special pin like a `HEATSINK` occur or a bottom plate `BOTTOM_PLATE` (only QFN).
If this is the case you can't use an array and you have to use a dictionary.
Note all not listed pins in the dictionary are `NC` by default.

See example below [ATtiny85](http://www.atmel.com/Images/atmel-2586-avr-8-bit-microcontroller-attiny25-attiny45-attiny85_datasheet.pdf):
```
  PDIP: &DIP [PB5, PB3, PB4, GND, PB0, PB1, PB2, Vcc]
  SOIC: *DIP
  TSSOP: *DIP
  QFN:
    1: PB5
    2: PB3
    5: PB4
    8: GND
    11: PB0
    12: PB1
    14: PB2
    15: Vcc
    BOTTOM_PLATE: GND
```

### Grid array

**Ball Grid Array:**

All pins can be defined by a column (letter) and a row (number).
The first pin `A1` is in the upper left corner (while viewing on top of chip).

The pins are defined in a dictionary with the position as key and the pin as value.

May a special pin like a `HEATSINK` occur.
**Note all not listed pins in the dictionary are `NOT_PRESENT` by default, not `NC`.**

See example below [DS32khz](http://datasheets.maximintegrated.com/en/ds/DS32kHz.pdf):
```
  BGA:
    A1: GND
    A2: GND
    A3: GND
    A4: V__BAT
    A5: V__BAT
    A6: GND
    A7: NC
    A8: NC
    A9: GND
    B1: GND
    B2: GND
    B3: GND
    B4: V__BAT
    B5: V__BAT
    B6: GND
    B7: NC
    B8: NC
    B9: GND
    C1: GND
    C2: Vcc
    C3: Vcc
    C4: 32khz
    C5: 32khz
    C6: GND
    C7: NC
    C8: NC
    C9: GND
    D1: GND
    D2: Vcc
    D3: Vcc
    D4: 32khz
    D5: 32khz
    D6: GND
    D7: NC
    D8: NC
    D9: GND
```


Wikipedia: [Semiconductor Package](https://en.wikipedia.org/wiki/Semiconductor_package)