<img align="right" src="https://github.com/n00b69/woa-a52s/blob/main/a52s.png" width="350" alt="Windows 11 running on a52sxq">

# Running Windows on the Samsung Galaxy A52s

## Partitioning your device

### Prerequisites
- Unlocked bootloader

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [Odin](https://github.com/n00b69/woa-a52s/releases/download/Files/Odin3_v3.14.4.zip)
  
- [Modded TWRP](https://github.com/n00b69/woa-a52s/releases/download/Files/a52stwrp.tar)

- [Patched vbmeta](https://github.com/n00b69/woa-a52s/releases/download/Files/a52svbmeta.tar)

### Notes
> [!WARNING]  
> 
> DO NOT REBOOT YOUR PHONE! If you think you made a mistake, ask for help in the [Telegram chat](https://t.me/a52sxq_uefi).
> 
> Do not run all commands at once, execute them in order!
>
> YOU CAN BREAK YOUR DEVICE WITH THE COMMANDS BELOW IF YOU DO THEM WRONG!!!

### Flash TWRP recovery
- Download **Odin3_v3.14.4.zip** and extract the contents somewhere, then open`Odin3_v3.14.4.exe`
- Turn off your phone, then connect it to your PC using a USB cable.
- Immediately start holding the **volume up** + **volume down** buttons to enter download mode.
- Click on **AP**, then select **a52stwrp.tar**.
- Click on **USERDATA**, then select **a52svbmeta.tar**.
- Click `Start` to begin flashing, then hold **volume up** + **power** right after to boot into the modded TWRP image

### Opening CMD as an admin
> Download **platform-tools** and extract the folder somewhere, then open CMD as an **administrator**.
>
> It is recommended to keep this window open and use it throughout the entire guide.
> 
> Replace `path\to\platform-tools` with the actual path to the platform-tools folder, for example **C:\platform-tools**.
```cmd
cd path\to\platform-tools
```

### Backing up important files
> This will back up **fsc**, **fsg**, **modemst1** and **modemst2** to the current path your CMD is opened in (for example **C:\platform-tools**). Confirm these files are actually there before proceeding.
> 
> Keep these backups in a safe place. If your device's software ever gets destroyed, you might need these backups or your phone could lose cellular capabilities.
>
> If you've got anything else you want to back up, do this now. Your Android data will be erased in the next steps.
```cmd
cmd /c "for %i in (fsg,fsc,modemst1,modemst2) do (adb shell dd if=/dev/block/by-name/%i of=/tmp/%i.bin & adb pull /tmp/%i.bin)"
```

#### Backing up your boot image
> This will back up your boot image in the current directory
```cmd
adb pull /dev/block/by-name/boot boot.img
```

### Partitioning guide
> Your Samsung Galaxy A52s may have different storage sizes. This guide uses the values of the 128GB model as an example. When relevant, the guide will mention if other values can or should be used.

#### Unmount data
```cmd
adb shell umount /dev/block/by-name/userdata
```

#### Preparing for partitioning
```cmd
adb shell parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions, userdata should be the last partition in the list.
```cmd
print
```

#### Removing userdata
> Replace **$** with the number of the **userdata** partition, which should be **34**
```cmd
rm $
```

#### Recreating userdata
> Replace **13.2GB** with the former start value of **userdata** which we just deleted
>
> Replace **90GB** with the end value you want **userdata** to have
```cmd
mkpart userdata ext4 13.2GB 90GB
```

#### Creating ESP partition
> Replace **90GB** with the end value of **userdata**
>
> Replace **90.3GB** with the value you used before, adding **0.3GB** to it
```cmd
mkpart esp fat32 90GB 90.3GB
```

#### Creating Windows partition
> Replace **90.3GB** with the end value of **esp**
>
> Only if you have the 256GB version, replace **127GB** with the end value of your disk, use `p free` to find it
```cmd
mkpart win ntfs 90.3GB 127GB
```

#### Making ESP bootable
> Use `print` to see all partitions. Replace "$" with your ESP partition number, which should be 35
```cmd
set $ esp on
```

#### Exit parted
```cmd
quit
```

### Rebooting recovery
> To fix partition symlinks
```cmd
adb reboot recovery
```

### Formatting Windows drive
```cmd
adb shell mkfs.ntfs -f /dev/block/by-name/win -L WINA52S
``` 

### Formatting ESP drive
```cmd
adb shell mkfs.fat -F32 -s1 /dev/block/by-name/esp -n ESPA52S
```

### Formatting data
- Format all data in TWRP, or Android will not boot.
- ( Go to Wipe > Format data > type yes )

#### Check if Android still starts
- Just restart the phone, and see if Android still works

## [Next step: Rooting your phone](/guide/2-root.md)





















