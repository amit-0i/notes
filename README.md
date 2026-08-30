# OnePlus Nord CE3 5G (ziti) Documentation

Community-maintained documentation for the **OnePlus Nord CE 3 5G (CPH2569)**, internally known as **ziti**.

This documentation covers bootloader unlocking, ADB/Fastboot setup, stock ROM backups, rooting, custom ROM installation, reverting to OxygenOS, etc

> [!WARNING]
>
> Flashing firmware, unlocking the bootloader, rooting, modifying partitions, or relocking the bootloader can permanently damage or brick your device.
>
> You are responsible for anything you do to your device. This documentation is community-maintained and is provided without warranty.

---

## Important: Read This Before Flashing Anything

### OxygenOS 15.0.0.1301 and newer

**Treat OOS 15.0.0.1301+ devices differently from older firmware.**

For users on **OOS 15.0.0.1301 or newer**:

* Do **not** downgrade to an older firmware unless a current device-specific guide explicitly confirms it is safe.
* Do **not** flash custom ROM packages containing older firmware over your current firmware.
* Prefer custom ROM builds explicitly shipped **without firmware** when required by the ROM maintainer.
* Make sure both A/B slots contain the expected firmware before flashing.
* Do **not** perform an OxygenOS update with an unlocked bootloader unless a current ziti-specific guide explicitly says that the update is safe.
* When reverting to OxygenOS, use the same firmware version you were running before installing the custom ROM whenever the current guide requires it.

Multiple active ziti ROM projects continue to publish these warnings for OOS 15.0.0.1301+ users.

### OxygenOS 13.1 warning

The bootloader is broken on OxygenOS 13.1 which was later fixed by OnePlus with OxygenOS 14.

**Do not downgrade to OOS 13.1 while the bootloader is unlocked.**

Do not follow an old downgrade guide blindly. Verify the exact firmware/build and current recovery procedure before proceeding.

---

# Quick Start

New to modding your ziti?

Read the documentation in this order:

1. [Start Here](docs/00-start-here.md)
2. [Drivers and Tools](docs/01-drivers-and-tools.md)
3. [Bootloader Unlock / Lock](docs/02-bootloader.md)
4. [Back Up Stock Images](docs/03-backup-stock.md)
5. [Root Stock OxygenOS](docs/05-root-stock.md)
6. [Flash a Custom ROM](docs/07-custom-rom.md)
7. [Revert to Stock OxygenOS](docs/08-reverting-to-stock.md)

If something goes wrong, see [Unbrick](docs/09-unbrick.md) and [Troubleshooting](docs/11-troubleshooting.md).

---

# Guides

## Drivers and Tools

Required PC tools:

* Android SDK Platform-Tools
* USB drivers
* ADB
* Fastboot
* Payload Dumper Go
* Magisk when rooting

Use the **latest Android SDK Platform-Tools** from Google whenever possible. The official Android page currently lists Platform-Tools 37.0.1 and provides always-current downloads.

See:

**[Drivers and Tools →](docs/01-drivers-and-tools.md)**

---

## Bootloader Unlock / Lock

Unlocking the bootloader will erase the device.

Before unlocking:

* Back up internal storage.
* Enable Developer Options.
* Enable USB Debugging.
* Enable the OEM/bootloader unlocking option when available.
* Install ADB/Fastboot drivers.
* Verify ADB communication with the phone.

Basic commands:

```bash
adb devices
adb reboot bootloader
fastboot devices
fastboot flashing unlock
fastboot reboot
```

To lock:

```bash
adb reboot bootloader
fastboot flashing lock
```

**Do not relock a modified/rooted device.**

Before locking, restore the correct stock boot image and completely return the device to an appropriate stock state.

See:

**[Bootloader Unlock / Lock →](docs/02-bootloader.md)**

---

# Back Up Stock Firmware

Before experimenting with custom ROMs, maintain a backup of important stock partitions.

On a rooted stock system, the community backup procedure traditionally used:

