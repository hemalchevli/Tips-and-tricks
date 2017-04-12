Tips and Tricks
===============

This document contains information and tip and tricks about hardware design including schematic, placement, layout, documentation etc. These are the things I learned while doing learning how to work with high speed digital design. 

__This document is currently in a work in progress.__

I found these from various places on the interwebs, magazines and reference manuals, etc.

__Tip__: Always maintain projects on github/lab.

## Project Tree
 - Project_Name
   - CAD/
   - Hardware/
     - KiCad_Project_Folder/
        - 3D renders/
        - Footprints.pretty/
        - Gerbers/
        - KiCad_Project.sch
        - KiCad_Project.kicad_pcb
        - KiCad_Project.lib
        - BOM.xls
     - Datasheets/ (also contains app notes)
   - Software/
     - Firmware/
       - Tests/
       - Project firmware/
     - App/  (if any)

# Testing
 - Power the test board from lab power supply with current limiter, if any short is present, it will not let the magic smoke out.
 - If you assembly a prototype if it doesn't work, do not assembly more boards, find and fix the problem found in first board.

# Placement

 - Place all components on top side of the PCB. On complex designs place short height components go on bottom, never place tall components on the bottom side else it will increase the total height of the PCB.
 - Place power supply, components high current traces first.
 - Plan you layout first, then start placement.

# Components

 - Try using 1% resistors rather than 5%. Price is almost same. 1% Board will be more stable in high temp environment than using 5%.

# Schematics

 - Add cover page for schematic and add following to it.
   - Project name, date, and re/version number. All the names of schematics, notes legend, company information.
   - Schematic status with date (Draft, Preliminary, Checked, Released)

    	__Draft__: Blocks, just the structure of the schematic.

    	__Preliminary__: Connections done, Quiet close to final.

    	__Checked__: No mistakes in schematic.

    	__Released__: PCB sent for fab.

 - Add separate sheet for revision history.
 - Place analog circuit in a corner, so it will not interfere with high speed/current traces.
 - Name schematic names with clear and short name. (Avoid CPU1 CPU2, instead use CPU_HDMI CPU_LVDS etc.) On power supply schematic include the voltage levels

 - Include voltage value on all power net names. e.g. +3.3_V_REG, +1.2_VCC_DDR. __Never use "Vcc" as net name__

 - Add in design notes on the schematic.

 - If approval from client is needed for one or two extra part, just add it. It can be removed later.

