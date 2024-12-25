<img align="right" src="https://github.com/n00b69/woa-a52s/blob/main/a52s.png" width="350" alt="Windows 11 running on a52sxq">

# Running Windows on the Samsung Galaxy A52s 5G

## Additional materials
> Below you will find a list of tweaks and materials for Windows on your ARM device

### List of supported apps/games
This is by no means a comprehensive list, it simply lists apps/games that have been tested by the community
[The link can be found here](https://docs.google.com/spreadsheets/d/1XYuoySgYQE0HL573sA-0RGMX7I4lt5rWJuQ8Z8yRJNY/edit?usp=drivesdk)

You can also find a list of dedicated ARM software [at this link](https://armrepo.ver.lt/)

#### Finished!

### Hide D drive (modem partition)
> [!NOTE]
> This is recommended because this drive should not be modified, while some applications may try to write to it

- Open a command prompt window and run ```diskpart```
- Run ```list volume``` to see all available volumes
- Select the disk that has letter D with ```select volume $```, replacing "$" with the volume number
- Remove the letter with ```remove letter d```
- Exit diskpart with ```exit```

#### Finished!

### Install Microsoft Office / Microsoft 365
- Download this [ISO file](https://mega.nz/file/hjAiSL4T#G7kOKpsUFpyL2UW9RQmY2e96urcQW5xZKdc7ciaNOy8) to the tablet
- Right-click on the iso file and select Mount to open it in explorer
- Double-click on ```Office Tool Plus.exe``` to start the installation wizard
- In the window that appears, click `Yes`
- Wait for the installation to complete

#### Finished!

### Activate Windows / Office
Follow the instructions by Massgravel [here](https://github.com/massgravel/Microsoft-Activation-Scripts)

#### Finished!

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




















