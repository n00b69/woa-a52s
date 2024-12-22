<img align="right" src="https://github.com/n00b69/woa-a52s/blob/main/a52s.png" width="350" alt="Windows 11 running on a52sxq">

# Running Windows on the Samsung Galaxy A52s

## Uninstalling Windows

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Modded TWRP](https://github.com/n00b69/woa-a52s/releases/download/Files/a52stwrp.tar) (should already be installed)

### Boot into the modded TWRP
> Run this command while booted into Android
>
> If you do not have TWRP intalled, flash it again using [these instructions](1-partition.md#flash-twrp-recovery)
```cmd
adb reboot recovery
```

### Run the restore script
> This will delete all your data, so back up anything beforehand if needes
```cmd
adb shell restore
```

#### Reboot your phone
> To check if Android works
```cmd
adb reboot
```
> [!Note]
> If Android does not boot, return to TWRP and perform a factory reset
- Go to the Wipe menu in TWRP and press **Format Data**, then type `yes`


## Finished!

















