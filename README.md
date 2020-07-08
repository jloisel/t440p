This is a fork of [https://github.com/jloisel/t440p](https://github.com/jloisel/t440p).	  
The main differences are: 
- Voodoo-Kexts have bee replaced with the ones from [https://notthebee/t440p-hackintosh](https://github.com/notthebee/t440p-hackintosh) 
- Removed uneccessary step to install kexts to /Library/Extension
- Replaced Lilu and AppleALC 
- Updated clover 
Thinkpad T440p Hackintosh configuration. This repository contains the following folders:

Tested on High Sierra, Mojave and Catalina.

It's a `99.99%` working Hackintosh, including: 

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

You're almost done! Reboot and enjoy macOS on your Thinpad T440p.

## Miscellaneous

### Audio Jack

Thanks [Tony's T440p Guide](https://www.tonymacx86.com/threads/guide-lenovo-thinkpad-t440p.233282/) for help in getting this to work. By default, speaker audio should work, but audio via the headhpone jack does not.

**Installing ALC Fix**

- Open terminalm head into `t440p/Audio Fix` and run:

```bash
sudo ./install.sh
```

Reboot after installation. 

### SSD Enable Trim

If you Sata ssd hasn't trim enabled, run the following command from the *Terminal* to enable it:

```
sudo trimforce enable
``` 

### iMessage / iCloud / FaceTime

Make sure to following [this guide](https://hackintosher.com/guides/quick-fixes-facetime-icloud-imessage-hackintosh-not-working/) to configure iMessage, iCloud and Facetime properly. 