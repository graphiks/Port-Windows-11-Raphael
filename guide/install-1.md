<img align="right" src="https://raw.githubusercontent.com/graphiks/woa-raphael/65c0ee06045c13d1ef0f5f88aa687c50274ef7f5/raphael.png" width="350" alt="Windows 11 Running On A Redmi 9T Pro">


# Running Windows on the Redmi K20 Pro / Mi 9T Pro

## Installation

## Partitioning your device

### Prerequisites
- A brain
- [Raphael TWRP 3.7.0_9](https://dl.twrp.me/raphael/twrp-3.7.0_9-0-raphael.img.html)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

### Notes
> [!WARNING]  
> If you ever delete any partitions via diskpart, Windows will send a UFS command which would erase the entire UFS storage!
> 
> All your data will be erased! Backup now if needed.
> 
> Do not run the same command twice.
> 
> DO NOT REBOOT YOUR PHONE if you think you made a mistake, ask for help in the [Telegram chat](https://t.me/woaraphael).
> 
>
> Do not run all commands at once, execute them in order!
>
> YOU CAN BREAK YOUR DEVICE WITH THE COMMANDS BELOW IF YOU DO THEM WRONG!!!

> [!IMPORTANT]
> Make sure you use the provided TWRP Recovery throughout this whole tutorial as this will make it easier for you.
> 
> If you don't use it and you face any errors, consider it your fault and consider yourself alone if you try asking for support as you have deferred from the main guide.

##### Flash TWRP recovery
```cmd
fastboot flash recovery path\to\twrp.img reboot recovery
```

> [!IMPORTANT]
> If you do anything incorrectly, you may wipe your UFS and render your device unusable.

Use TWRP now to back up your Modem and EFS partition (as well as anything else if you have important data). Move this backup to a safe place (e.g your PC) as the next steps will wipe your data.

### Partitioning guide
> Your Redmi K20 Pro / Mi 9T Pro may have different storage sizes. Check free space using "(parted) free" and set the end value accordingly. This guide uses the values of the 128GB model.

##### Extending the partition limit
```cmd
adb shell sgdisk --resize-table=128 /dev/block/sda
```

##### Preparing for partitioning
> Run these commands seperately
```cmd
adb push parted /cache/
```

```cmd
adb shell "chmod 755 /cache/parted"
```

```cmd
adb shell /cache/parted /dev/block/sda
```

##### Printing the current table partition:
> Parted will print the list of partitions, userdata should be the last partition in the list.
```cmd
print
```

##### Resizing userdata
> Replace $ with the number of the userdata partition
```cmd
resizepart $
```
> Parted will now ask you for the end value.
> You can choose the size you want, as long as it is lower than the value it provides to you. In this example we resize it to 32GB
```cmd
32GB
```

##### Checking free space
```cmd
p free
```

##### Creating ESP partition
> 32GB is the **End** of the **userdata** partition and 32.5GB is the end of the ESP partition we will be creating, so it will be 500MB in size. Also replace 32GB to the end of userdata accordingly.
```cmd
mkpart esp fat32 32GB 32.5GB
```

> Replace "$" with your ESP partition number, usually 30, or 31
```cmd
set $ esp on
```

##### Creating Windows partition
> Here, 122GB is the end value of your phone's total storage. Replace with the end value you see when executing "p free"
> 32.5GB is the end of esp
```cmd
mkpart win ntfs 32.5GB 122GB
```

##### Exit parted
```cmd
quit
```

##### Formatting data
Format all data in TWRP, or Android will not boot.


#### Check if Android still starts
Just restart the phone, and see if Android still works


## [Next step: Installing Windows](/guide/install-2.md)