```bash
adb shell
su
dd if=/dev/block/by-name/super of=/sdcard/super.img
dd if=/dev/block/by-name/persist of=/sdcard/persist.img
```

The resulting files are normally:

```text
super.img
persist.img
```

### Important

`persist.img` contains device-specific data.

Do **not** distribute your personal `persist.img`.

Keep your own backup somewhere safe.

It may contain device-specific calibration, fingerprint-related, sensor-related, or other unique data required by your particular handset.

See:

**[Back Up Stock Images →](docs/03-backup-stock.md)**

---

# Downgrading OxygenOS

Downgrading is **firmware-specific and build-specific**.

Older guides for Ziti used OxygenOS local installation packages. However, the downgrade rules changed significantly with later OxygenOS versions.

Do **not** treat an old downgrade package as universally safe.

### Older local-install method

When supported by the firmware:

1. Enable Developer Options.
2. Open:

```text
Settings
→ About Device
→ Version
```

3. Use the menu in the OxygenOS updater/local installation interface.
4. Select the correct rollback/downgrade package.
5. Start the installation.

A downgrade normally performs a factory reset.

**Back up everything first.**

### OOS 15.0.0.1301+

Do not use an old OOS downgrade guide on these builds without verifying that the procedure is currently supported.

Active Ziti community ROM documentation continues to warn users not to downgrade to older firmware from the 1301+ branch.

See:

**[Downgrade Guide →](docs/04-downgrade.md)**

---

# Rooting Stock OxygenOS

The basic Magisk workflow is:

1. Obtain the **exact stock `boot.img` matching your currently installed build**.
2. Install Magisk.
3. Patch the stock boot image with Magisk.
4. Copy the patched image back to the PC.
5. Reboot to bootloader.
6. Flash the patched boot image.
7. Reboot and verify root.

Typical commands:

```bash
adb reboot bootloader
fastboot flash boot magisk_patched.img
fastboot reboot
```

Example file naming:

```text
boot.img
magisk_patched.img
```

### Critical rule

Never assume that a boot image from another OxygenOS build is compatible with your current firmware.

Always match:

```text
Installed build
        ↓
Matching stock boot.img
        ↓
Magisk-patched boot.img
```

Current Magisk releases should be obtained from the official Magisk project rather than relying on an old version embedded in an old tutorial.

See:

**[Root Stock OxygenOS →](docs/05-root-stock.md)**

---

# Rooting Custom ROMs

There are two common approaches.

## Method A — Recovery / ADB Sideload

When supported by the ROM recovery:

```bash
adb reboot recovery
adb sideload Magisk.apk
```

The exact method depends on the recovery and Android version.

## Method B — Patch the ROM Boot Image

1. Extract the ROM payload.
2. Locate `boot.img`.
3. Copy it to the device.
4. Patch it using Magisk.
5. Copy the patched image to the PC.
6. Reboot to bootloader.
7. Flash the patched boot image.

Example:

```bash
adb reboot bootloader
fastboot flash boot magisk_los_patched.img
fastboot reboot
```

Always use the boot image belonging to the exact ROM build you are installing.

See:

**[Root Custom ROM →](docs/06-root-custom-rom.md)**

---

# Payload Dumper Go

Some ROM/OTA packages contain Android payload images inside a payload archive.

Payload Dumper Go can be used to extract them.

Example layout:

```text
payload-dumper/
├── payload-dumper-go
└── rom.zip
```

Run:

```bash
payload-dumper-go rom.zip
```

The extracted images can include files such as:

```text
boot.img
vendor_boot.img
dtbo.img
vbmeta.img
```

Always verify which images your ROM maintainer actually instructs you to flash.

Do not flash every extracted image simply because it exists.

See:

**[Drivers and Tools → Payload Dumper](docs/01-drivers-and-tools.md)**

---

# Flashing Custom ROMs

Custom ROM installation depends on the ROM.

A ROM may use:

