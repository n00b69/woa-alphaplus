<img align="right" src="https://github.com/n00b69/woa-alphaplus/blob/main/alphaplus.png" width="350" alt="Windows 11 running on alphaplus">

# Running Windows on the LG G8

## Installing Windows

### Prerequisites
- [Mass storage image](https://github.com/n00b69/woa-alphaplus/releases/download/Files/msc.img)

- [Windows on ARM image](https://arkt-7.github.io/woawin/)
  
- [Drivers](https://github.com/n00b69/woa-alphaplus/releases/tag/Drivers)

- [UEFI image](https://github.com/n00b69/woa-alphaplus/releases/tag/UEFI)

### Reboot into fastboot mode
- With the device turned off, hold the **volume down** button, then plug the cable in.

#### Boot into the mass storage mode image
> Replace `path\to\msc.img` with the actual path of the image
```cmd
fastboot boot path\to\msc.img
```

#### Enabling mass storage mode
> Once booted into the UEFI, use the volume buttons to navigate the menu and the power button to confirm
- Select **UEFI Boot Menu**.
- Select **USB Attached SCSI (UAS) Storage**.
- Press the **power** button twice to confirm.

> [!Note]
> If you are facing issues (e.g your device randomly reboots), follow [the steps described in this guide](https://github.com/n00b69/woa-betalm/blob/main/guide/troubleshooting.md#the-device-reboots-in-mass-storage-mode) for an alternative way of entering mass storage mode.

### Diskpart
> [!WARNING]
> DO NOT ERASE, CREATE OR OTHERWISE MODIFY ANY PARTITION WHILE IN DISKPART!!!! THIS CAN ERASE ALL OF YOUR UFS OR PREVENT YOU FROM BOOTING TO FASTBOOT!!!! THIS MEANS THAT YOUR DEVICE WILL BE PERMANENTLY BRICKED WITH NO SOLUTION! (except for flashing it with EDL, which is complicated)
```cmd
diskpart
```

#### Select the Windows volume of the phone
> Use `list volume` to find it, replace `$` with the actual number of **WINALPHA**
```diskpart
select volume $
```

#### Assign the letter X
```diskpart
assign letter x
```

#### Select the ESP volume of the phone
> Use `list volume` to find it, replace `$` with the actual number of **ESPALPHA**
```diskpart
select volume $
```

#### Assign the letter Y
```diskpart
assign letter y
```

#### Exit diskpart
```cmd
exit
```

### Installing Windows
> [!Important]
> For performance reasons, it is recommended to use Windows 11 24H2 (builds that start with 261XX, such as 26100.2454)

> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named install.wim or 22631.2861.XXXXXXX.esd)

```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:path\to\install.esd`, then replace `index:6` with the actual index number of **Windows 11 Pro** in your image

### Copying your boot.img into Windows
- Drag and drop the **rooted_boot.img** from the **platform-tools** folder into the **WINALPHA** disk in Windows Explorer, then rename it to **boot.img**

### Installing drivers
- Unpack the driver archive, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINALPHA** (which should be **X**), then press enter
  
#### Create the Windows bootloader files
> If any error shows up, such as "Failure when attempting to copy boot files", open `diskpart` again and assign any new letter to **ESPBETALM**, then replace the letter `Y` in the next commands with the letter that you just added.
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Enabling test signing
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Disabling recovery
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

#### Disabling integrity checks
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

#### Remove the drive letter for ESP
> If this does not work, ignore it and skip to the next command. This phantom drive will disappear the next time you reboot your PC.
```cmd
mountvol y: /d
```

### Rebooting into fastboot mode
- Reboot into fastboot mode by holding the **volume down** + **power** buttons until the text on the screen disappears, then immediately release the **power** button whilst continuing to hold **volume down**.
> If your phone turns on instead, turn it off while the cable is plugged in, and keep holding tbe **volume down** button until it enters fastboot mode.

### Boot into the UEFI
> Replace `path\to\alpha-uefi.img` with the actual path of the image
```cmd
fastboot boot path\to\alpha-uefi.img
```

### Reboot into Android
Your device should reboot by itself after +- 10 minutes of waiting, after which you will be booted into Android, for the last step.

## [Last step: Setting up dualboot](4-dualboot.md)






















