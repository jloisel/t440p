![T440p MacOS Catalina](https://raw.githubusercontent.com/jloisel/t440p/master/t440p-macos-catalina.png)
*T440p running on MacOS Catalina with i5-4300m, 16GB RAM and 128GB mSata SSD Transcend MTS430S*

![T440p MacOS Mojave](https://raw.githubusercontent.com/jloisel/t440p/master/t440p-macos-mojave.jpg)
*T440p running on MacOS Mojave with i7 4712MQ, 16GB RAM and Western Digital 500GB SSD + 1TB HDD in Sata Ultrabay*

## What works


- Power management/sleep
- Brightness/Volume Control
- Battery Information
- Audio : from internal speaker and headphone jack
- USB Ports, Built-in Camera
- Graphics Acceleration
- FaceTime/iMessage
- DVD Drive
- Automatic OS updates
- Trackpoint/Touchpad (gestures and scrolling included)
- Dock USB ports
- Dock DisplayPorts, HDMI, DVI and VGA

## Known problems

- Ultra Dock problems (sleep/shutdown causes kernel panic and reboot when docked, also audio jack broken)
- SD card reader
- Automatic switching between internal and external speakers through jack (need to switch manually)


## Changelog
=======

### 3.2.2 (3rd October 2020)

- Remove audio fix scripts (not required anymore since we use VoodooHDA now)

### 3.2.1 (21th September 2020)

- Fix reboot after wake-up from sleep: replace AppleALC and CodecCommander by VoodooHDA `2.9.4` (#78)

### 3.2 (7th September 2020)

- Remoe [Intel Bluetooth driver](https://github.com/OpenIntelWireless/IntelBluetoothFirmware): conflicts with itwlm (See [#177](https://github.com/OpenIntelWireless/IntelBluetoothFirmware/issues/177))

### 3.1 (4th September 2020)

- Add [Intel Bluetooth driver](https://github.com/OpenIntelWireless/IntelBluetoothFirmware): Bluetooth now works with the integrated Intel wireless card
- Improve Audio fix
- Remove DW1820A Wi-fi configuration (as Integrated Intel Wi-fi works fine now)

### 3.0 (28th August 2020)

- Internal Intel Wifi now working thanks to [itwlm](https://github.com/OpenIntelWireless/itlwm)
- AppleALC `1.5.1`
- Lilu `1.4.6`
- WhateverGreen `1.4.1`
- Clover `r5121`


### 2.4 (27th July 2020)

HoRNDIS kext to support online USB installer through USB tethering (share wi-fi connection from your phone with the laptop through USB).

### 2.3 (17th April 2020)

- Clover r5112
- `USBPorts.kext` => `USBInjectAll.kext`
- AppleALC `1.4.8`
- Lilu `1.4.3`
- WhatEverGreen `1.3.8`
- VoodooPS2Controller `2.1.3`

### 2.2 (17th January 2020)

Custom USBPorts.kext (instead of USBInjectAll.kext) with support for docking station. (USB ports / Audio)

### 2.1 (17th December 2019)

Updated AppleALC, Lilu, WhatEvergreen and VoodooPS2.

### 2.0 (2nd December 2019)

Experimental Support for MacOS Catalina `10.15.x`. Tested on `10.15.1`.

### 1.4 (22th August 2019)

Separate DW1820 wifi card config.

### 1.3 (19th August 2019)

Special thanks to @ameeno for this release.

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
- `EFI/CLOVER/kexts/Other`: kexts to install in `/Library/Extensions` or your local drive once macOS has been installed.

Tested on High Sierra `10.13.6`, Mojave `10.14.6` and Catalina `10.15.6`.

It's a `99.99%` working hackintosh, including:

- *Apfs* and *HFS* disk partitions: using `ApfsDriverLoader-64.efi` and `HFSPlus-64.efi` respectively,
- **Power management**, **Temperature sensors**: Thanks to [FakeSMC](https://bitbucket.org/RehabMan/os-x-fakesmc-kozlek), which also emulates macbook pro hardware,
- **Battery status**: handled by [ACPIBatteryManager](https://bitbucket.org/RehabMan/os-x-acpi-battery-driver) kext,
- Brightness control: Thanks to [WhatEverGreen](https://github.com/acidanthera/WhateverGreen) kext,
- Audio on speakers: using VoodooHDA kext,
- USB ports: custom made inside SSDT-T440p.aml & USBInjectAll kext (Thanks to rehabman & Snikii,
- Graphical acceleration (QE/CI): thanks to [WhatEverGreen](https://github.com/acidanthera/WhateverGreen) kext.
- Audio Jack connector,
- Intel Wi-fi working with itwlm and [Heliport](https://github.com/OpenIntelWireless/HeliPort/releases),
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

## Bootable USB Drive

### From macOS

The guide [how to create a macOS USB Installer Drive](https://hackintosher.com/guides/how-to-make-a-macos-10-14-mojave-flash-drive-installer/) explains how to create a USB flash drive to install MacOs on your T440p.


### Copy EFI Folder to USB

Copy the content of the `EFI` folder provided here on your USB flash drive `EFI` partition. The EFI partition is usually hidden. Use [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/) to mount the EFI partition of your flash drive on your mac (it appears as a disk on the desktop once done).

### Install macOS

Install macOS by booting on the USB key. It takes about 30min. The computer will restart multiple times. Make sure to select `Install macOS ...` each time. Once installed, choose to boot from local drive in Clover boot menu.

### What's next?

To finish the setup, you need to:

- **Copy EFI** folder from USB flash drive to local drive `EFI` partition (like you did for the USB drive). It will make the local drive bootable (so you can get ride of the USB drive now),

You're done! Reboot and enjoy macOS on your Thinpad T440p.

## Miscellaneous

### Internet Connection needed for installing macOS

The problem is the following: for some reason when you write the USB from a PC (not a mac) it only writes the online installer, even though it downloads the full offline installer. Why? Good question, haven't figured out yet.
Why ethernet won't work? Because in mojave / catalina, recovery it's disabled.

Solutions:

- You'll need to have a wireless network card compatible with mac, OR
- use usb tethering your wifi from your phone.

This is why `HoRNDIS.kext` has been added to the kexts. Make sure to connect your android phone with an USB cable to your laptop when installing macOS. Share the phone wi-fi connection with the connected laptop.

### Integrated Intel Wi-fi

Once macOS is installed, install [Heliport](https://github.com/OpenIntelWireless/HeliPort/releases) and connect to your favorite wi-fi network. Add Heliport to startup programs to launch it automatically on macOS boot.


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

### Card Reader Driver

To fix get the card reader working on T440P, do the following (thank you to NoobsPlanet for the initial guide which I have modified specifically for the T440P):

- Open Finder and Goto S/L/E (System/Library/Extensions) and look for AppleStorageDriver.kext and copy this kext to Desktop
- Right Click in AppleStorageDriver.kext located at Desktop and select Show Package Contents and navigate to Contents > Plugins > Then find `AppleUSBCardReader.kext`,
- Right Click on `AppleUSBCardReader.kext` and select Show package Contents.
- Navigate to Contents and you'll find Info.plist,
- Right Click on Info.plist and open with Xcode or Plist Editor to edit a file.
- Find `IOKitPersonalities > AppleSDCardReader > Physical Interconnect Location` and then edit Physical Interconnect Location value section as External,
- Again find Vendor Identification and change value section to "Generic Reader by NoobsPlanet",
- Again find Apple_Internal_SD_Card_Reader_1_00 and edit sting value idProduct and idVenedor to decimal idProduct and idVendor, you can find Product ID and Vendor ID information in System Info into HEX value, so you need to convert it to Decimal Value. You can convert it online through https://www.binaryhexconverter.com/hex-t. On my T440P Product ID is 5227 and the HEX value is 21031. The Vendor ID is 10EC and the Hex value is 4332.
- Again find Apple_Internal_SD_Card_Reader_2_00 and edit the string value idProduct and idVendor to decimal value. (Use the same decimal value we did in above step)
- Make sure you change value for Physical Interconnect Location on Apple_internal_SD_Card_Reader_1_00 and Apple_Internal_SD_Card_Reader_2_00 to External
- Rename extension of original AppleStorageDriver.kext to .old
- Save the edited file and Copy AppleStorageDriver.kext and paste it into /System/Library/Extensions/ and replace the kext if asked.
- Open Terminal and fix permission and rebuild Kernel cache with following commands :

```bash
sudo chmod -R 755 /System/Library/Extensions/
sudo chown -R root:wheel /System/Library/Extensions/
sudo touch /System/Library/Extensions && sudo touch /Library/Extensions && sudo kextcache -u /
```

Reboot and enjoy working memory card!