* ADB sideload
* Fastboot
* FastbootD
* A ROM-specific recovery
* A combination of these

**Always follow the ROM maintainer's current flashing instructions first.**

## Typical ADB/Sideload workflow

### 1. Unlock the bootloader

See:

[Bootloader Unlock / Lock](docs/02-bootloader.md)

### 2. Reboot to bootloader

```bash
adb reboot bootloader
```

### 3. Flash the recovery supplied by the ROM maintainer

A typical recovery package may contain:

```text
boot.img
dtbo.img
vendor_boot.img
vbmeta.img
super_empty.img
flash.bat
flash.sh
```

Do not assume these files are interchangeable between ROMs.

### 4. Enter recovery

If required:

```bash
fastboot reboot recovery
```

### 5. Format data

For a clean installation:

```text
Factory Reset
→ Format Data / Factory Reset
```

Formatting data is commonly required when moving from OxygenOS to a custom ROM.

### 6. Sideload the ROM

In recovery:

```text
Apply Update
→ ADB Sideload
```

Then:

```bash
adb sideload rom.zip
```

### 7. Optional additional packages

Depending on the build:

* GMS build → usually do not flash another GApps package unless instructed.
* Vanilla build → flash a compatible GApps package if required.

Do not mix incompatible GApps packages or Android versions.

### 8. Reboot

```text
Reboot System
```

See:

**[Custom ROM Installation →](docs/07-custom-rom.md)**

---

# Firmware Rules for OOS 15.0.0.1301+

This section is intentionally prominent.

For users on **OOS 15.0.0.1301+**, current community ROM documentation advises maintaining the appropriate modern firmware and using ROM packages that do not replace it with an older firmware stack.

The important concepts are:

```text
ROM
Firmware
Slot A
Slot B
```

A/B devices can have different software states on their two slots.

Before flashing anything, determine:

```bash
fastboot getvar current-slot
```

The active slot is normally reported as either:

```text
a
```

or

```text
b
```

Changing slots should only be done when a device-specific procedure explicitly tells you to.

See:

**[Slots and Firmware →](docs/10-slots-and-firmware.md)**

---

# Reverting to Stock OxygenOS

Reverting from a custom ROM is not simply:

```text
flash OTA → reboot
```

On Ziti, the recovery and firmware state must be considered together.

Typical workflow:

1. Obtain the correct stock OTA package.
2. Obtain a compatible reverting/recovery package.
3. Reboot to bootloader.
4. Flash the required recovery.
5. Enter recovery.
6. Format data.
7. Sideload the stock OTA.
8. Reboot to bootloader.
9. Run the appropriate stock/reverting script.
10. Allow the script to finish.
11. Boot OxygenOS.

Example:

```bash
adb reboot bootloader
```

Then use the exact recovery and flashing script supplied for your target stock build.

### Match your firmware

For newer OOS 15 branches, current Ziti community documentation recommends reverting using the appropriate same-version/current firmware rather than arbitrarily choosing an older OxygenOS package.

See:

**[Reverting to Stock →](docs/08-reverting-to-stock.md)**

---

# Common Failure: "System Destroyed"

A common community-reported mistake is attempting to relock the bootloader after rooting/modifying the device without restoring the correct stock images.

Typical scenario:

```text
Rooted stock OOS
        ↓
Uninstall Magisk
        ↓
Attempt bootloader lock
        ↓
Boot failure / "System destroyed"
```

### General recovery concept

If the device can still enter Fastboot:

```bash
fastboot flashing unlock
```

Then flash the **matching stock boot image**:

```bash
fastboot flash boot boot.img
```

A data wipe may be required:

```bash
fastboot -w
```

Then:

```bash
fastboot reboot
```

Only attempt relocking after the device has successfully returned to a completely appropriate stock state.

Do not flash a Magisk-patched image when your goal is to restore a clean stock boot state.

See:

**[Unbrick →](docs/09-unbrick.md)**

---

# Fastboot Commands Reference

### Check connected device

