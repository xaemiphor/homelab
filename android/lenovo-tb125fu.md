# Lenovo Tab M10 Plus 3rd Gen - TB125FU

Logically order of operations are:
1. Unlock bootloader
2. Apply Magisk
3. Apply GSI ROM

!> This process will set security level "Orange", which will give a warning on every startup with a 5s delay. I have not yet figured out how to resolve that.

## Stock firmware bundles
```
```

## Unlock bootloader

!> This probably voids your warranty

1. Enable `OEM Unlock` in Developers menu
2. Reboot into bootloader
3. Unlock the bootloader
   * `fastboot flashing unlock`
   * Tablet screen will display a warning and expect the user to press the VolUp button twice to proceed, there is a timeout
4. Reboot the device, the bootloader is now unlocked
   * `fastboot reboot`
