# OnePlus Nord CE 3 (Ziti) — Android Modding Notes

> Community-maintained notes for the **OnePlus Nord CE 3 (Ziti)**.
>
> **Device:** OnePlus Nord CE 3 5G  
> **Codename:** `ziti`  
> **Model:** `CPH2569`  
> **Region:** India-only variant in the source notes  
> **China counterpart:** OPPO K11

> [!CAUTION]
> Bootloader unlocking/locking, downgrading, rooting, flashing custom ROMs, and reverting to stock can erase data or brick the device.
> **You are responsible for what you do to your device. Back up important data before modifying anything.**
>
> The source notes specifically warn **not to downgrade to OxygenOS 13 with an unlocked bootloader**.

---

## Table of Contents

- [Device Information](#device-information)
- [Required Tools and Drivers](#required-tools-and-drivers)
- [Critical Warnings](#critical-warnings)
- [Bootloader Unlock / Lock](#bootloader-unlock--lock)
- [Downgrade OxygenOS](#downgrade-oxygenos)
- [Payload Dumper Go](#payload-dumper-go)
- [Root on Stock OxygenOS](#root-on-stock-oxygenos)
- [Root on Custom ROMs](#root-on-custom-roms)
- [Before Installing a Custom ROM](#before-installing-a-custom-rom)
- [Flashing Custom ROMs via ADB Sideload](#flashing-custom-roms-via-adb-sideload)
- [Flashing Fastboot ROMs](#flashing-fastboot-roms)
- [Flashing Custom ROMs on OOS 15.0.0.1301+](#flashing-custom-roms-on-oos-15001301)
- [Flashing the Same Firmware to the Other Slot](#flashing-the-same-firmware-to-the-other-slot)
- [Reverting to Stock OxygenOS](#reverting-to-stock-oxygenos)
- [Stock Firmware List](#stock-firmware-list)
- [Emergency Recovery: "System Destroyed"](#emergency-recovery-system-destroyed)
- [Reference Links](#reference-links)

---

## Device Information

# OnePlus Nord CE 3 — Specifications

## Network

| Category | Specifications |
|---|---|
| 2G bands | GSM 850 / 900 / 1800 / 1900 |
| 3G bands | HSDPA 850 / 900 / 1700(AWS) / 1900 / 2100 |
| 4G bands | 1, 2, 3, 4, 5, 7, 8, 28, 34, 38, 39, 40, 41 |
| 5G bands | 1, 3, 5, 8, 28, 40, 41, 78 (SA/NSA) |
| Speed | HSPA / LTE / 5G |

## Launch

| Item | Details |
|---|---|
| Announced | July 5, 2023 |
| Released | August 5, 2023 |
| Status | Available |

## Body

| Item | Details |
|---|---|
| Dimensions | 162.7 × 75.5 × 8.2 mm |
| Weight | 184 g |
| Build | Glass front, plastic frame, plastic back |
| SIM | Nano-SIM + Nano-SIM |

## Display

| Item | Details |
|---|---|
| Type | Fluid AMOLED, 1B colors, 120 Hz, HDR10+ |
| Size | 6.7 inches (108.0 cm²) |
| Screen-to-body ratio | ~87.9% |
| Resolution | 1080 × 2412 pixels |
| Aspect ratio | 20:9 |
| Pixel density | ~394 ppi |

## Platform

| Item | Details |
|---|---|
| OS | Android 13 / OxygenOS 13.1 |
| Chipset | Qualcomm Snapdragon 782G (6 nm) |
| CPU | 1×2.7 GHz Cortex-A78 + 3×2.4 GHz Cortex-A78 + 4×1.8 GHz Cortex-A55 |
| GPU | Adreno 642L |

## Memory & Storage

| Item | Details |
|---|---|
| Card slot | microSDXC (shared SIM slot) |
| Internal storage | 128 GB + 8 GB RAM; 256 GB + 12 GB RAM |
| Storage type | UFS 3.1 |

## Cameras

### Main Camera

| Item | Details |
|---|---|
| Setup | Triple camera |
| Main | 50 MP, f/1.8, 24 mm wide, 1/1.56\", 1.0 µm, multi-directional PDAF, OIS |
| Ultrawide | 8 MP, f/2.2, 112°, 1/4.0\", 1.12 µm |
| Macro | 2 MP |
| Features | LED flash, HDR, panorama |
| Video | 4K@30fps; 1080p@30/60/120fps; gyro-EIS |

### Selfie Camera

| Item | Details |
|---|---|
| Setup | Single camera |
| Camera | 16 MP, f/2.4, 24 mm wide, 1.0 µm |
| Features | HDR |
| Video | 1080p@30fps, gyro-EIS |

## Sound

| Item | Details |
|---|---|
| Loudspeaker | Stereo speakers |
| 3.5 mm headphone jack | No |
| Hi-Res audio | 24-bit / 192 kHz |

## Connectivity

| Item | Details |
|---|---|
| WLAN | Wi-Fi 802.11 a/b/g/n/ac/6, dual-band, Wi-Fi Direct |
| Bluetooth | 5.2, A2DP, LE, aptX HD, aptX Adaptive |
| Positioning | GPS, GLONASS, GALILEO, BDS, QZSS |
| NFC | Yes |
| Infrared port | Yes |
| FM radio | No |
| USB | USB Type-C 2.0 |

## Sensors

- Fingerprint sensor (under-display, optical)
- Accelerometer
- Gyroscope
- Proximity sensor
- Compass
- Temperature sensor

## Battery

| Item | Details |
|---|---|
| Type | Li-Po |
| Capacity | 5000 mAh |
| Charging | 80 W wired |
| Charging claim | 61% in 15 minutes |

## Miscellaneous

| Item | Details |
|---|---|
| Colors | Aqua Surge, Gray Shimmer |
| Model | CPH2569 |
| SAR | 1.17 W/kg (head), 0.91 W/kg (body) |


Official device specs:  
https://www.oneplus.in/nord-ce-3-5g/specs

---

## Required Tools and Drivers

### ADB / Fastboot drivers

- Universal ADB Drivers: https://adb.clockworkmod.com/
- Google USB Drivers: https://developer.android.com/studio/run/win-usb
- Latest ADB/Fastboot installer (GitHub): https://github.com/fawazahmed0/Latest-adb-fastboot-installer-for-windows
- Android SDK Platform-Tools: https://developer.android.com/tools/releases/platform-tools

> [!IMPORTANT]
> The source notes repeatedly recommend using the **latest Platform-Tools** and current GApps when flashing.

---

## Critical Warnings

### Downgrading

- **Do not downgrade to OxygenOS 13 with an unlocked bootloader.**
- Downgrading can erase internal storage.
- The source notes state that OxygenOS 13.1 on this device has bootloader-related problems and later notes say downgrading is effectively unavailable for OOS 15.0.0.1301+ users.

### Bootloader locking

- **Unroot before relocking.**
- Do not relock while a patched/rooted boot image is active.
- The recovery procedure in these notes assumes you restore the correct stock boot image first.

### OOS 15.0.0.1301+ / newer firmware

For devices on `CPH2569_15.0.0.1301` or newer:

1. Use custom ROMs **without bundled firmware** for builds after 26 November 2025.
2. Before flashing a custom ROM, put the **same currently installed firmware** on the other slot.
3. If returning to OxygenOS, return to the same firmware version to avoid issues with later OnePlus updates.

The source warns that missing these precautions can cause a **hard brick**, potentially requiring service-center recovery.

---

## Bootloader Unlock / Lock

### Prerequisites

- Back up everything. Unlocking or locking erases internal storage.
- Install current ADB/Fastboot drivers.
- Use a compatible OOS version where bootloader unlocking is available.
- Enable Developer Options:
  - Settings → About phone → Version
  - Tap the version number 7–8 times.
- In Developer Options, enable:
  - **USB debugging**
  - **Allow bootloader unlock**

### Verify ADB connection

```bash
adb devices
```

Accept the authorization prompt on the phone, then run:

```bash
adb devices
```

A serial number indicates that the device is connected to ADB.

### Enter Fastboot / Bootloader

```bash
adb reboot bootloader
```

Or use the hardware keys:

```text
Volume Up + Volume Down + Power
```

Verify Fastboot:

```bash
fastboot devices
```

### Useful slot commands

Check active slot:

```bash
fastboot getvar current-slot
```

Switch active slot:

```bash
fastboot --set-active=a
```

Replace `a` with `b` to select slot B.

### Unlock

```bash
fastboot flashing unlock
```

Confirm **Unlock** on the phone using the volume and power buttons.

### Lock

Only after restoring the correct stock state and removing root:

```bash
fastboot flashing lock
```

Confirm **Lock** on the phone.

### Reboot

```bash
fastboot reboot
```

---

## Downgrade OxygenOS

> [!CAUTION]
> **Do not perform this with an unlocked bootloader.**
>
> The process wipes user data. Make a complete backup first.

1. Enable Developer Options.
2. Open:
   - Settings → About phone → OxygenOS
3. Open the three-dot menu.
4. Select **Local install**.
5. Select the downgrade package.
6. Tap **Install**.
7. The phone reboots and the source notes state that all internal data will be erased.

---

## Payload Dumper Go

Use this to extract partition images from a payload/ROM package.

### Procedure

1. Download the stock or custom ROM ZIP.
2. Download Payload Dumper Go.
3. Put the ROM ZIP and Payload Dumper Go in the same folder.
4. Open a terminal in that folder.
5. Run:

```bash
payload-dumper-go romname.zip
```

You can also drag the ZIP into the terminal.

The extracted images will appear in a separate output folder.

---

## Root on Stock OxygenOS

### Requirements

- Stock `boot.img` matching the **exact build currently installed**.
- Magisk app.
- ADB / Platform-Tools.
- Unlocked bootloader.

### Patch the boot image

1. Extract the matching stock ROM.
2. Obtain its `boot.img`.
3. Copy `boot.img` to the phone.
4. Keep another copy in the Platform-Tools folder for recovery/unrooting.
5. Open Magisk.
6. Select:
   - Install → Select and Patch a File
7. Choose the copied `boot.img`.
8. Magisk places the patched image in the Download directory.
9. Rename it to:

```text
magisk_patched.img
```

### Flash the patched image

Copy the patched image to the Platform-Tools directory, then:

```bash
adb reboot bootloader
fastboot flash boot magisk_patched.img
fastboot reboot
```

After reboot, open Magisk and verify root.

---

## Root on Custom ROMs

The source notes give two methods.

### Method A — Magisk via recovery sideload

1. Connect to the PC and verify ADB:

```bash
adb devices
```

2. Reboot to recovery:

```bash
adb reboot recovery
```

3. In recovery:
   - Apply Update
   - ADB Sideload
4. On the PC:

```bash
adb sideload magisk.apk
```

5. Reboot to system and open Magisk.

### Method B — Patch the custom ROM boot image

1. Extract the ROM with Payload Dumper.
2. Copy the ROM's `boot.img` to the phone.
3. In Magisk:
   - Install → Select and Patch a File
4. Patch `boot.img`.
5. Rename the resulting file to:

```text
magisk_los_patched.img
```

6. Copy it to Platform-Tools.
7. Flash:

```bash
adb reboot bootloader
fastboot flash boot magisk_los_patched.img
fastboot reboot
```

8. Open Magisk after reboot to verify root.

---

## Before Installing a Custom ROM

> [!IMPORTANT]
> The source strongly recommends backing up stock partition images before modifying the device.

### Back up `super.img` and `persist.img`

With root access:

```bash
adb shell
su
dd if=/dev/block/by-name/super of=/sdcard/super.img
dd if=/dev/block/by-name/persist of=/sdcard/persist.img
```

The source notes:

- `super.img` may be around 14–15 GB.
- `persist.img` may be around 30–40 MB.
- `persist.img` contains device-specific data such as fingerprint-related data.
- Keep `persist.img` safe; losing it may result in fingerprint or VoLTE problems.
- Keep backups of newer `super.img` files after major stock updates.

---

## Flashing Custom ROMs via ADB Sideload

Use this flow for ROMs that are distributed as recovery/ADB-sideload packages.

### Files required

- Custom ROM ZIP
- Latest ADB / Platform-Tools
- ADB/Fastboot drivers
- Unlocked bootloader
- Recovery ZIP containing:

```text
boot.img
dtbo.img
vendor_boot.img
vbmeta.img
super_empty.img
```

The source recovery package uses commands equivalent to:

```bash
fastboot wipe-super super_empty.img
fastboot flash boot boot.img
fastboot flash vendor_boot vendor_boot.img
fastboot flash dtbo dtbo.img
fastboot flash vbmeta vbmeta.img
fastboot reboot recovery
```

### Flashing procedure

1. Extract the recovery ZIP into the Platform-Tools directory.
2. Reboot to bootloader:

```bash
adb reboot bootloader
```

3. Run the supplied `flash.bat` / `flash.sh`.
4. Boot into recovery.
5. **Format / Reset Data**. The source marks this as mandatory for the initial flash.
6. Go to:
   - Apply Updates → ADB Sideload
7. Sideload the ROM:

```bash
adb sideload rom.zip
```

8. When prompted about additional packages:
   - Select **Yes** when you need an additional package such as GApps.
   - Select **No** for builds that already include GMS/GApps.
9. Reboot to system.

### `kinstalldeviceopenerror`

If Lineage recovery reports:

```text
kinstalldeviceopenerror
```

The source recommends:

1. Format Data in recovery.
2. Reboot to recovery again.
3. Retry the ROM sideload.

> [!NOTE]
> Format Data is also noted as necessary when doing the first ROM flash, switching between ROMs, or when the ROM maintainer explicitly requires it.

---

## Flashing Fastboot ROMs

Use this method only when the ROM maintainer specifically says the ROM is intended for Fastboot flashing.

### Procedure

1. Download the ROM ZIP.
2. Put the device in bootloader mode:

```bash
adb reboot bootloader
```

Or use:

```text
Power + Volume Up + Volume Down
```

3. Place the ROM ZIP in the Platform-Tools folder.
4. Run:

```bash
fastboot update romname.zip
```

5. Format data on first boot, if required:

```bash
fastboot -w
```

The source notes say the ADB method should be preferred for LineageOS and similar ROMs unless the ROM post explicitly calls for Fastboot flashing.

---

## Flashing Custom ROMs on OOS 15.0.0.1301+

This section consolidates the newer firmware-specific instructions from the source.

> [!CAUTION]
> For `CPH2569_15.0.0.1301` and newer:
>
> - Flash only custom ROMs **without firmware** for builds after 26 November 2025.
> - Put the currently installed firmware on the other slot before flashing the ROM.
> - Do not update OxygenOS while the bootloader is unlocked.
> - Do not downgrade to older firmware.

### Flash flow

1. Confirm the bootloader is unlocked.
2. Reboot to bootloader:

```bash
adb reboot bootloader
```

3. Flash the recovery supplied by the ROM maintainer.
4. Run its `flash.bat` / equivalent script.
5. In recovery:
   - Factory reset
   - Format Data
6. Sideload the ROM:

```bash
adb sideload rom.zip
```

7. During the sideload:
   - The progress may stop around **47%** temporarily.
   - Choose **Yes** for additional packages when needed.
   - Choose **No** for builds that already contain the necessary Google components.
8. Reboot.

---

## Flashing the Same Firmware to the Other Slot

This is required by the newer OOS 15 instructions before flashing certain custom ROMs.

### Procedure

1. Check your current OxygenOS version:
   - Settings → About phone → Version
2. Download the **same** version OTA.
3. Enable Developer Options.
4. Install the OTA using Local Install:
   - Settings → About phone → Update
   - Three-dot menu → Local install
5. Select the downloaded OTA.
6. Reboot after installation.

### Alternative recovery-based method

The source also describes:

1. Flash compatible recovery from bootloader.
2. Format Data in recovery.
3. Sideload the same firmware OTA:

```bash
adb sideload 1601.zip
```

4. If verification fails, choose **Yes** to install anyway.
5. When the package reaches about 47% and asks to reboot recovery for additional files, choose **No**.
6. Reboot to bootloader from recovery.
7. Run the stock/reversion script.
8. The other slot should contain the same OOS build.

After that, proceed with the custom ROM flash.

---

## Reverting to Stock OxygenOS

There are several versions of the source procedure. The common flow is:

### Files required

- A recovery that supports reverting to stock.
- Matching stock OTA ZIP.
- Stock/reversion script package (called `my_shit.zip` in the source notes).
- Latest Platform-Tools.

The source notes state that **not all recoveries support reverting**.

### Step 1 — Enter bootloader

```bash
adb reboot bootloader
fastboot devices
```

### Step 2 — Flash the compatible recovery

Extract the recovery ZIP into Platform-Tools and run its supplied script:

```text
flash.bat
```

or the corresponding Linux/macOS script.

The device should boot into recovery.

### Step 3 — Format Data

In recovery:

```text
Factory reset → Format Data
```

### Step 4 — Sideload stock OTA

Go to:

```text
Apply Update → ADB Sideload
```

Then:

```bash
adb sideload stock_rom.zip
```

The source notes say to choose **Yes** for prompts such as:

- Signature verification failed
- This is a downgrade package
- This will downgrade your system

For the additional-package/reboot-recovery prompt, choose **No** according to the source procedure.

### Step 5 — Return to bootloader

From recovery:

```text
Advanced → Reboot to Bootloader
```

### Step 6 — Run the stock/reversion script

Extract the supplied stock script package into Platform-Tools and run its script.

The source describes the process as automating commands such as:

```bash
fastboot reboot fastboot
sleep 5
fastboot create-logical-partition my_company_a 0
fastboot create-logical-partition my_company_b 0
fastboot create-logical-partition my_preload_a 0
fastboot create-logical-partition my_preload_b 0
fastboot flash my_company --slot=all my_company.img
fastboot flash my_preload --slot=all my_preload.img
sleep 5
fastboot reboot bootloader
fastboot -w
fastboot reboot
```

The expected result is a boot into stock OxygenOS.

---

## Emergency Recovery: "System Destroyed"

The source describes this scenario as commonly occurring when relocking after removing Magisk without first restoring the stock boot image.

### Recovery procedure

If the device is locked, unlock it again:

```bash
fastboot flashing unlock
```

If it is boot-looping but not entering Fastboot automatically:

1. Unplug it from the PC.
2. Force Fastboot using:

```text
Volume Up + Volume Down + Power
```

3. Connect it to the PC after Fastboot appears.

Then flash the **matching stock boot image**:

```bash
fastboot flashing unlock
fastboot flash boot boot.img
fastboot reboot
```

The source notes that:

- The `boot.img` must match the OxygenOS version installed on the device.
- To unroot, use the **stock** boot image, not a patched Magisk image.
- `fastboot -w` can format the device if necessary, but the notes say it is not always required.

After the device successfully boots into the system, you may attempt to relock:

```bash
adb reboot bootloader
fastboot flashing lock
```

---

## Stock Firmware List

The source groups the following builds as follows.

### Non-ARB

```text
CPH2569_14.0.0.1101(EX01)
CPH2569_14.0.0.1401(EX01)
CPH2569_14.0.0.1402(EX01)
CPH2569_15.0.0.402(EX01)
CPH2569_15.0.0.700(EX01)
CPH2569_15.0.0.901(EX01)
```

### Questionable update

```text
CPH2569_15.0.0.1201(EX01)
```

### ARB

```text
CPH2569_15.0.0.1301(EX01)
CPH2569_15.0.0.1601(EX01)
CPH2569_15.0.0.1602(EX01)
CPH2569_15.0.0.1604(EX01)
CPH2569_15.0.0.1800(EX01)
CPH2569_15.0.0.1901(EX01)
CPH2569_15.0.0.1902(EX01)
```

> [!WARNING]
> The source notes specifically advise OOS 15.0.0.1301 users to avoid older firmware when flashing or reverting. Treat firmware/slot state as a first-class prerequisite, not an afterthought.

---

## OOS 15.0.0.1301 — Special Warning Summary

For users already on `CPH2569_15.0.0.1301`:

1. Update `1301` with a future OTA while the bootloader is locked, **or** put `1301` on the other slot as described earlier.
2. Use custom ROMs shipped **without firmware** where required.
3. Do not flash custom ROMs or downgrades containing older firmware.
4. Do not update OxygenOS with the bootloader unlocked.
5. The source warns that ignoring these steps can hard-brick the device.

For users who **never updated to OOS 15.0.0.1301**, the source says **not to update to 1301 solely for modding purposes** and not to revert to it from a custom ROM.

---

## Reverting Files / Packages

The source references the following recovery/script packages:

```text
lineage recovery
myshit_zip
evox recovery + myshit_zip with platform tools
```

The original notes indicate that download links are maintained in their Telegram/XDA/community posts rather than embedded consistently in the notes.

---

## Reference Links

### Drivers / Platform Tools

- Universal ADB Drivers: https://adb.clockworkmod.com/
- Google USB Drivers: https://developer.android.com/studio/run/win-usb
- Platform-Tools: https://developer.android.com/tools/releases/platform-tools
- ADB/Fastboot installer: https://github.com/fawazahmed0/Latest-adb-fastboot-installer-for-windows

### Device

- OnePlus Nord CE 3 official specs:  
  https://www.oneplus.in/nord-ce-3-5g/specs

### Community resources

- Telegram Support Group:  
  https://t.me/OnePlusNordCE35G
- Telegram Update Channel:  
  https://t.me/oneplusnordce3channel
- Flashing steps for 1301/1601/1602+:  
  https://t.me/OnePlusNordCE35G/76698
- Reverting to OOS files:  
  https://sourceforge.net/projects/evox-unofficial-ziti/files/Reverting%20to%20OOS/
- XDA warning thread referenced by the source:  
  https://xdaforums.com/t/final-warning-permanent-bootloader-lock-incoming-for-oppo-oneplus-realme-devices.4776062/

### GApps

The source references:

- MindTheGapps A-14.0.0
- NikGapps

Use a package appropriate for the Android version and ROM build being flashed.

---

## Practical Flashing Checklist

Before touching partitions:

- [ ] Back up personal data.
- [ ] Back up `persist.img` and `super.img` where possible.
- [ ] Confirm exact model: `CPH2569`.
- [ ] Record current OxygenOS version.
- [ ] Record active slot:

```bash
fastboot getvar current-slot
```

- [ ] Install current Platform-Tools.
- [ ] Install working USB/ADB/Fastboot drivers.
- [ ] Confirm `adb devices`.
- [ ] Confirm `fastboot devices`.
- [ ] Confirm the ROM's required firmware state.
- [ ] Confirm whether the ROM is an ADB-sideload build or Fastboot build.
- [ ] Confirm whether recovery supports reverting to stock.
- [ ] Keep the correct stock `boot.img`.
- [ ] Do not downgrade with an unlocked bootloader.
- [ ] Do not relock while rooted or while using a patched boot image.
- [ ] For OOS 15.0.0.1301+ workflows, verify both slots use the intended firmware before proceeding.

---

## Source Notes

This README is a **curated reorganization of the supplied notes dump**. The original material contains tutorials, warnings, community references, and shorthand such as `my_shit.zip` / `myshit_zip`; these names have been retained where they are part of the documented procedure.

Source notes include contributions credited to Anchal Singh / `@loid_ok`, `@pjgowtham`, `@venkat3620`, `@vekye`, `@MrSnklp`, `@r0ckstar126`, and others.

> [!NOTE]
> Community instructions can become outdated as firmware changes. Before flashing, check the current ROM maintainer post and the current firmware requirements for your exact build.
