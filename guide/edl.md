<img align="right" src="https://github.com/n00b69/woa-a52s/blob/main/a52s.png" width="350" alt="Windows 11 running on a52sxq">

# Running Windows on the Samsung Galaxy A52s 5G

## Restoring your device in EDL mode
> You're probably reading this after installing Windows 11 24H2 and your device has become unoperational. There's good news: Your device can be recovered, and your data is not lost.

### Prerequisites
- [Qfil](https://github.com/n00b69/woa-betalm/releases/tag/Qfil)

- [A52s firehose](https://github.com/n00b69/woa-a52s/releases/download/Files/a52s_firehose_bit9.elf) (Thanks to [Arminas](https://github.com/arminask) 🙏)

- [A52s GPT backups](https://github.com/n00b69/woa-a52s/releases/download/Files/a52s_GPT.zip)

### Setting up Qfil
- Open **Qfil**.
- In "Select Build Type", select **flat build**.
- In "Select programmer", select the downloaded firehose.
- In "Configuration", make sure the "Device Type" is set to **UFS**.

#### Checking if EDL drivers are installed
- Open **Device Manager** on your PC and search for **Qualcomm HS-USB QDLoader 9008** in the **Ports (COM & LPT)** category of Device Manager.
- If the device is called **QUSB_BULK_CID** or has a ⚠️ yellow warning triangle / question mark, and is located in any other category (for example **Other devices**), you need to install EDL drivers first.
- To install EDL drivers, extract the contents of **QUD.zip** somewhere, right click on **QUSB_BULK_CID**, click on **Update driver** and **Browse my computer for drivers**, then find and select the **QUD** folder.

### Making sure Qfil works
- In **Qfil**, make sure the correct port is selected. If it says `No Port Available`, select the **Qualcomm HS-USB QDLoader 9008** port.
> Remember the `COM$` port number, as you will need it shortly.
- At the top, select "Tools" > "Partition manager", and click **Ok**.
- If you see a **Download Fail:Sahara Fail** error, make sure your cable stays connected and reboot to EDL again by holding **volume down** + **power**.
- Once you're back in EDL, try opening the Partition manager again.
- If it still fails, try to repeat the last step a few times. You can also try rebooting your phone and PC.

#### Minimize partition manager
> Once partition manager is open, leave it open in the background. Do not close it.

#### Copying GPT files
> Download and extract the GPT header files (**lun1-lun5_gpt_header.bin**) and copy them into `C:\Program Files (x86)\Qualcomm\QPST\bin`

### Opening CMD as an admin
> Open CMD as an admin, then run the following command to change the working directory
```cmd
cd "C:\Program Files (x86)\Qualcomm\QPST\bin"
```

#### Restoring LUN1 (sdb)
> Replace `COM$` with the actual port listed in Qfil, for example **COM8**
```cmd
.\fh_loader.exe --port=\\.\COM$ --sendimage=lun1_gpt_header.bin --start_sector=0 --lun=1 --noprompt --showpercentagecomplete --zlpawarehost=1 --memoryname=ufs
```

#### Restoring LUN2 (sdc)
> Replace `COM$` with the actual port listed in Qfil, for example **COM8**
```cmd
.\fh_loader.exe --port=\\.\COM$ --sendimage=lun2_gpt_header.bin --start_sector=0 --lun=2 --noprompt --showpercentagecomplete --zlpawarehost=1 --memoryname=ufs
```

#### Restoring LUN3 (sdd)
> Replace `COM$` with the actual port listed in Qfil, for example **COM8**
```cmd
.\fh_loader.exe --port=\\.\COM$ --sendimage=lun3_gpt_header.bin --start_sector=0 --lun=3 --noprompt --showpercentagecomplete --zlpawarehost=1 --memoryname=ufs
```

#### Restoring LUN4 (sde)
> Replace `COM$` with the actual port listed in Qfil, for example **COM8**
```cmd
.\fh_loader.exe --port=\\.\COM$ --sendimage=lun4_gpt_header.bin --start_sector=0 --lun=4 --noprompt --showpercentagecomplete --zlpawarehost=1 --memoryname=ufs
```

#### Restoring LUN5 (sdf)
> Replace `COM$` with the actual port listed in Qfil, for example **COM8**
```cmd
.\fh_loader.exe --port=\\.\COM$ --sendimage=lun5_gpt_header.bin --start_sector=0 --lun=5 --noprompt --showpercentagecomplete --zlpawarehost=1 --memoryname=ufs
```

### Reboot your device
- Hold the **volume down** + **power** button for +- 30 seconds and your device should hopefully turn on.

## Finished!


















