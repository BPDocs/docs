## What's the Simplest Way to Add OTA Firmware Updates for Attendees?

At Badge Pirates, we make firmware updates simple for attendees by using **Wi-Fi OTA (Over-the-Air) updates built directly into the badge firmware**.

Here’s how it works:

1. **The badge connects to Wi-Fi**  
   When triggered (usually from a menu option or on boot), the badge automatically connects to a configured Wi-Fi network.

2. **It checks for the latest firmware version**  
   The badge downloads a small text file (called the **manifest**) from our server. This file contains the latest firmware version number.

3. **It compares the version**  
   If the server version is newer than what the badge is running, it begins the update process.  
   If the badge is already up-to-date, it shows a message and restarts.

4. **It securely downloads and installs the new firmware**  
   The badge downloads the latest `.bin` firmware file directly over Wi-Fi and flashes itself — no cables, no flashing tools needed.

5. **The badge restarts automatically**  
   Once updated, the badge reboots into the new firmware, ready to go.

---

**Why do we like this method?**  
- It's seamless for the attendee — just connect to Wi-Fi and click "Update."
- No need to install any flashing software.
- Updates can be pushed even after the event if new features or bug fixes are released.
- It's fast and reliable, tested directly on the hardware.

> **Pro Tip:** We recommend attendees stay plugged into a power source (or fully charged) before starting an update, just in case!

---

## How Does the Badge Pirates OTA Update System Work? (Developer Details)

Badge Pirates badges implement OTA updates using the **ESPhttpUpdate** library on the ESP32 platform.  
Here’s a deeper technical overview:

- **Manifest Check:**  
  The badge downloads a simple text file (e.g., `firmware.version`) from a predefined OTA server URL.  
  This manifest contains the latest firmware version number.

- **Version Comparison:**  
  The downloaded version is compared to the running firmware version embedded in the badge (`VERSION` macro).  
  If a newer version is available, the update process begins.

- **Firmware Download:**  
  The badge then downloads the corresponding `.bin` firmware file (e.g., `firmware.bin`) from the OTA server.

- **Flashing and Reboot:**  
  Using **ESPhttpUpdate**, the badge flashes the new firmware into memory over Wi-Fi and triggers a reboot.

- **Error Handling:**  
  Common OTA errors (Wi-Fi unavailable, download failure, already up-to-date) are visually indicated on the badge's display using the TFT.

---

**Hosting Requirements:**
- A server or hosting platform capable of serving static files (`.bin` and `.version` files).
- Accessible by the badge via HTTP.

**Example Folder Structure:**
https://your-server.com/ota/
  ├── firmware.version
  └── firmware.bin


**Libraries Used:**
- [ESPhttpUpdate](https://github.com/espressif/arduino-esp32/tree/master/libraries/HTTPUpdate)
- [TFT_eSPI](https://github.com/Bodmer/TFT_eSPI) (for display updates)

---

By using this Wi-Fi based OTA method, Badge Pirates can rapidly deploy firmware patches, new features, or post-event updates with minimal attendee involvement.

