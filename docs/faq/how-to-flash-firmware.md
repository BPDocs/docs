# How do I flash firmware to my badge?

If your badge is one of ours and uses an ESP32, ESP32-S2, or ESP32-S3, the easiest way to flash firmware is through our **web flasher** — no software install required.

## Web Flasher

1. Visit [firmware.badgepirates.com](https://firmware.badgepirates.com)
2. Plug your badge into your computer with a USB cable
3. Pick your badge from the dropdown
4. Click **Connect** and select your badge's serial port from the browser dialog
5. Click **Install** — the flasher will write the firmware over USB

The web flasher works in any Chromium-based browser (Chrome, Edge, Brave, Opera) thanks to the Web Serial API. **Firefox and Safari are not supported** — Web Serial isn't available there.

## What if my badge isn't in the dropdown?

The flasher only knows about badges we've explicitly added. If you have an older or one-off BadgePirates badge that isn't listed, hop on the [Discord](https://discord.gg/BfsYbHY8m7) and ask — we may have firmware archived somewhere, or someone in the community might.

## Reflashing at a conference

If you're at an event where we have a table, just **bring your badge** — we'll often reflash it on the spot, no charge. This is especially common when we ship updated firmware after a conference.

## Manual flashing (advanced)

If you'd rather flash from the command line or your own toolchain, the binaries are available in either:

- The badge's project repo on [our GitHub](https://github.com/BadgePiratesLLC), or
- Our public S3 bucket (`badgepirates-firmware.s3.amazonaws.com/<badge-key>/`)

You can use [esptool.py](https://github.com/espressif/esptool) to flash them yourself. Each manifest file lists the offsets and parts for that specific badge.

## Help! Something went wrong

The most common issues are:

| Problem | Likely fix |
|---|---|
| Browser can't see the badge | Check the USB cable — some are charge-only and have no data lines |
| "No serial ports available" | Try a different USB port; on macOS you may need to install drivers for the USB-to-serial chip |
| Firefox or Safari | Switch to a Chromium browser — Web Serial isn't supported elsewhere |
| Flash hangs at "Connecting..." | Hold the BOOT button on your badge while clicking Connect (forces bootloader mode) |

If you're still stuck, the [Discord](https://discord.gg/BfsYbHY8m7) is the fastest way to get help.
