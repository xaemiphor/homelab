# Lenovo Tab M10 Plus 3rd Gen - TB125FU

Logically order of operations are:
1. Unlock bootloader
2. Apply Magisk
3. Apply GSI ROM

!> This process will set security level "Orange", which will give a warning on every startup with a 5s delay. I have not yet figured out how to resolve that.

## Stock firmware bundles
```md5
bf7e87373410514d23dd74c3e445f5e9  TB125FU_S100105_230920_ROW.zip
```

## Unlock bootloader

!> This probably voids your warranty

1. Enable `OEM Unlock` in Developers menu
2. Reboot into bootloader
   * `adb reboot bootloader`
3. Unlock the bootloader
   * `fastboot flashing unlock`
   * Tablet screen will display a warning and expect the user to press the VolUp button twice to proceed, there is a timelimit
4. Reboot the device, the bootloader is now unlocked
   * `fastboot reboot`