```bash
fastboot devices
```

### Show current slot

```bash
fastboot getvar current-slot
```

### Reboot normally

```bash
fastboot reboot
```

### Reboot to recovery

```bash
fastboot reboot recovery
```

### Unlock bootloader

```bash
fastboot flashing unlock
```

### Lock bootloader

```bash
fastboot flashing lock
```

### Flash boot image

```bash
fastboot flash boot boot.img
```

### Erase user data

```bash
fastboot -w
```

> Never execute a destructive Fastboot command unless you understand exactly which partition/state it affects.

---

# ADB Commands Reference

### Verify ADB connection

```bash
adb devices
```

### Reboot normally

```bash
adb reboot
```

### Reboot to bootloader

```bash
adb reboot bootloader
```

### Reboot to recovery

```bash
adb reboot recovery
```

### Open shell

```bash
adb shell
```

### Copy file to phone

```bash
adb push file.img /sdcard/
```

### Copy file from phone

```bash
adb pull /sdcard/file.img
```

### Start sideload

```bash
adb sideload rom.zip
```

---

# Troubleshooting

## `adb devices` shows nothing

Check:

* USB cable
* USB port
* USB debugging
* Windows driver installation
* Authorization popup on the phone
* Device Manager
* ADB server

Try:

```bash
adb kill-server
adb start-server
adb devices
```

---

## `fastboot devices` shows nothing

Check that the phone is actually in Fastboot mode.

Try:

```bash
fastboot devices
```

If nothing appears, verify:

* USB cable
* Fastboot driver
* Windows Device Manager
* Platform-Tools version

Always prefer the latest Platform-Tools release from Google.

---

## ROM installation stops around 47%

Some Ziti recovery/ROM workflows report the installation reaching around 47% and appearing to pause while the recovery waits for another action.

Do not immediately assume the flash failed.

Read the recovery message carefully and follow the ROM maintainer's instructions regarding additional packages and rebooting recovery.

---

## `INSTALL DEVICE OPEN ERROR`

For some older Ziti sideload workflows, the community workaround was:

1. Format data.
2. Reboot recovery.
3. Attempt the ROM installation again.

This should not be treated as a universal solution for every ROM or recovery.

Always check the ROM-specific documentation first.

---

# Before You Start: Checklist

```text
[ ] Device is OnePlus Nord CE 3 5G / CPH2569 / ziti
[ ] Battery sufficiently charged
[ ] Important files backed up
[ ] Correct ROM downloaded
[ ] Correct recovery downloaded
[ ] Correct firmware verified
[ ] Latest Platform-Tools installed
[ ] ADB works
[ ] Fastboot works
[ ] Bootloader status confirmed
[ ] Correct slot/firmware state verified
[ ] Stock recovery/images backed up where appropriate
[ ] I have read the warnings
```

---

# Community Resources

### Telegram Support Group

https://t.me/OnePlusNordCE35G

### Telegram Update Channel

https://t.me/oneplusnordce3channel

### XDA

Use the relevant OnePlus Nord CE 3 / Oplus bootloader and firmware threads.

### SourceForge

Community ROM maintainers may publish Ziti builds, recoveries and reverting files through SourceForge.

---

# Credits

This documentation consolidates procedures and community knowledge contributed by Ziti users, maintainers and ROM developers.

Original material referenced in the source notes includes contributions attributed to:

* Anchal Singh / `@loid_ok`
* `@pjgowtham`
* `@venkat3620`
* Ziti ROM developers and testers
* OnePlus / OxygenOS community members
* Realme / OPlus community resources used for recovery/reverting procedures

Individual guides should retain their original credits when copied or adapted.

---

# Important Notice

This repository is a **community documentation project**, not an official OnePlus resource.

Information can become outdated as OxygenOS, firmware, recoveries and custom ROM installation methods change.

Before flashing:

**Check the ROM maintainer's current instructions.**

A guide that worked on an older OxygenOS build may be unsafe on a newer one.
