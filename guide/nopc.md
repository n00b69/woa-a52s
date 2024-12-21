<img align="right" src="https://github.com/n00b69/woa-a52s/blob/main/a52s.png" width="350" alt="Windows 11 running on a52sxq">

# Running Windows on the Samsung Galaxy A52s

## Installing Windows without a PC

### Prerequisites
- A rooted A52s

- [Termux](https://play.google.com/store/apps/details?id=com.termux) or TWRP already installed

- [Modified TWRP](https://github.com/n00b69/woa-a52s/releases/download/Files/a52stwrp.img) and [Patched vbmeta](https://github.com/n00b69/woa-a52s/releases/download/Files/a52svbmeta.img)

- [A52s WinInstaller](https://github.com/n00b69/woa-a52s/releases/download/Files/A52sWinInstaller_v6.9.zip)

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
> Run the below two commands in this terminal

### Setting GPT online
> Or Windows will not boot
```cmd
fix-gpt
```

### Run the partitioning script
> After running the script, enter the size (in GB) that you want Windows to be
>
> Do not write **GB**, just the number (for example **50**)
```cmd
partition
``` 

#### Check if Android still starts
- Just restart the phone, and see if Android still works.
- If it doesn't, boot back into TWRP and format data. 

### Preparing necessary files
- Download the Windows image and make sure it remains in the `Download` folder of your **internal storage**.
- Download **WinInstaller.zip** and keep it in the `Download` folder as well.
- Download and install the [WOA Helper app](https://github.com/n00b69/woa-helper/releases/tag/APK), then open it and grant it root access. Do not do anything else inside the app yet.

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
> [!Warning]
> DO NOT SKIP THIS STEP

> Do this immediately after booting into Windows, if you don't, Windows may brick your device later.
- Navigate to `C:\RUN-THIS-IMMEDIATELY` and open **GPTfix.cmd**.

#### Booting to Android
- Run the **Android** shortcut on your desktop (you can also pin it to your start menu / taskbar for ease of access).

#### Booting to Windows
- Press **QUICKBOOT TO WINDOWS** inside the WOA Helper app, or use the newly created toggle in your quick settings panel.

## Finished!


















