# OnePlus Nord CE 3 (Ziti) — Flashing & Modding Guide

> ⚠️ **Disclaimer:** Unlocking the bootloader, flashing, and rooting will erase your data and can permanently damage (hard-brick) your device if done incorrectly. Proceed at your own risk. Always back up your data first.

## Table of Contents
1. [Device Specs](#device-specs)
2. [Required Tools & Drivers](#required-tools--drivers)
3. [Critical Warnings](#critical-warnings)
4. [Enable Developer Options](#enable-developer-options)
5. [Unlock / Lock Bootloader](#unlock--lock-bootloader)
6. [Downgrade OxygenOS](#downgrade-oxygenos)
7. [Rooting](#rooting)
8. [Extracting a ROM (Payload Dumper)](#extracting-a-rom-payload-dumper)
9. [Flashing a Custom ROM](#flashing-a-custom-rom)
10. [Reverting to Stock OOS](#reverting-to-stock-oos)
11. [Recovering from a Bad Relock](#recovering-from-a-bad-relock)
12. [Stock ROM Links](#stock-rom-links)
13. [Credits & Community Links](#credits--community-links)

---

## Device Specs

**OnePlus Nord CE 3 5G** — Code name: `Ziti` — Model: `CPH2569` (sold as Oppo K11 in China)
Launch date: 5 August 2023 · [Official specs](https://www.oneplus.in/nord-ce-3-5g/specs)

| Category | Details |
|---|---|
| Display | Fluid AMOLED, 1B colors, 120Hz, HDR10+, 6.7", 1080x2412, 394 ppi, 2160Hz PWM dimming |
| Weight | 184g |
| Chipset | Snapdragon 782G (6nm), family sm7325-af (Yupik/Lahaina) |
| CPU | Octa-core: 1x2.7GHz + 3x2.4GHz Cortex-A78, 4x1.8GHz Cortex-A55 |
| GPU | Adreno 642L |
| Rear Camera | 50MP (IMX890, OIS+EIS) + 8MP (IMX355) + 2MP |
| Front Camera | 16MP (IMX481) |
| Battery | 5,000mAh dual-cell (2x2,500mAh), 80W SUPERVOOC |
| OS (launch) | Android 13, OxygenOS 13.1 (2 major OS + 3 years security updates) |
| Storage | UFS 3.1, MicroSD supported |
| Connectivity | Bluetooth 5.2, Wi-Fi 6, NFC, IR Blaster |
| Audio | Dolby Atmos, Hi-Res (wired + wireless) |
| Other | X-Axis linear motor, in-display fingerprint |

---

## Required Tools & Drivers

- **Platform Tools (ADB/Fastboot):** always use the latest — [Download](https://developer.android.com/tools/releases/platform-tools)
- **Universal ADB Drivers:** https://adb.clockworkmod.com/
- **Google USB Drivers:** https://developer.android.com/studio/run/win-usb
- **Alt ADB/Fastboot installer:** https://github.com/fawazahmed0/Latest-adb-fastboot-installer-for-windows
- **GApps:** MindTheGapps A-14.0.0 or NikGapps

---

## Critical Warnings

- 🚫 **Never downgrade to OOS 13 with an unlocked bootloader.** OOS 13.1's bootloader is corrupted on Ziti, and there's no way to enter Bootloader/Fastboot mode from it.
- 🚫 **Never update OxygenOS while the bootloader is unlocked.**
- 🔒 **Before relocking, unroot first** (flash the *stock* boot.img, not the patched one).
- 🧬 If you're on **OOS 15.0.0.1301 or newer**:
  - Only flash custom ROMs built **without firmware** (builds after 26 Nov 2025).
  - Before flashing a custom ROM, flash your current stock version to the *other slot* first (see [Flashing on Another Slot](#flash-current-version-to-other-slot)).
  - If reverting back to stock, revert to the **same version** you were originally on — flashing an older firmware than what's on the other slot risks a **hard brick** recoverable only by a service center.
- If you've never updated to OOS 15.0.0.1301, **do not** update to it, and don't revert back to it from a custom ROM either.
- Read the [XDA warning on permanent bootloader locks for Oppo/OnePlus/Realme devices](https://xdaforums.com/t/final-warning-permanent-bootloader-lock-incoming-for-oppo-oneplus-realme-devices.4776062/) before touching firmware/slots.

---

## Enable Developer Options

`Settings > About Phone > Version` → tap the version number 7–8 times.

Then, in Developer Options, enable:
- **USB debugging**
- **Allow Bootloader Unlock**

---

## Unlock / Lock Bootloader

**Video tutorials:** [Unlock](#) · [Lock](#) *(see original notes for links)*

**Requirements:**
- A working PC/laptop with ADB & Fastboot drivers installed
- Device on OOS 14+ (bootloader option only available from OOS14 onward on Ziti)
- Full backup (unlocking/locking wipes internal storage)

**Steps:**
1. Enable USB debugging + Allow Bootloader Unlock (see above), connect device via USB.
2. Extract the latest Platform Tools, open a terminal in that folder (Shift + Right-click → *Open terminal here*).
3. Verify device connection: