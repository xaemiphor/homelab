# GSI ROMs

These are my notes only for A/B devices.

These commands don't work in the bootloader, only in fastboot mode.

## What is a GSI ROM?

ELI5 explanation by Microsoft Copilot:
> A GSI (Generic System Image) is a complete Android system image that can be installed on any device supporting Project Treble. It’s useful for compatibility, testing, and updates, but may lack some device-specific features. Developers often use GSIs for experimentation and customization.

## ROMs

| Name | Notes |
| ---- | ---- |
| [Andy Yan's Unofficial LineageOS GSI ROMs](https://sourceforge.net/projects/andyyan-gsi/files/) | I'm playing with `TD` builds, seems to work well and was able to cut down the Android Taskbar added in Android 13+ |
| [Pixel Experience](https://get.pixelexperience.org/) | Official ROMs are device targetted |
| [Pixel Experience Unofficial GSI ROMs](https://github.com/ponces/treble_build_pe/releases) | Looks abandoned/archived |


## Applying

!> This probably voids your warranty

1. Boot into fastboot mode(not bootloader)
   * `fastboot reboot fastboot`
   * `adb reboot fastboot`
2. Use fastboot(the cli) to wipe product_a and product_b
   * `fastboot delete-logical-partition product_a`
   * `fastboot delete-logical-partition product_b`
3. Use fastboot(the cli) to flash the GSI image to system partition
   * `fastboot flash system #_.img`
4. Reboot to recovery
5. Factory reset one last time
