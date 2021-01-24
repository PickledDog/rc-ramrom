# rc-ramrom
 Pageable RAM/ROM card for RC2014

## Overview
This RC2014-compatible board provides both ROM and RAM in a single card. ROM comes from an EPROM or EEPROM, with 8k/16k/32k granularity, and RAM is provided by a 128k x 8 SRAM. The ROM can be paged out and replaced by RAM.

## Memory details
For ROM, multiple EPROM and EEPROM chips are supported (8K through 64K from the 27Cxx and 28Cxx series - see below for supported chips). Room is provided for a ZIF socket for the EPROM, if desired. For RAM, an AS6C1008 SRAM is used, providing 128K of addressable memory. The upper 64K is difficult to use (page size is the entire 64K Z80 address space), but is there for the adventurous coder; consider this 64K of RAM for most purposes.

## Paging
The ROM is enabled by default, appearing at the bottom of memory (the RAM filling the rest of the address space). A config register allows it to be disabled (paged out) and replaced with RAM - this is required by systems like CP/M. A second config register selects between lower and upper 64K RAM banks. These registers are presented as two I/O devices to the system: ROM paging at 0x38, and RAM selection at 0x30. Writing a **1** to 0x38 disables the ROM, and writing a **1** to 0x38 switches to the upper RAM bank. Both of these actions are indicated by LEDs.

The ports are chosen to have the same organization as the [SC114 Motherboard](https://smallcomputercentral.wordpress.com/sc114-documentation/), and the ROM control address is common to most Z80 retrocomputers (the official RC2014 RAM/ROM cards included). As such, this board is basically the SC114's memory subsystem, in card form. 

## Chip support
The board supports 27C64, 27C128, 27C256, and 27C512 EPROMs, as well as 28C64 and 28C256 EEPROMs. Other chips with similar pinouts will *probably* work, but are untested. 150ns parts (like most 28C256s) are running at the edge of their specification in a standard 7.3Mhz system, and may require lowering the CPU clock. The [27C256](https://www.mouser.com/ProductDetail/AT27C256R-70PU/), [27C512](https://www.mouser.com/ProductDetail/AT27C512R-70PU/), and [28C256](https://www.mouser.com/ProductDetail/AT28C256-15PU/) can be purchased new.

## Firmware
Most (if not all) [RC2014 ROM images](https://github.com/RC2014Z80/RC2014/tree/master/ROMs) can be used unmodified (selecting the right images for your serial board, of course). Stephen C Cousins' excellent [Small Computer Monitor](https://smallcomputercentral.wordpress.com/small-computer-monitor/) can be used as well - all of the R* configurations are supported. You will need an EPROM programmer (for example, a [TL866](https://www.ebay.com/sch/i.html?_nkw=tl866ii+plus)) to load the ROM images onto a chip.

## Jumper settings
Refer to the front and back of the board for detailed jumper setting instructions.

## Part selection
Bill Of Materials and part references are below. I recommend using gold-plated header for the bus connection - I use these ones from [Pololu](https://www.pololu.com/product/967) or [Sparkfun](https://www.sparkfun.com/products/553). A nice detail of these, is that they sit at the same height as double-row header in a backplane. The jumper headers can be snapped from regular (or double-row) breakaway header, for which eBay is substantially cheaper; the Mouser listings are provided for convenience.

The specified parts are just the ones I used, and can be substituted as needed - Mouser links provided for convenience and reference. A ZIF socket can be used for the EPROM - these are best [sourced from eBay](https://www.ebay.com/sch/i.html?_nkw=28+pin+zif+socket).

| Reference | Value | Qty | Mouser link |
| --------- | ----- | --- | ----------- |
| C1-C5 | 100nF ceramic | 5 | [KEMET C315C104M5U5TA](https://www.mouser.com/ProductDetail/C315C104M5U5TA7303) |
| D1, D2 | 3mm green LED | 2 | [Lite-On LTL-4231N](https://www.mouser.com/ProductDetail/LTL-4231N) |
| J1 | 1x40 right-angle header | 1 | [Wurth 61304011021](https://www.mouser.com/ProductDetail/61304011021) |
| JP1/2 | 2x3 header | 1 | [Amphenol 10129381-906002BLF](https://www.mouser.com/ProductDetail/10129381-906002BLF) |
| JP3/4/5 | 3x3 header | 1 | [Samtec TSW-103-07-L-T](https://www.mouser.com/ProductDetail/TSW-103-07-L-T) |
| JP6 | 2x2 header | 1 | [Amphenol 10129381-904002BLF](https://www.mouser.com/ProductDetail/10129381-904002BLF) |
| | jumpers | 7 | [Harwin M7583-46](https://www.mouser.com/ProductDetail/M7583-46)
| R1, R2 | 470Ω resistor | 2 | [Yageo CFR-25JT-52-470R](https://www.mouser.com/ProductDetail/CFR-25JT-52-470R) |
| R3, R4 | 10kΩ resistor | 2 | [Yageo CFR-25JT-52-10K](https://www.mouser.com/ProductDetail/CFR-25JT-52-10K) |
| U1 | EPROM | 1 | (see above for EPROM choices) |
| | socket | 1 | [Amphenol DILB28P-223TLF](https://www.mouser.com/ProductDetail/DILB28P-223TLF), or above ZIF |
| U2 | AS6C1008 SRAM | 1 | [Alliance AS6C1008-55PCN](https://www.mouser.com/ProductDetail/AS6C1008-55PCN) |
| | socket | 1 | [Amphenol DILB32P-223TLF](https://www.mouser.com/ProductDetail/DILB32P-223TLF) |
| U3 | 74HCT4075 | 1 | [TI CD74HCT4075E](https://www.mouser.com/ProductDetail/CD74HCT4075E) |
| U4 | 74HCT74 | 1 | [TI SN74HCT74N](https://www.mouser.com/ProductDetail/SN74HCT74N) |
| U5 | 74HCT138 | 1 | [TI SN74HCT138N](https://www.mouser.com/ProductDetail/SN74HCT138N) |