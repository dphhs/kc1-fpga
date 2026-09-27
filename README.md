# kc1-fpga

KC1-FPGA is an FPGA development board that pairs a Lattice iCE40UP5K FPGA with an ESP32-S3-WROOM and various user I/O. The schematic is complete, and we are currently working on the layout. 

We wanted to build our own FPGA devboard after using them in second-year classes at UofT. This is our first take on one.

## MCU side (ESP32-S3)
 
The ESP32-S3-WROOM-1 (R8/R8V, octal PSRAM) handles networking, storage, audio, and most of the general I/O:
 
- W5500 Ethernet controller
- SD card slot
- Microphone over I2S
- 10 addressable LEDs
- Programmed over its native USB interface
## FPGA side (iCE40UP5K)
 
The iCE40 handles custom logic and has its own memory, I/O, and programming path:
 
- Extra PSRAM, connected directly to the FPGA over QSPI (separate from the ESP32's onboard PSRAM)
- 3 LEDs, 4 switches, and 4 push buttons
- Self-boots from a dedicated SPI flash in Master Config mode
- Some pins broken out to a PMOD connector and a header for expansion
## ESP32 ↔ FPGA link
 
The two chips connect over QSPI, using the ESP32's SPI2 peripheral which can be expanded to QSPI.
 
## FPGA programming
 
A dedicated FTDI chip handles getting a bitstream onto the FPGA, with two paths:
 
1. **Standalone boot:** USB programs the SPI flash, and the FPGA boots from it on its own.
2. **Direct config:** USB drives the FPGA directly, for faster iteration during development.
## Power
 
5V via USB-C, stepped down to 3.3V with a buck converter. The 3.3V rail powers the ESP32 and the iCE40's I/O voltage bank. A 3.3V to 1.2V LDO powers the iCE40 core.

## Next Steps

- [ ] PCB layout
- [ ] Fabrication and assembly
- [ ] Bring-up and testing



## Authors

[Matthew Kong](https://github.com/HynixCJR)
[Albert Huang](https://github.com/dphhs)
[Arnav Agarwal](https://github.com/arnyagrwl)