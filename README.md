# Thinkpad T440P Hackintosh

![T440p Hackintosh](https://raw.githubusercontent.com/jloisel/t440p/master/t440p-hackintosh.jpg)

## Changelog

### 1.3 (19th August 2019)

- DW1820A wifi card support (Full 5GHZ wifi and Bluetooth 4.1),
- Lighter Clover Theme,
- Modified Patched SSDT to have better working touchpad,
- Deleted all the unecesary ._ files in his repo,
- Removed unecesary drivers and kexts,
- Updated all the kexts and clover to the latest version,
- Removed unecessary Kext Files That could cause issues,
- Tested on Mojave `10.14.6`.

### 1.2 (3rd August 2019)

- Revert renaming LPC to LPCB (both in ACPI patch and config.plist) as it seems not to work properly.

### 1.1 (12th April 2019)

- Updated configuration tested with 10.14.4.

### 1.0.1 (18th January 2019)

- Remove unnecessary Kernel Extensions. Add HFS+ driver to support MacOS Journalized filesystem.

### 1.0.0 (3rd January 2019)

Initial Release.

## Introduction

Thinkpad T440p Hackintosh configuration. This repository contains the following folders:

- `EFI`: put this in your EFI partition in `EFI` folder, including `Boot` and `CLOVER` sub-folders,
- `Kexts`: kexts to install in `/Library/Extensions` or your local drive once macOS has been installed.

Tested on High Sierra `10.13.6` and Mojave `10.14.4`, `10.14.5` & `10.14.6`.

It's a `99.99%` working hackintosh, including:

- *Apfs* and *HFS* disk partitions: using `ApfsDriverLoader-64.efi` and `HFSPlus-64.efi` respectively,
- **Power management**, **Temperature sensors**: Thanks to [FakeSMC](https://bitbucket.org/RehabMan/os-x-fakesmc-kozlek), which also emulates macbook pro hardware,
- **Battery status**: handled by [ACPIBatteryManager](https://bitbucket.org/RehabMan/os-x-acpi-battery-driver) kext,
- Brightness control: Thanks to [WhatEverGreen](https://github.com/acidanthera/WhateverGreen) kext,
- Audio on speakers: using [AppleALC](https://github.com/acidanthera/AppleALC) kext,
- USB ports: custom made inside SSDT-T440p.aml & USBInjectAll kext (Thanks to rehabman & Snikii,
- Graphical acceleration (QE/CI): thanks to [WhatEverGreen](https://github.com/acidanthera/WhateverGreen) kext.
- Audio Jack connector,
- And Display Port external display.

## Setup

### Bios Settings

The bios must be properly configured prior to installing MacOS.

In `Security` menu, set the following settings:

- `Security > Security` Chip: must be **Disabled**,
- `Memory Protection > Execution Prevention`: must be **Enabled**,
- `Virtualization > Intel Virtualization Technology`: must be **Disabled**,
- `Internal Device Access > Bottom Cover Tamper Detection`: must be **Disabled**,
- `Anti-Theft > Current Setting`: must be **Disabled**,
- `Anti-Theft > Computrace > Current Setting`: must be **Disabled**,
- `Secure Boot > Secure Boot`: must be **Disabled**.

In `Startup` menu, set the following options:

- `UEFI/Legacy Boot`: **Both**,
- `UEFI/Legacy Priority`: **UEFI First**,
- `CSM Support`: **Yes**.

Now you can go through the install. 

### Bootable USB Drive

The guide [how to create a Mojave USB Installer Drive](https://hackintosher.com/guides/how-to-make-a-macos-10-14-mojave-flash-drive-installer/) explains how to create a USB flash drive to install MacOs on your T440p.

### Copy EFI Folder to USB

Copy the content of the `EFI` folder provided here on your USB flash drive `EFI` partition. The EFI partition is usually hidden. Use [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/) to mount the EFI partition of your flash drive on your mac (it appears as a disk on the desktop once done).

### Install macOS

Install macOS by booting on the USB key. It takes about 30min. The computer will restart multiple times. Make sure to select `Install macOS ...` each time. Once installed, choose to boot from local drive in Clover boot menu.

### What's next?

To finish the setup, you need to:

- **Copy EFI** folder from USB flash drive to local drive `EFI` partition (like you did for the USB drive). It will make the local drive bootable (so you can get ride of the USB drive now),
- **Install Kexts**: install kernel extensions provided by `Kexts` from this repository into `/Library/Extensions`.

Once kexts copied, run in *Terminal*:

```
sudo kextcache -i /
```

You're almost done! Reboot and enjoy macOS on your Thinpad T440p.

## Miscellaneous

##### Audio Jack

Thanks [Tony's T440p Guide](https://www.tonymacx86.com/threads/guide-lenovo-thinkpad-t440p.233282/) for help in getting this to work. By default, speaker audio should work, but audio via the headhpone jack does not.

**Installing ALC Fix**

- Copy the .zip file called `alc_fix.zip` inside the foldr `Audio` to the desktop,
- Open terminal and run:

```bash
cd Desktop/alc_fix
sudo su
./install.sh
```

The provided `config.plist` is already configured to use *Audio* layout `28`.

Reboot after installation. If you hear a strong white noise when connecting to audio jack, disconnect and reconnect your hearphones.

### SSD Enable Trim

If you Sata ssd hasn't trim enabled, run the following command from the *Terminal* to enable it:

```
sudo trimforce enable
```

### Touchpad / Trackpoint Kext

The trackpoint / Touchpad driver used here is the one from [tluck on Insanelymac](https://www.insanelymac.com/forum/topic/315451-guide-lenovo-t460-macos-with-clover/).

**Improving scrolling responsiveness**

Turn off 'inertia' at system-pref/accessibility/mouse & trackpad/trackpad options.

Insstall [Smart Scroll](https://www.marcmoini.com/sx_fr.html). under 'Scroll Wheel+' - Turn up 'Range for a single tick' to max. (this gives the appearance that scrolling becomes more sensitive)
Then you can adjust the speed and inertia under the same tab.

**Fix Stuttering**

To solve the jittery mouse, increase the speed with [BetterTouchTool](https://folivora.ai/) to about '8'. The touchpad feels almost the same as on my MacBook now, but the scrolling is still slow and awful. I will solve it somehow!

Special thanks to **Romeo Blues** for these tweaks. Those definitely improve how the touchpad feels!

### UltraBay HDD

When using HDD in Ultrabay (instead of optical drive): install [AHCIPortInjector.kext](https://www.insanelymac.com/forum/files/file/436-ahciportinjectorkext/) and [AppleAHCIPort.kext](https://www.insanelymac.com/forum/files/file/815-appleahciportkext/) in `/Library/Extensions`.

`AHCIPortInjector.kext` fixes the `Disk not initialized` issue (disk cannot be read). `AppleAHCIPort.kext` fixes the disk being detected as an external drive (instead of internal).

### HiDPI

For FHD (1920x1080) panels, I recommend to install [One Key HiDPI](https://github.com/xzhih/one-key-hidpi).

### High Sierra to Mojave Upgrade

Once the upgrade complete, make sure to rebuild the kext cache to fix brightness control issue, by running in Terminal:

```
sudo kextcache -i /
```

Then reboot.

### iMessage / iCloud / FaceTime

Make sure to following [this guide](https://hackintosher.com/guides/quick-fixes-facetime-icloud-imessage-hackintosh-not-working/) to configure iMessage, iCloud and Facetime properly. 
