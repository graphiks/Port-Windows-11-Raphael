<img align="right" src="https://raw.githubusercontent.com/graphiks/woa-raphael/65c0ee06045c13d1ef0f5f88aa687c50274ef7f5/raphael.png" width="350" alt="Windows 11 Running On A Poco X3 Pro">


# Running Windows on Redmi K20 Pro / Mi 9T Pro (raphael/raphaelin)

## Installation

## Partitioning your device

### Prerequisites

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

##### Flash the TWRP recovery
```cmd
fastboot flash recovery path\to\twrp.img
fastboot reboot recovery
```
##### Partition backup
> If you do anything incorrectly, you may wipe your UFS and render your device unusable.
Use TWRP to back up your Modem and EFS partition (as well as anything else if you have important data). Move this backup to a safe place (e.g your PC) as the next steps will wipe your data.

##### Partitioning guide

> If it asks you to run it once again, do so

> This is **optional** but you can **set custom sizes using this script**

> To set custom sizes do ```adb shell partition [TARGET WINDOWS SIZE IN GB]```

> Make sure you do not add GB at the end, just the number

```cmd
adb shell partition
```

#### Check if Android still starts
Just restart the phone, and see if Android still works


## [Next step: Installing Windows](/guide/install-2-en.md)
