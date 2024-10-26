<img align="right" src="https://github.com/n00b69/woa-a52s/blob/main/a52s.png" width="350" alt="Windows 11 running on a52sxq">

# Running Windows on the Samsung Galaxy A52s

## Uninstalling Windows

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Modded TWRP](https://github.com/n00b69/woa-a52s/releases/download/Files/a52stwrp.tar) (should already be installed)

#### Boot into the modded TWRP
> Run this command while booted into Android
>
> If you do not have TWRP intalled, flash it again using [these instructions](1-partition.md#flash-twrp-recovery)
```cmd
adb reboot recovery
```

#### Unmount data
```cmd
adb shell umount /dev/block/by-name/userdata
```

### Run parted
```cmd
adb shell parted /dev/block/sda
```

#### Delete Windows Partition
> Use `print all` to make sure that partition 36 is Windows
```sh
rm 36
```

#### Delete ESP Partition
> Use `print all` to make sure that partition 35 is ESP
```sh
rm 35
```

#### Resize userdata Partition
> Use `print all` to make sure that partition 34 is userdata
>
> Only if you have the 256GB version, replace **127GB** with the end value of your disk, use `p free` to find it
```sh
resizepart 34
127GB
```

#### Exit Parted
```sh
quit
```

### Format data
Go to the Wipe menu in TWRP and press Format Data, then type `yes`

#### Check if Android boots
Reboot your device and check if Android boots.

## Finished!

















