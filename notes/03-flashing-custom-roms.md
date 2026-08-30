# Flashing Custom ROMs guide for OnePlus Nord CE3 5G (ziti)

>[!WARNING]
> Flashing firmware, unlocking the bootloader, rooting, modifying partitions, or relocking the bootloader can permanently damage or brick your device.
>
> You are responsible for anything you do to your device. This documentation is community-maintained and is provided without warranty.

>[!CAUTION]
> Your data will be lost during the process, please backup your data.

## Prerequisites
- Make sure you have read the warning: [here](./00-warning.md)
- Install the required adb and fastboot drivers: [guide](./01-resources.md#latest-adbfastboot-installer-github--httpsgithubcomfawazahmed0latest-adb-fastboot-installer-for-windows)
- Download the required files:- [platform tools](./01-resources.md#platform-tools--httpsdeveloperandroidcomtoolsreleasesplatform-tools), recovery which the ROM maintainer recommends, ROM zip

>[!TIP]
> Before installing custom ROM, backup your super.img and persist.img. More on that [here](./02-backup-super-persist.md)

## Steps
### 1. Unlock bootloader
>[!CAUTION]
> - Unlocking bootloader is only possible on **OxygenOS 14** or above
> - DO NOT try to downgrade to **OxygenOS 13** with an unlocked bootloader
> - This process will erase your data, backup before proceeding
#### 1. Turn on Developer option

Go to Settings > About phone > Version > Tap version 7-8 times

#### 2. Turn on USB debugging

Go to Settings > Addition settings > Developer option > Enable usb debugging

#### 3. Authentication ADB

Connect your phone to your pc then type
```shell
adb devices
```
a pop-up will appear on the phone, click allow

again type the above command and this type a serial device number will appear, this means the device is connected to the ADB interface successfully.

#### 4. Reboot to Bootloader
```shell
adb reboot bootloader
```
You can also enter Bootloader/Fastboot Mode by pressing and holding `volume -` & `power button` while restarting the device.

#### 5. Unlock / Lock bootloader
to check if you have proper connection between your phone and pc/laptop run:
```shell
fastboot devices
```
if nothing shows up, install proper drivers from [here](./01-resources.md)

to unlock bootloader, run:
```shell
fastboot flashing unlock
```

to lock bootloader, run:
```shell
fastboot flashing lock
```

### 2. Flashing recovery
Each recovery zip will have
- boot.img, dtbo.img, super_empty.img, vbmeta.img, vendor_boot.img
- flash.sh, flash.bat

first, reboot to bootloader, run:
```shell
adb reboot bootloader
```

second, Unzip the recovery zip and run:
```shell
./flash.bat // or flash.sh if your are on linux
```
this script flashes the above mentioned images with fastboot command and then reboots your phone into the recovery

### 3. Format Data
while in recovery, press `Factory reset` > then `Format data/Factory reset`

