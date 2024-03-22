<img align="right" src="https://github.com/n00b69/woa-alphaplus/blob/main/alphaplus.png" width="350" alt="Windows 11 running on alphaplus">

# Running Windows on the LG G8

## Updating drivers

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [Drivers](https://github.com/n00b69/woa-alphaplus/releases/download/Drivers/alphaplus-drivers.zip)

- [Qfil](https://github.com/n00b69/woa-alphaplus/releases/tag/Qfil)

- [Mass storage boot image]() FILE NEEDED

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
```cmd
diskpart
```

#### Select the phone's Windows volume
> Use `list volume` to find it, it should be named **WINMH2LM**
```diskpart
select volume <number>
```

#### Assign the letter x
```diskpart
assign letter x
```

#### Exit diskpart:
```diskpart
exit
```

### Installing Drivers
> Unpack the driver archive, then open the `OfflineUpdater.cmd` file

> Enter the drive letter of `Windows`, which should be X, then press enter

#### Reboot your device
> Once the drivers have finished installing

## Finished!

















