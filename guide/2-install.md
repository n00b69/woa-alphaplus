<img align="right" src="https://github.com/n00b69/woa-alphaplus/blob/main/alphaplus.png" width="350" alt="Windows 11 running on alphaplus">

# Running Windows on the LG G8

## Installing Windows

### Prerequisites
- [Windows on ARM image](https://worproject.com/esd)
  
- [Drivers](https://github.com/Icesito68/Port-Windows-11-Lge-devices/releases/download/Drivers/mh2lm.drivers.zip)

- [Parted script](https://github.com/Icesito68/Port-Windows-11-Lge-devices/releases/download/Files/parted)

- [TWRP or Orange Fox](https://github.com/Icesito68/Port-Windows-11-Lge-devices/releases/tag/Recoveries)

### Reboot to download mode
- Hold **volume down** + **power**.
- Keep holding as it displays the unlocked bootloader warning.
- After the screen turns dark, release the **power** button while continuing to hold the **volume up** button.
- While holding the **volume down** button, press the **volume up** button.

#### Setting up mass storage mode
```cmd
fastboot boot LGG8XMassStorageBoot.img
```

### Diskpart
> [!WARNING]
> DO NOT ERASE ANY PARTITION WHILE IN DISKPART!!!! THIS WILL ERASE YOUR ENTIRE UFS!!!! THIS MEANS THAT YOUR DEVICE WILL BE PERMANENTLY BRICKED WITH NO SOLUTION! (except for taking the device to Xiaomi or flashing it with EDL, both of which will likely cost money)

```cmd
diskpart
```

#### Finding your phone
> This will list all connected disks
```cmd
lis dis
```

#### Selecting your phone
> Replace $ with the actual number of your phone (it should be the last one)
```cmd
sel dis $
```

#### Listing your phone's partitions
> This will list your device's partitions
```cmd
lis par
```

#### Selecting the Windows partition
> Replace $ with the partition number of Windows (should be 32)
```cmd
sel par $
```

#### Formatting Windows drive
```cmd
format quick fs=ntfs label="WINMH2LM"
```

#### Add letter to Windows
```cmd
assign letter x
```

#### Selecting the ESP partition
> Replace $ with the partition number of ESP (should be 31)
```cmd
sel par $
```

#### Formatting ESP drive
```cmd
format quick fs=fat32 label="ESPMH2LM"
```

#### Add letter to ESP
```cmd
assign letter y
```

#### Exit diskpart
```cmd
exit
```

### Reboot to recovery
> Reboot to recovery. Reinstall the Magisk recovery module if needed

#### Running parted
```cmd
adb push parted /cache/ && adb shell "chmod 755 /cache/parted" && adb shell /cache/parted /dev/block/sda
```

#### Making ESP bootable
> Use `print` to see all partitions. Replace "$" with your ESP partition number, which should be 31
```cmd
set $ esp on
```

#### Exit parted
```sh
quit
```

### Installing Windows
> Replace `<path\to\install.esd>` with the actual path of install.esd (it may also be named install.wim)

```cmd
dism /apply-image /ImageFile:<path\to\install.esd> /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:<path\to\install.esd>`, then replace `index:6` with the actual index number of Windows 11 Pro in your image

#### Installing drivers
> Unpack the driver archive, then open the `OfflineUpdater.cmd` file

> Enter the drive letter of `WINMH2LM`, which should be X, then press enter
  
#### Create the Windows bootloader files
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

#### Reboot back to Android
Simply reboot your device

## [Last step: let's setup dualboot](dualboot.md)
