# Layout
 - Plan your layout first.
 - Use slightly different foot prints for resistor and capacitor for same size e.g. 0805.
 - Create board variants of PCB design.
 - Use optional resistor to re-route signal to different interfaces or connectors
 - Have exactly same pins on symbols as on foot print part. Draw all pins even if a group of pins connects to same net.
 - __via aspect ratio__ find minimum drill size and via aspect ratio from fab size. E.g. 1:12 means 0.1mm holes max thickness of board (or max drill depth) 1.2mm. So 0.1 mm hole/via will not work for 1.6mm PCB. For micro via e.g. 1:1 means 0.1mm hole, max depth will be 0.1mm, find layer to layer distance from fab and draw appropriate uVia.

 - __Always ALWAYS think about return current for high speed signals__

 - For BGA, fan out all pins routes just outside the package and place all the vias before starting any routing the board.

 - __Never use auto router, not even for small section of pcb.__

 - __Never split ground planes__ (from mixed signals article issue June 2001 Printed Circuit design & circuits assembly design magazine), it will cause EMC problems by creating a dipole antenna. Do partition in layout, separate the analog and digital sections. Don't create voids in planes either, it creates an antenna.

 - Read PCB Design Guidelines For Reduced EMI - Texas Instruments (www.ti.com/lit/an/szza009/szza009.pdf)

 - Read 6 pillars of DfMA article in 03-16 issue of Printed Circuit design & circuits assembly design magazine's design practices section, all issue are free to download from magazine's website.

 - Use low ESR X7R 0604 caps

 - Check and double check rx tx pins connections between two components in schematics.

 -  For 4 to 6 PCB layers have 2 to 4 power planes.

 - Clearance: 6 mils
     - Trace width: 6 mils

 - Use PCB thickness: 1.6mm - 2mm(Less than this will cause heating issues leading to potential warpage.

 - Via hole 0.3

 - __Avoid Stubs__(stubs? http://www.polarinstruments.com/support/si/AP8166.html) to prevent signal reflections.

 - Isolate clock and HI-SPEED signal

 - Good article to avoid PCB defects (https://www.linkedin.com/pulse/how-avoid-embedded-pcb-design-defects-lisa-liu-jingwen)

 ### Layout Approach

 Route interfaces from high to low speeds, follow below order
 1. PCI Express
 2. USB 3.0
 3. SATA
 4. Ethernet
 5. HDMI
 6. LVDS
 7. USB 2.0
 8. SD/MMC/SDIO
 9. Parallel RGB LCD
 10. Parallel Camera
 11. Digital Audio
 12. VGA
 12. Analog audio, DC
 13. Low speed interfaces (I2C, UART, SPI, CAN, S/PDIF, and GPIO)


## Misc.

 - Place bypass caps as close to IC as possible, use combination of 10uF and 100nF, place smaller cap closer to IC.

 - Use stitching Caps when signals use power plane as reference for return path to gnd. __Very important__

 - Do not route high speed traces near the edge of the board and/or edge of reference plane.

 - Keep clocks and high current switching circuits like power supplies away from analog circuits. Also keep distance between traces if digital and analog are running in parallel, to avoid cross talk.

 - Use virtual split between analog and digital grounds, use mechanical layer to draw the split.

 - Use resistor of 22 ohm in series with clock line on MCU.

 - Keep gap between tracks as big as possible where space is available, especially keep more gaps on both sides on clock trace to avoid cross talk.

 - Keep reset signal from away from other signals. Use manufacture's app note to design reset circuit. If this part is not wired correctly, it can lead to unstable board.

 - Make sure enough space around mounting holes for screw heads to sit on and try placing big components around PCB.

 - Keep more space around headers pins/connectors. Lean from arduino's mistake on placing ISP of 168p too close to arduino headers. There is no space for screw head on mount hole near USB connector.

 - Always mark pin 1 of connectors on silk screen.

 - Route power track with min 0.4mm thickness.


## LAN interface

 - Use LAN port with integrated magnetics.
 - Shield LAN port with adequate GND plane.
 - Differential impedance: 100E
 - Common mode impedance: 50E
 - RX/TX mismatch: must be 0, max 1
 - For Gigabit max trace length: 3-5”
 - No traces under the connector.
 - Network jargon MII, SGMII, RGMII, PHY: http://stackoverflow.com/questions/15777399/clarification-on-ethernet-mii-sgmii-rgmii-and-phy#15777553
 - If phy is not on SoM, place phy at least 1” away from connector

## USB interface

 - Differential impedance: 80-100 ohms
 - CM impedance: 45
 - Continuous reference plane under diff pair

## SATA interface

 - Differential pair: 100
 - CM impedance: 60
 - Continuous reference plane under diff pair.
 - Minimum via use.
 - Strong matching not required but recommended

## PCI Express

 - Diff impedance: 100
 - CM impedance: 60
 - Intra pair matching is must, max difference 10mil
 - SD/MMC interface:

### PCB Stack up

#### Typical 4 layer stack up

| Layer        | Type               |
| ------------ | ------------------ |
| Top Layer    | High speed signals |
| Layer 2      | GND plane          |
| Layer 3      | Power plane        |
| Bottom Layer | High speed signals |

It’s recommended to route high speed signal on top rather than bottom, as the signals are directly referenced to ground plane. If high speed signals need to be on the bottom layer, swap power and gnd plane.

#### Typical 6 layer stack up
| Layer        | Type               |
| ------------ | ------------------ |
| Top Layer    | High speed signals |
| Layer 2      | Power plane        |
| Layer 3      | Low Speed plane    |
| Layer 4      | Low Speed plane    |
| Layer 5      | GND plane          |
| Bottom Layer | High speed signals |

Again route high speed signals with ground reference plane, in above case, it’s on bottom. Low speed signals do not need impedance matching.

#### Eight Layer Stack up

| Layer        | Type               |
| ------------ | ------------------ |
| Top layer    | High speed signals |
| Layer 2      | GND plane          |
| Layer 3      | High speed signals |
| Layer 4      | Power plane        |
| Layer 5      | Gnd plane          |
| Layer 6      | High speed signals |
| Layer 7      | Gnd plane          |
| Bottom       | High speed signals |

Layer 6 for high speed signals with most critical impedance control, next preference layer 1 and 8 for high speed routing.
If needed and if supported do polarity reversal and/or if needed and/or supported do lane reversal on PCIe
Keep all differential signals on the same layer, if layer switch is needed, switch both signals.


## 	Resources

Various Printed Circuit design & circuits assembly design magazine issues(http://pcdandf.com/pcdesign/)

Robert Feranec tips from YouTube and his courses.(http://www.fedevel.com/academy/)

Webinar and guides on toradex website(https://www.toradex.com/carrier-board-design)

Wiki on Daves SoM (http://wiki.dave.eu/index.php/Carrier_board_design_guidelines_(SOM))

Right the first time by Lee W. Ritchey