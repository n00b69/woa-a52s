<img align="right" src="https://github.com/n00b69/woa-a52s/blob/main/a52s.png" width="350" alt="Windows 11 running on a52sxq">

# Running Windows on the Samsung Galaxy A52s

## Installing Windows without a PC

### Prerequisites
- A rooted A52s

- [Termux](https://play.google.com/store/apps/details?id=com.termux) or TWRP already installed

- [Modified TWRP](https://github.com/n00b69/woa-a52s/releases/download/Files/a52stwrp.img) and [Patched vbmeta](https://github.com/n00b69/woa-a52s/releases/download/Files/a52svbmeta.img)

- [A52s WinInstaller](https://github.com/n00b69/woa-a52s/releases/download/Files/A52sWinInstaller_v6.8.1.zip)

- [Windows on ARM image](https://worproject.com/esd)

- [WOA Helper app](https://github.com/n00b69/woa-helper/releases/tag/APK)

### Notes
> [!WARNING]  
> All your data will be erased! Back up now if needed.
> 
> DO NOT REBOOT YOUR PHONE if you think you made a mistake, ask for help in the [Telegram chat](https://t.me/a52sxq_uefi).

> [!Warning]
> DO NOT INSTALL WINDOWS IF YOUR A52S IS RUNNING **BIT10 FIRMWARE**
> 
> If your device happens to get bricked, recovery will be very expensive.

> [!Important]
> This guide assumes you have already unlocked your bootloader and are already rooted, if this is not the case, you'll still need a PC to do that.

### Flash the modified TWRP
> If you already have a TWRP installed, you can instead also boot into TWRP and flash the modified TWRP using the **Install** button.
- Download **Termux** and grant it root access.
- Download the **modified TWRP** and **patched vbmeta** files and leave them in your download folder in your internal storage.
- In **Termux** run the below two commands seperately.
```cmd
su -c dd if=/sdcard/Download/a52svbmeta.img of=/dev/block/by-name/vbmeta
```

```cmd
su -c dd if=/sdcard/Download/a52stwrp.img of=/dev/block/by-name/recovery bs=8M
```

#### Boot into the modified TWRP
> Run this command in Termux as well
```cmd
su -c reboot recovery
```

#### Opening TWRP terminal
- Once booted into TWRP press the **Advanced** button on the bottom right of the screen, then press **Terminal**.
> Run all future commands in this terminal

### Setting GPT online
> Or Windows will not boot
```cmd
fix-gpt
```

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
```cmd
mkpart win ntfs 90.35GB -0MB
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

### Fixing GPT
> Do this immediately after booting into Windows, if you don't, Windows may brick your device later.
- Navigate to `C:\RUN_GPT_FIX_ASAP` and open **flash-GPT.cmd** as an administrator.

#### Booting to Android
- Run the **Android** shortcut on your desktop (you can also pin it to your start menu / taskbar for ease of access).

#### Booting to Windows
- Press **QUICKBOOT TO WINDOWS** inside the WOA Helper app, or use the newly created toggle in your quick settings panel.

## Finished!


















