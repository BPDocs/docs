# ESP32-S3 Platform Reference

A handful of BadgePirates badges share the same ESP32-S3 hardware platform — different firmware, same silicon. CactusCon 13, CactusCon 14, BSidesKC 2025 (Project Suplex), and BSidesKC 2026 are all built on it. This page is a one-stop reference for hacking on that platform: pin map, peripherals, dev environment, common gotchas.


## Core hardware

| Component | Detail |
|-----------|--------|
| MCU | Espressif ESP32-S3, dual-core 240 MHz, integrated WiFi + BLE 5.0 |
| Flash | 16 MB QIO |
| PSRAM | (varies per build — check the schematic for your specific badge) |
| USB | Native USB-C (CDC + JTAG, no separate USB-to-serial chip needed) |


## Pin map (BSidesKC 2026 reference)

The CC13 / CC14 / BSidesKC 2025 boards share the same pinout for the major peripherals; minor variants are noted in each badge's KiCad schematic.

| Peripheral | GPIO |
|------------|------|
| Display SPI MOSI | 11 |
| Display SPI SCLK | 12 |
| Display CS | 10 |
| Display DC | 5 |
| Display RST | 4 |
| Display Backlight | 6 |
| Touch I2C SDA | 8 |
| Touch I2C SCL | 9 |
| Touch RST | 3 |
| Touch INT | 7 |
| NeoPixel data | 18 |
| Encoder A / B | (per board — check schematic) |
| Buzzer | (per board — check schematic) |
| MAX17048 fuel gauge I2C | shared with touch (SDA 8 / SCL 9) |


## Peripherals

- **Display:** 320×240 SPI TFT, ILI9341 controller. Works with most ESP32 graphics libraries (LVGL, TFT_eSPI, esp_lcd).
- **Touch:** FT6336U capacitive touch over I2C. INT line goes low when a touch event is available.
- **NeoPixels:** 6× WS2812B chained off a single GPIO (default: 18). Use any standard NeoPixel library (FastLED, Adafruit_NeoPixel, ESP-IDF led_strip).
- **Buzzer:** simple piezo, drive with PWM.
- **Battery:** LiPo with MAX17048 fuel gauge over I2C. Provides accurate state-of-charge reading without the usual "voltage divided by 4.2" approximation.
- **SD Card:** microSD slot wired for SPI mode (some boards also expose SDIO).
- **USB-C:** native USB-OTG. Acts as both CDC serial (for logs/flashing) and HID/MSC for custom apps.


## Dev environment

### PlatformIO (recommended)

```ini
[env:bp-badge-esp32s3]
platform = espressif32
board = esp32-s3-devkitc-1
framework = arduino    ; or 'espidf' for native
monitor_speed = 115200
board_build.flash_mode = qio
board_build.flash_size = 16MB
board_build.partitions = default_16MB.csv
build_flags =
  -DARDUINO_USB_MODE=1
  -DARDUINO_USB_CDC_ON_BOOT=1
```

### ESP-IDF (native)

```bash
idf.py set-target esp32s3
idf.py menuconfig    # configure flash size, PSRAM, USB
idf.py build flash monitor
```

### Arduino IDE

1. Add the Espressif ESP32 board manager URL: `https://espressif.github.io/arduino-esp32/package_esp32_index.json`
2. Install "esp32" boards
3. Select **ESP32S3 Dev Module**
4. Settings: Flash Size **16MB (128Mb)**, USB Mode **Hardware CDC and JTAG**, USB CDC On Boot **Enabled**


## Common gotchas

- **USB Mode:** if you set USB Mode to "USB-OTG (TinyUSB)" without configuring TinyUSB descriptors, the badge won't enumerate at all. Stick with "Hardware CDC and JTAG" unless you know you need OTG.
- **PSRAM detection:** the ESP32-S3 has multiple PSRAM SKUs (octal vs quad). Auto-detect usually works; if your sketch crashes on `psramInit()`, manually configure for the chip variant in your schematic.
- **Boot loop with custom firmware:** ESP32-S3 has stricter brownout detection than the original ESP32. If your code does heavy work right after boot before the LiPo settles, you may hit a brownout reboot. Add a `delay(500)` after `setup()` or check battery voltage first.
- **NeoPixel timing on dual-core:** if you write to NeoPixels from one core while WiFi is busy on the other, you can get color glitches. Use the IDF `led_strip` driver (RMT-based, immune to this) or pin NeoPixel writes to core 1 with WiFi on core 0.


## Where the source lives

- **Hardware (KiCad files, gerbers, schematics):** see the [Catalog](../catalog/index.md) for the public hardware repo per badge. CactusCon 14 has the most up-to-date set: [CactusCon14](https://github.com/BadgePiratesLLC/CactusCon14).
- **Common library (KiCad symbols, footprints, BP logos):** [BadgePirates_Common_Library](https://github.com/BadgePiratesLLC/BadgePirates_Common_Library).
- **Firmware:** varies per badge. The BSidesKC 2026 firmware repo is private; the [Marauder port](https://github.com/BadgePiratesLLC/badgepirates-wifi-marauder) is public and a good starting point for understanding the hardware abstraction layer.


## Further reading

- [Flash Your Badge](../flash/index.md) — how to load firmware onto an assembled badge
- [Catalog](../catalog/index.md) — every BP badge with hardware + firmware repo links
- [BadgePirates Common Library README](https://github.com/BadgePiratesLLC/BadgePirates_Common_Library) — KiCad library setup and conventions
