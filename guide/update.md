<img align="right" src="https://github.com/n00b69/woa-alphaplus/blob/main/alphaplus.png" width="350" alt="Windows 11 running on alphaplus">

# Running Windows on the LG G8

## Updating drivers

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Qfil](https://github.com/n00b69/woa-alphaplus/releases/tag/Qfil)

- [Engineering ABL](https://github.com/n00b69/woa-alphaplus/releases/download/Files/engabl_ab.bin)
  
- [Drivers](https://github.com/n00b69/woa-alphaplus/releases/tag/Drivers)

- [Mass storage image](https://github.com/n00b69/woa-alphaplus/releases/download/Files/msc.img)

### Boot to EDL
> If fastboot works on your device by default, skip to the "Reboot to fastboot mode" step
- Open **Device Manager** on your PC
- With the phone turned off, hold **volume down** + **power**.
- After the screen turns dark, while still holding **volume down** + **power**, start rapidly pressing the **volume up** button.
- Keep doing this until you see **QDLoader 9008** or **QUSB_BULK** in the Device Manager on your PC.
- If the device has a ⚠️ yellow warning triangle, you need to install EDL drivers before you can continue to the next step.

#### Setting up Qfil
- Open **Qfil**.
- In "Select Build Type", select **flat build**.
- In "Select programmer", select the downloaded firehose.
- In Configuration, make sure the "Device Type" is set to **UFS**.

### Flashing engineering ABL
> Make sure you've made abl backups before
- In **Qfil**, select Tools > Partition manager, and click **Ok**.
- Right click on **abl_a** > **Manage Partition Data** and press **Load Image**.
- Select and flash the **engabl_ab.bin** file.
- Do the same thing for **abl_b**.

### Reboot to fastboot mode
- Force reboot your phone by holding **volume down** + **power** until you see the LG logo.
- With the device turned off, hold the **volume down** button, then plug the cable in.
- If the phone in device manager is called **Android** and has a ⚠️ yellow warning triangle, you need to install fastboot drivers before you can continue.

#### Boot to the mass storage mode UEFI
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
> After 1-2 minutes **WINALPHA** should automatically appear in Windows Explorer. If it does, skip to the "Installing drivers" step, else continue with the "Diskpart" steps.

### Diskpart
```cmd
diskpart
```

#### Select the phone's Windows volume
> Use `list volume` to find it, replace `$` with the actual number of **WINALPHA**
```diskpart
select volume $
```

#### Assign the letter x
```diskpart
assign letter x
```

#### Exit diskpart
```diskpart
exit
```

### Installing Drivers
> Unpack the driver archive, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINALPHA** (which should be **X**), then press enter

### Reboot back to edl
> To restore your original abl
- In **Qfil**, select Tools > Partition manager, and click **Ok**.
- Right click on **abl_a** > **Manage Partition Data** and press **Load Image**.
- Select and flash the **abl_a.bin** file you've hopefully backed up before that is located in `C:\Users\YOURNAME\AppData\Roaming\Qualcomm\QFIL\COMPORT_#\`
- Do the same thing for **abl_b**.

### Reboot your device
> Force reboot your phone by holding **volume down** + **power** until you see the LG logo.
>
> If you end up in Android instead of Windows, simply use the WOA Helper app to switch back.

## Finished!





















