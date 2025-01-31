<img align="right" src="https://github.com/n00b69/woa-a52s/blob/main/a52s.png" width="350" alt="Windows 11 running on a52sxq">

# Running Windows on the Samsung Galaxy A52s 5G

## Additional materials
> Below you will find a list of tweaks and materials for Windows on your ARM device


### Check bootloader version
> Currently, only bootloader version 9 (BIT9) and below can be recovered for free.
> 
> If your device is running BIT10 firmware, it is not recommended to install Windows due to the risk of costly repairs if anything goes wrong.

How to check which BIT version you have? This is very simple.
- Go into your phone's Android settings.
- Go to **About phone** > **Software information** and look for **Baseband version**. It will look something like **A528BXXS4EWGB**.
- The first number near the middle after **A528...** will be the bootloader version. In this example the device would be running BIT8 firmware.
- If you do not see a number, it is highly likely that you are on BIT10 firmware.

#### Finished!


### List of supported apps/games
> These are by no means comprehensive lists, they do however list apps/games that have been tested by the community

- [Renegade Google Sheets list](https://docs.google.com/spreadsheets/d/1XYuoySgYQE0HL573sA-0RGMX7I4lt5rWJuQ8Z8yRJNY/edit?usp=drivesdk)

- [ARM Repo (native ARM software)](https://armrepo.ver.lt/)

- [News & supported applications](https://windowsonarm.org/)

#### Finished!


### Set up Android boot.img auto-flashing

>[!NOTE]
> Set up Android boot.img auto-flashing on Windows boot or when the battery is low (<15%) to prevent battery dies with uefi.img flashed. 

- Download the **boot.img auto-flasher** [here](https://github.com/Misha803/My-Scripts/releases/tag/boot.img-Auto-Flasher).
- Run it, click **INSTALL** button, select when should Android boot.img be auto-flashed (on Windows boot/Low battery) and wait for installation to complete.

#### Finished! 


### Install Microsoft Office
- Go to [Gravesoft's Office installer page](https://gravesoft.dev/office_c2r_links).
- Download the installer that fits your purposes. Make sure you select `Online x64`.
- Open the `setup.exe` and follow any instructions provided within.

#### Finished!


### Activate Windows / Office
- Follow the instructions by Massgravel [here](https://github.com/massgravel/Microsoft-Activation-Scripts)

#### Finished!


### Making the keyboard float
> [!WARNING]  
> Make sure these steps are done on the device running Windows, not your computer!

- Open CMD as an administrator and run ```reg delete HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Scaling /v MonitorSize```
- Press `y` then enter.
- Reboot your device.

##### Finished!








