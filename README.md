# Board definition files

a new pre-defined board 'Ebaz4205' to select the processor type and some i/o desinitions. Copy into <base>/Xilinx/Vivado/2020.2/data/boards
[ebaz4205 board files](./ebaz4205)

## create project

![select board](./Screenshot from 2021-02-18 13-40-42.png)
![board selected](./Screenshot from 2021-02-18 11-31-01.png)

## configure ps7 

When a block design with the ps7 is created the system offers to 'run block automation'

![Designer Assistance](./DesignerAssistance.png)

An option is to 'Apply Board Preset', this is configured to set the neccessary values to make the memory and other devices work. The parameters are in the presets.xml found in the board files

![Block Automation](./BlockAutomation.png)


## show configuration

An overview of the applied settings is shown here:

![Block Design](./BlockDesign.png)

![show clocks](./Screenshot from 2021-02-18 13-38-26.png)

## configure ps7 - alternative method

Before the board preset was configured a .tcl script was used to perform a similar purpose

![select preset](./Screenshot from 2021-02-18 13-37-39.png)

A new board preset to automatically configure the i/o devices and memory parts. apply in ps7 block configuration screen.
[ebaz-4207-preset.tct](./ebaz4205-ps7-preset.tcl)


# pin definitions


A benefit of using a board definition file is the ease of use it allows when assigning pins to IP components. the sample board file here defines the pis for the board LEDs and fan connectors and an experimental input and output expansion card which has on it an SD card interface, a button, and a DIgilent style Pmod connector. The pin assignments are shown below.

|Ref |Name|Pin|Comment|
|----|----|---|-------|
|pl_sw_1bit_tri_i|Button|D19||
|pl_led_r_tri_o|Red LED|W14||
|pl_led_g_tri_o|Green LED|W13||
|JA1|Pmod 1|H16||
|JA2|Pmod 1|B19||
|JA3|Pmod 1|B20||
|JA4|Pmod 1|C20||
|JA5|Pmod 1|H17||
|JA6|Pmod 1|D20||
|JA7|Pmod 1|D18||
|JA8|Pmod 1|H18||
|GPIO_GROVE0_0|Fan 0 0|V15||
|GPIO_GROVE0_1|Fan 0 1|V12||
|GPIO_GROVE1_0|Fan 1 0|V13||
|GPIO_GROVE1 1|Fan 1 1|U12||

# Pmod interface


[pmod interface specification](https://reference.digilentinc.com/_media/reference/pmod/pmod-interface-specification-1_2_0.pdf)

The Digilent Pmod interface is used to connect low frequency, low I/O pin count peripheral modules to host
controller boards. There are six-pin and twelve-pin versions of the interface defined, encompassing SPI, I²C, UART,
I2S, H-bridge and GPIO protocols. The six-pin version provides four digital I/O signal pins, one power pin and one
ground pin. The twelve-pin version provides eight I/O signal pins, two power pins and two ground pins. The signals
of the twelve-pin version are arranged so that it provides two of the six-pin interfaces stacked.

## connector example

![pmod connector](./pmod-connector.png)


## Digilent pmod IP library

The Digilent pmod library for zynq contains lots of Ip and example code to demo the library in a very easy to use way. The library is here: https://github.com/Digilent/vivado-library A document describing how to use it with an easy to follow walk through is here: https://reference.digilentinc.com/reference/programmable-logic/guides/getting-started-with-pmod-ips.

## prototype hardware 

The example walk trrough uses the pmod-enc IP together with a Digilent rotary encode pmod, a similar board was prototyped to allow testing of the complete project. The prototype board has a simplified circuit, pull-up resistors were added afterwards (red sil network) when I realized that I didnt know how to add pull-ups to the pin definitions in the board definition file (todo, find out)

The Diigilent pmod encoder is described here: [pmod-enc](https://reference.digilentinc.com/reference/pmod/pmodenc/reference-manual)
The prototype board has all inputs switching to -ve, with 10k pull-up resitors to +ve. The series resistors are ommited - there are series resistors on the ebaz board inputs.

Pmod interface socket with pmod encoder board

![pmod enc proto](./pmod-enc-proto.png)

## demo application running

The board connected up and ready to go

![pmod inuse](./pmod-inuse.png)

Terminal output from demo application

![pmod enc term](./pmod-enc-term.png)

