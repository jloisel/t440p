# t440p

Thinkpad T440p Hackintosh configuration. 

Contains the following folders:

- `CLOVER`: put this in your EFI partition in `EFI` folder,
- `Kexts`: kexts to install in `Library/Extensions`.

Tested on High Sierra `10.13.6` and Mojave `10.14.2`.

What works:

- Power management,
- Temperature sensors,
- Battery status,
- Brightness control,
- Sound,
- USB ports,
- Graphical acceleration (QE/CI).

## HiDPI

For FHD (1920x1080) panels, I recommend to install [One Key HiDPI](https://github.com/xzhih/one-key-hidpi).

## Upgrade High Sierra => Mojave

Once the upgrade complete, make sure to rebuild the kext cache to fix brightness control issue, by running in Terminal:

```
sudo kextcache -i /
```

Then reboot.
