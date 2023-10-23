# Read / Write NOR Flash Data Using FT232H

## Requirements

```bash
sudo apt-get install flashrom
sudo apt-get install binwalk
```

## `flashrom`

Read from NOR flash and dump to `dump.bin`:

```bash
flashrom -p ft2232_spi:type=232H,port=A -r dump.bin
```

Write to NOR flash from `dump.bin`:

```bash
flashrom -p ft2232_spi:type=232H,port=A -w dump.bin
```

## `binwalk`

```bash
binwalk dump.bin
```

## Resources

- [Practical Reverse Engineering Part 4 - Dumping the Flash](https://jcjc-dev.com/2016/06/08/reversing-huawei-4-dumping-flash/)
- [FTDI 2232H Breakout For Hardware Hacking](https://hackaday.io/project/164346-andxor-dc27-badge/log/166065-ftdi-2232h-breakout-for-hardware-hacking)
- [Programming SPI flash with an FT232H breakout](https://learn.adafruit.com/programming-spi-flash-prom-with-an-ft232h-breakout)
- [A tool for reading and writing data in SPI flash memory chips using a FT232H (TOO SLOW!!!)](https://github.com/swharden/FTFlash)
