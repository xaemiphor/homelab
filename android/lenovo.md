# Lenovo notes

## Unlocking bootloaders

It seems some models can be simply unlocked with fastboot, others require a serialnumber-unique `sn.img` file.

## dm-verity corruption error

Some articles online report this can be fixed by booting into the bootloader and running
```
fastboot oem cdms
```
Presence of this command varies by device

## Downgrading using RSA utility
1. Install Lenovo RSA
2. Download old firmware from somewhere
3. Plugin Device
4. Download latest firmware, but do not apply
5. Rename firmware folder in `C:\ProgramData\RSA\Download\RomFiles` to something else
6. Create empty folder of same name, extract old firmware to it
7. Start rescue procedure in RSA

## References
https://github.com/bkerler/mtkclient/issues/261
