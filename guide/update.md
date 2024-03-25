<img align="right" src="https://github.com/n00b69/woa-alphaplus/blob/main/alphaplus.png" width="350" alt="Windows 11 running on alphaplus">

# Running Windows on the LG G8

## Updating drivers

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [Drivers](https://github.com/n00b69/woa-alphaplus/releases/tag/Drivers)

- [Msc script](https://github.com/n00b69/woa-alphaplus/releases/download/Files/msc.sh)

- [TWRP or Orange Fox]() FILE NEEDED (should already be installed)

### Boot to recovery
> Boot to TWRP, Orange Fox, or Lineage Recovery

#### Running the msc script
> Put msc.sh in the platform-tools folder, then run:
```cmd
adb push msc.sh / && adb shell sh msc.sh
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

















