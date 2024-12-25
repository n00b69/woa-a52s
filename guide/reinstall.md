<img align="right" src="https://github.com/n00b69/woa-a52s/blob/main/a52s.png" width="350" alt="Windows 11 running on a52sxq">

# Running Windows on the Samsung Galaxy A52s 5G

## Reinstalling Windows

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Modded TWRP](https://github.com/n00b69/woa-a52s/releases/download/Files/a52stwrp.tar) (should already be installed)

### Opening CMD as an admin
> Download **platform-tools** and extract the folder somewhere, then open CMD as an **administrator**.
>
> It is recommended to keep this window open and use it throughout the entire guide.
> 
> Replace `path\to\platform-tools` with the actual path to the platform-tools folder, for example **C:\platform-tools**.
```cmd
cd path\to\platform-tools
```

### Boot into the modded TWRP
> Run this command while booted into Android
>
> If you do not have TWRP intalled, flash it again using [these instructions](1-partition.md#flash-twrp-recovery)
```cmd
adb reboot recovery
```

### Formatting Windows and ESP partitions
```cmd
adb shell mkfs.ntfs -f /dev/block/by-name/win -L WINA52S
```

```cmd
adb shell mkfs.fat -F32 -s1 /dev/block/by-name/esp -n ESPA52S
```

## [Next step: Reinstalling Windows](3-install.md)



