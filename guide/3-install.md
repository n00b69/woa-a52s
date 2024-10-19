<img align="right" src="https://github.com/n00b69/woa-a52s/blob/main/a52s.png" width="350" alt="Windows 11 running on a52sxq">

# Running Windows on the Samsung Galaxy A52s

## Installing Windows

### Prerequisites
- [Modded TWRP](https://github.com/n00b69/woa-a52s/releases/download/Files/a52stwrp.tar)

- [Gdisk](https://github.com/n00b69/woa-winner/releases/tag/Gdisk)

- [Windows on ARM image](https://worproject.com/esd)
  
- [Drivers](https://github.com/n00b69/woa-a52s/releases/tag/Drivers)

- [UEFI image](https://github.com/n00b69/woa-a52s/releases/tag/UEFI)

### Boot into TWRP
> Hold **volume up** + **power** with the phone turned off, or with the phone turned on run
```cmd
adb reboot recovery
```

#### Execute the msc script
> If it asks you to run it once again, do so
```cmd
adb shell msc
```

### Windows Disk Management
- In your start menu, type "disk manager" and press enter.
- Look for your phone (which should be a 512GB disk) in disk manager.
- If it says **Offline**, right click the disk and set it to **Online**.

#### Gdisk
> Open **gdisk** as an admin, then run the following command in gdisk, replacing **$** with the actual number of the disk
```cmd
\\.\physicaldrive$
```

#### Restoring the GPT table
> In **gdisk**, run these commands individually in this exact order.
>
> If `y` does not work. type `yes y` instead.
```cmd
r
```
```cmd
c
```
```cmd
y
```
```cmd
w
```
```cmd
y
```

#### Reconnect your phone
> Simply replug the cable

### Diskpart
> [!WARNING]
> DO NOT ERASE, CREATE OR OTHERWISE MODIFY ANY PARTITION WHILE IN DISKPART!!!! THIS CAN ERASE ALL OF YOUR UFS OR PREVENT YOU FROM BOOTING TO FASTBOOT!!!! THIS MEANS THAT YOUR DEVICE WILL BE PERMANENTLY BRICKED WITH NO SOLUTION! (except for flashing it with [EDL](edl.md))
```cmd
diskpart
```

#### Select the Windows volume of the phone
> Use `list volume` to find it, replace `$` with the actual number of **WINA52S**
```diskpart
select volume $
``` 

#### Assign the letter X
```diskpart
assign letter x
``` 

#### Select the ESP volume of the phone
> Use `list volume` to find it, replace `$` with the actual number of **ESPA52S**
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
> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named install.wim or 22631.2861.XXXXXXX.esd)

```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:path\to\install.esd`, then replace `index:6` with the actual index number of **Windows 11 Pro** in your image

### Copying your boot.img into Windows
- Drag and drop the **rooted_boot.img** from the **platform-tools** folder into the **WINA52S** disk in Windows Explorer, then rename it to **boot.img**.

### Installing Drivers
- Unpack the driver archive, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINA52S** (which should be **X**), then press enter
  
#### Create Windows bootloader files
> If any error shows up, such as "Failure when attempting to copy boot files", open `diskpart` again and assign any new letter to **ESPA52S**, then replace the letter `Y` in the next commands with the letter that you just added.
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

#### Disabling failure checks
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" bootstatuspolicy IgnoreAllFailures
```

> [!WARNING]
>
> If your phone enters Windows [recovery mode](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference?view=windows-11), it will damage your UFS and permanently brick the device!
>
> This issue only occurs on Samsung devices running Windows.
>
> To make sure that never happens, it is strongly recommended to [follow this guide](https://github.com/Project-Silicium/WoA-Guides/blob/main/Mu-Qcom/Vendors/Samsung/remove-win-recovery-disk-checking.md).
> 
> Do not continue before completing all the steps in that guide.

#### Remove the drive letter for ESP
> If this does not work, ignore it and skip to the next command. This phantom drive will disappear the next time you reboot your PC.
```cmd
mountvol y: /d
```

### Reboot your device
```cmd
adb reboot
```

## [Last step: Setting up dualboot](/guide/4-dualboot.md)

















