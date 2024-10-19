<img align="right" src="https://github.com/n00b69/woa-a52s/blob/main/a52s.png" width="350" alt="Windows 11 running on a52sxq">

# Running Windows on the Samsung Galaxy A52s

## Installing Windows without a PC
> [!Warning]
> THIS GUIDE IS NOT YET FINISHED AND MAY NOT WORK. DO NOT USE IT UNTIL YOU SEE THIS WARNING GONE.
>
> AT BEST, IT WILL WORK
>
> AT WORST, YOUR DEVICE MAY BRICK
>
> JOIN THE [TELEGRAM CHAT](https://t.me/a52sxq_uefi) FOR FURTHER SUPPORT

### Prerequisites
- A rooted A52s

- [A52s WinInstaller](https://github.com/n00b69/woa-a52s/releases/download/Files/A52sWinInstaller_v6.8.zip)

- [Windows on ARM image](https://worproject.com/esd)

- [Modified TWRP]() zzzzzzzzzzz

- [WOA Helper app](https://github.com/Marius586/WoA-Helper-update/releases/tag/WOA)

### Notes
> [!WARNING]  
> All your data will be erased! Back up now if needed.
> 
> DO NOT REBOOT YOUR PHONE if you think you made a mistake, ask for help in the [Telegram chat](https://t.me/a52sxq_uefi).

> [!Important]
> This guide assumes you have already unlocked your bootloader and are already rooted, if this is not the case, you'll still need a PC to do that.

### Flash the modified TWRP
- Zzzzzzzz

#### Opening TWRP terminal
- Once booted into TWRP press the **Advanced** button on the bottom right of the screen, then press **Terminal**.
- Run all future commands in this terminal

#### Unmount data
```cmd
umount /dev/block/by-name/userdata
```

#### Preparing for partitioning
```cmd
parted /dev/block/sda
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
> Replace **90GB** with the end value you want **userdata** to have. In this example your available usable space in Android will be 90GB-13.2GB = 76.8GB
```cmd
mkpart userdata ext4 13.2GB 90GB
```

#### Creating ESP partition
> Replace **90GB** with the end value of **userdata**
>
> Replace **90.35GB** with the value you used before, adding **0.35GB** to it
```cmd
mkpart esp fat32 90GB 90.35GB
```

#### Creating Windows partition
> Replace **90.35GB** with the end value of **esp**
>
> Replace **127GB** with the actual end value of your disk (if your device is the 128GB version, leave it as 127GB)
```cmd
mkpart win ntfs 90.35GB 127GB
```

#### Making ESP bootable
> Use `print` to see all partitions. Replace "$" with your ESP partition number, which should be **35**
```cmd
set $ esp on
```

#### Exit parted
```cmd
quit
```

### Formatting data and rebooting
- Format all data in TWRP, or Android will not boot.
- ( Go to Wipe > Format data > type `yes` ).
- Press the reboot button to reboot into Android.

### Preparing necessary files
- Download the Windows image and make sure it remains in the `Download` folder of your **internal storage**.
- Download **WinInstaller.zip** and keep it in the `Download` folder as well.
- Download and install the [WOA Helper app](https://github.com/Marius586/WoA-Helper-update/releases/tag/WOA), then open it and grant it root access. Do not do anything else inside the app yet.

### Booting into TWRP
- Press the `Reboot to Recovery` button in the top right of Magisk again.
- Once booted into TWRP, enter your password if it asks you to.

### Flashing WinInstaller
- In TWRP, select **Install** and then locate **WinInstaller.zip** and flash it.
> [!Note]
> Wait untill all processes complete and your device boots into Windows. This will take around 15-20 minutes.

> [!Tip]
> If you wish to skip the Microsoft Account login, press the **I don't have internet** button in the WiFi page, then when prompted, press the **Continue with limited setup** button.

#### Booting to Android
- Run the **Android** shortcut on your desktop (you can also pin it to your start menu / taskbar for ease of access).

#### Booting to Windows
- Press **QUICKBOOT TO WINDOWS** inside the WOA Helper app, or use the newly created toggle in your quick settings panel.

## Finished!


















