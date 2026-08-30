# Flashing Custom ROMs guide for OnePlus Nord CE3 5G (ziti)

>[!WARNING]
> Flashing firmware, unlocking the bootloader, rooting, modifying partitions, or relocking the bootloader can permanently damage or brick your device.
>
> You are responsible for anything you do to your device. This documentation is community-maintained and is provided without warranty.

## Prerequisites
- Make sure you have read the warning: [here](./00-warning.md)
- Install the required adb and fastboot drivers: [guide](./01-resources.md#latest-adbfastboot-installer-github--httpsgithubcomfawazahmed0latest-adb-fastboot-installer-for-windows)
- Download the required files:- [platform tools](./01-resources.md#platform-tools--httpsdeveloperandroidcomtoolsreleasesplatform-tools), recovery which the ROM maintainer recommends, ROM zip

>[!CAUTION]
> Your data will be lost during the process, please backup your data.
>[!TIP]
> Before installing custom ROM, backup your super.img and persist.img. More on that [here](./02-backup-super-persist.md)

## Steps
### 1. Unlock bootloader
>[!CAUTION]
> Unlocking bootloader is only possible on **OxygenOS 14** or above
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