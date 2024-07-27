# Magisk

!> Bootloader should be unlocked first

## Applying

!> This probably voids your warranty

1. Boot into device
2. Install Magisk apk
   * `adb install #magisk.apk`
3. Copy boot.img to device
   * `adb push boot.img /sdcard/Downloads`
4. Use Magisk app to modify boot.img
5. Download the resulting file
   * `adb pull /sdcard/Downloads/$(adb ls /sdcard/Downloads/magisk.*img)`
6. Reboot into bootloader
   * `adb reboot bootloader`
7. Flash the modified bootloader
   * `fastboot flash boot #magisk_boot.img`
8. Reboot to OS
   * `fastboot reboot`
9. Open Magisk app incase of follow up steps that may require additional reboots

## References
https://topjohnwu.github.io/Magisk/install.html#patching-images
