# Flash Your Badge

You have a BadgePirates badge in your hand. You want to:

- Update it to the latest firmware
- Switch it to a different firmware (e.g. ESP32Marauder, a different conference's build)
- Recover from a brick
- Hack on the source and load your own build

This page covers all four. The easy path is the browser flasher — most badges are USB-C, plug in, click flash, done. The recovery and dev-mode paths are below if the easy path fails.


## The easy way: web flasher (Chrome / Edge / Brave)

1. Plug your badge into your computer via USB-C.
2. Open **<https://firmware.badgepirates.com>** in a Chromium-based browser (Chrome, Edge, Brave). Web flashing requires the WebSerial API; Firefox and Safari don't support it.
3. Pick your badge from the list (BSidesKC 2026, CactusCon 14, etc.). Each has a manifest of the firmware variants we publish — production, debug, Marauder where available.
4. Click **Connect**. A serial port picker pops up; pick the one labeled with your badge's chip (usually shows up as a USB JTAG/serial device or `cp210x` / `ch340`).
5. Click **Install** and watch the bar. It takes 30–90 seconds depending on the firmware size.
6. When it finishes, the badge reboots into the new firmware.

If the badge doesn't show up in the picker:

- Try a **different USB-C cable**. Cheap charge-only cables don't carry data and are by far the most common cause of "the badge doesn't appear."
- Try a different USB port (some hubs cause issues; direct-to-laptop is most reliable).
- On Windows, you may need the **CP210x or CH340 driver** depending on the badge. Both are free downloads from Silicon Labs / WCH.
- On macOS, the device should show up automatically as `/dev/cu.usbserial-*` or `/dev/cu.usbmodem*`.


## When the easy way doesn't work: esptool

If the browser flasher can't talk to your badge — usually because the badge is in a wedged state — drop down to **esptool.py**, the official Espressif command-line flasher.

```bash
# install (one-time)
pip install esptool

# put the badge into download mode (most BP badges):
# 1. Hold the BOOT button
# 2. Press and release RESET
# 3. Release BOOT
# (Some badges auto-enter download mode when esptool talks to them. Try without the manual dance first.)

# erase + reflash from a downloaded .bin
esptool.py --chip esp32s3 --port /dev/ttyUSB0 --baud 460800 erase_flash
esptool.py --chip esp32s3 --port /dev/ttyUSB0 --baud 460800 write_flash 0x0 firmware.bin
```

You can grab the same `.bin` files the web flasher uses from `s3://badgepirates-firmware/` (URLs are in each badge's `manifest.json` — view-source the firmware page to see them, or check the [esp32-flasher repo](https://github.com/BadgePiratesLLC/esp32-flasher)).


## OTA: updating without a cable

The BSidesKC 2026 firmware (and any badge that ships with the OTA module enabled) supports over-the-air updates. From the badge:

1. Settings → WiFi → connect to a network
2. Settings → Updates → Check for Update
3. If a new version is available, the badge pulls it from S3 and reboots into the new firmware automatically.

OTA only updates *within the same firmware family* — it won't switch a CC14 badge to BSidesKC 2026 firmware, or to Marauder. For cross-firmware switches, use the web flasher.


## Dev mode: load your own code

The badges are stock ESP32-S3s. If you want to flash your own builds:

- **PlatformIO**: works out of the box. Use the appropriate `board = esp32-s3-devkitc-1` (or matching variant) and the pin map from [ESP32-S3 Platform Reference](../platform/esp32-s3.md).
- **ESP-IDF**: same — use `idf.py set-target esp32s3` and configure the pins.
- **Arduino IDE**: install the ESP32 board package (Espressif), pick "ESP32S3 Dev Module," set Flash Size to 16MB, USB Mode to Hardware CDC and JTAG (or USB-OTG depending on what your sketch uses).

The KiCad project files for each badge are public — see the [Catalog](../catalog/index.md) for links per badge.


## Recovering a brick

If your badge is stuck in a boot loop or won't enumerate:

1. Hold **BOOT** and tap **RESET** to force download mode.
2. From a terminal, run `esptool.py --chip esp32s3 --port <port> chip_id`. If esptool can talk to it, the badge isn't bricked — just confused. Reflash with the production firmware.
3. If esptool can't connect at all, the bootloader may be corrupted. Hold BOOT, plug in, release BOOT after 2 seconds — this enters the ROM bootloader, which always exists. Then reflash.
4. If the chip itself is fried (rare — usually requires reverse polarity or shorting power rails), the badge needs replacement. Open an issue on the relevant badge's repo or ping us in Discord.


## Need help?

[Join the Discord](https://discord.gg/BfsYbHY8m7) — `#firmware-help` is the right channel. Bring the badge name, your OS, and the exact error message you're seeing.
