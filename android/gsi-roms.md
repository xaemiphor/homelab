# GSI ROMs

These are my notes only for A/B devices.

These commands don't work in the bootloader, only in fastboot mode.

## What is a GSI ROM?

ELI5 explanation by Microsoft Copilot:
> A GSI (Generic System Image) is a complete Android system image that can be installed on any device supporting Project Treble. It’s useful for compatibility, testing, and updates, but may lack some device-specific features. Developers often use GSIs for experimentation and customization.

## ROMs

Shy of AndyYans or TrebleDroid AOSP, feels like GSI ROMs aren't really out there. Check [Treble's WIKI](https://github.com/phhusson/treble_experimentations/wiki/Generic-System-Image-%28GSI%29-list) the next time I try to find something new again...

| State | Name | Notes |
| ---- | ---- | ---- |
| Active | [ImbrogliOS](https://xdaforums.com/t/gsi-14-imbroglios-v2024-08-09-aosp-android-14-0-0_r61-pure-full-edition.4681055/) [GH](https://github.com/imbroglius/imbroglios_gsi/releases/tag/v2024.08.18) | |
| Alive?/Beta | [LeafOS](https://leafos.org/) | Can't tell what version of Android it's based on, also was a pain to actually download the zip for some reason |
| Alive? | [RisingOS](https://sourceforge.net/projects/risingos-official/) [GH](https://github.com/ItsLynix/RisingTreble) | No web site? |
| Unofficial | [Evolution-X](https://github.com/ahnet-69/treble_evo) |  |
| Unofficial | [Andy Yan's Unofficial LineageOS GSI ROMs](https://sourceforge.net/projects/andyyan-gsi/files/) | I'm playing with `TD` builds, seems to work well and was able to cut down the Android Taskbar added in Android 13+ |
| Discontinued | [Pixel Experience](https://get.pixelexperience.org/) | Official ROMs are device targetted |
| Archived | [Pixel Experience Unofficial GSI ROMs](https://github.com/ponces/treble_build_pe/releases) | Looks abandoned/archived |
| Drama/Discontinued | [Project Elixir](https://projectelixiros.com/) | [Drama](https://www.reddit.com/r/Android/comments/1cvwd4f/comment/l58aoat/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button) |
| Abandoned | [pixelplusui](https://ppui.site) | ... Site looks like Elixir's, Patreon link points to same user... |

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
   * `fastboot reboot recovery`
5. Factory reset one last time
