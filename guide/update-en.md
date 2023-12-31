<img align="right" src="https://raw.githubusercontent.com/graphiks/woa-raphael/65c0ee06045c13d1ef0f5f88aa687c50274ef7f5/raphael.png" width="350" alt="Windows 11 Running On A Redmi 9T Pro">


# Running Windows on the Redmi K20 Pro / Mi 9T Pro

## Reinstall guide
> This guide is used whenever you want to update or change your windows and / or driver installation.

### Prerequisites
- [TWRP](https://dl.twrp.me/raphael/twrp-3.7.0_9-0-raphael.img.html) (should already be installed)
- [DriverUpdater](https://github.com/WOA-Project/DriverUpdater/releases/tag/v1.9.0.0)
- [Drivers]() EDIT THIS
- [UEFI]() EDIT THIS
- [Msc script](https://cdn.discordapp.com/attachments/1148093151744118816/1158416286703943840/surfaceduo1-msc.tar)

## Reinstalling Windows
> [!IMPORTANT]
> If you have come here from the [troubleshooting page](troubleshooting.md) because you need to reinstall/update drivers, you can skip some steps. Make sure to read the guide properly.

##### Boot to TWRP
> If your recovery has been replaced with the stock recovery, flash it again in fastboot with:
```cmd
fastboot flash recovery path\to\twrp.img reboot recovery
```

##### Pushing the msc script
Extract the msc.sh and put it in the platform-tools folder, then run:
```cmd
adb push msc.sh /
```

##### Running the msc script
```cmd
adb shell sh msc.sh
```

## Opening diskpart
>  [!WARNING]
> DO NOT ERASE ANY PARTITION WHILE IN DISKPART!!!! THIS WILL ERASE ALL OF YOUR UFS!!!! THIS MEANS THAT YOUR DEVICE WILL BE PERMANENTLY BRICKED WITH NO SOLUTION! (except for taking the device to Xiaomi or flashing it with EDL, both of which will likely cost money)

After you hear your phone getting reconnected to your PC run:
```cmd
diskpart
```
> Run the following commands in the newly opened window

##### Finding your phone
```cmd
lis dis
```
> This will show all available disks. Find the disk number of your phone and replace it with "$" in the command below
```cmd
sel dis $
```

##### Selecting the ESP partition
```cmd
lis par
```
> This will print out all of the partitions in the selected disk. Check if they match up with your device and replace "$" with the number of the ESP partition (usually 30 or 31)
```cmd
sel par $
```

##### Formatting the ESP partition
> Skip this step if you are only reinstalling/updating drivers, or you will have to also reapply the image.
> This will format ESP to fat32
```cmd
format quick fs=fat32 label="System"
```

##### Add letter Y to the ESP partion
```cmd
assign letter y
```

##### Selecting the Windows partitiom
> Replace "$" in the command below with the number of the Windows partition, usually 31 or 32. If you don't know the number, run "lis par" again
```cmd
sel par $
```

##### Formatting the Windows partition
> Skip this step if you are only reinstalling/updating drivers, or you will have to also reapply the image.
> This will format Windows to NTFS
```cmd
format quick fs=ntfs label=Windows
```

##### Add letter X to the Windows partion
```cmd
assign letter x
```

##### Exit diskpart
```cmd
exit
```

## Installing Windows
> Skip this step if you are only reinstalling/updating drivers



## Finished!
