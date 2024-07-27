# Lenovo Tab M11 - TB330FU

Logically order of operations are:
1. Unlock bootloader
2. Apply Magisk
3. Apply GSI ROM

!> So far, this trips the dm-verity complaint and declares security level "Orange". So every reboot needs you to press the power button in the first 5s, and then it delays another 5s before startup. I haven't yet figured out a solution to this yet. The dm-verity complaint could be due to being unlocked without Lenovo's official `sn.img` file, I have no idea.

## Stock firmware bundles
```
52d5511d000440e02a54826be33971bf  TB330FU_ROW_OPEN_USER_V14.218_T_ZUI_15.1.072_ST_231208.zip
c476729184e1f8dc65bed72e978f4ed3  TB330FU_ROW_OPEN_USER_V15.155_U_ZUI_16.0.070_ST_240711.zip
```

## Unlock bootloader

!> This probably voids your warranty

### "Official"

1. Obtain serial-number-unique sn.img
   1. Download via `http://cdn.zui.lenovomm.com/developer/tabletboot/(your_sn_number)/sn.img`
      * This file did not work for me, kept geting error `remote: 'Invalid unlock image header'`
   1. Fill out form at https://www.zui.com/iunlock
      * This didn't work for me, never got the emails
      * Having the browser directly translate this page borks the form, so either copy+paste the text to translate, or open a second page for the translation.
      * Some people report Gmail is blocking their emails, etc. So may try a few times with different mail providers.
      * Too many attempts and they will start blocking submissions for that serial number. TBD if that gets cleared...
2. Enable `OEM Unlock` in Developers menu
3. Reboot into bootloader
   1. Power device off
   2. Vol Up + Power
   3. When prompted, press volume down
4. Run `fastboot flash unlock sn.img`
   * I could not obtain an sn.img file that worked
5. Assuming above worked, unlock the bootloader with whichever of the following is supported
   * `fastboot oem unlock-go`
   * `fastboot flashing unlock`
6. Reboot
   * `fastboot reboot`

### "Unofficial"

1. Obtain mtkclient https://github.com/bkerler/mtkclient
   * You can clone the repo, install deps, and go down that rabbit hole.
   * There's a LiveDVD with everything preinstalled
   * It didn't seem to have ADB or fastboot installed though.
     * `apt-get update; apt-get -y install adb fastboot`
2. Download + Boot into `re_livedvdV4.iso`
   * I could not get my Tablet to pass through VirtalBox in a way to be usable, as the device cycles a number of different USB devices
3. Enable `OEM Unlock` in Developers menu
4. Power down tablet
5. Plug in data cable, but don't power up the tablet
6. Open a terminal, goto the mtlclient folder
   * `cd /opt/mtkclient`
7. Clear misc userdata
   * `python mtk e metadata,userdata,md_udc`
8. Unlock the bootloader
   * `python mtk da seccfg unlock`
9. "Reset" the CPU
   * `python mtk reset`
   * You'll have to disconnect the data cable and reconnect to do further activities
10. Power up the device, the bootloader is now unlocked
   * Will probably have a dm-verity error


## References
https://github.com/bkerler/mtkclient

