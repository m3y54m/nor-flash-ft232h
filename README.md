# Read / Write NOR Flash Data Using FT232H

If you are trying to hack a hardware it is necessary to have a backup of flash memories on the hardware. I use a module based on FT232H for this purpuse.
FT232H (or FT2232H) can read and write NOR flash memories through SPI interface.

![image](https://github.com/m3y54m/nor-flash-ft232h/assets/1549028/4141005e-8237-452d-9b51-b7c07e2b40a7)

## Hardware Connection

The perfect way to avoid interference would be to simply desolder the Flash IC so it’s completely isolated from the rest of the circuit.

![image](https://github.com/m3y54m/nor-flash-ft232h/assets/1549028/67e66e1c-8931-4944-9528-ff1e8aa39075)

![image](https://github.com/m3y54m/nor-flash-ft232h/assets/1549028/9f221afd-f15d-4b2e-a1c3-2f859e720446)

| FT232H  |  NOR Flash  | Description                                            |
| ------- | ----------- | ------------------------------------------------------ |
| AD0     | CLK         | Clock - Idles low, levels are sampled on the rising edge |
| AD1     | MOSI (DI)   | Master Out Serial In - FT232H shifts data to the memory |
| AD2     | MISO (DO)   | Master In Serial Out - FT232H reads data from the memory |
| AD3     | CS          | Chip Select - Idles high, FT232H pulls low to initiate commands |
| +3.3V   | VCC         | 3.3V output of the regulator on FT232H module     |
| GND     | GND         | Common ground     |

## Requirements

```bash
sudo apt-get install flashrom
sudo apt-get install binwalk
```

## `flashrom`

flashrom is a utility for identifying, reading, writing, verifying and erasing flash chips. It is designed to flash BIOS/EFI/coreboot/firmware/optionROM images on mainboards, network/graphics/storage controller cards, and various other programmer devices.

### Read from NOR flash and dump to a file named `dump.bin`:

```bash
flashrom -p ft2232_spi:type=232H,port=A -r dump.bin
```

### Write to NOR flash from the file `dump.bin`:

```bash
flashrom -p ft2232_spi:type=232H,port=A -w dump.bin
```

## `binwalk`

You can analyze and interpret the contents of th dumped data using the `binwalk` tool.

```bash
binwalk dump.bin
```

![image](https://github.com/m3y54m/nor-flash-ft232h/assets/1549028/e873b3e6-7297-49e0-b549-c6c57d16818b)

## Resources

- [Practical Reverse Engineering Part 4 - Dumping the Flash](https://jcjc-dev.com/2016/06/08/reversing-huawei-4-dumping-flash/)
- [flashrom](https://flashrom.org)
- [FTDI 2232H Breakout For Hardware Hacking](https://hackaday.io/project/164346-andxor-dc27-badge/log/166065-ftdi-2232h-breakout-for-hardware-hacking)
- [Programming SPI flash with an FT232H breakout](https://learn.adafruit.com/programming-spi-flash-prom-with-an-ft232h-breakout)
- [A tool for reading and writing data in SPI flash memory chips using a FT232H (TOO SLOW!!!)](https://github.com/swharden/FTFlash)
- [Binwalk](https://www.kali.org/tools/binwalk/)
