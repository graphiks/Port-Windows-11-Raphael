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

> Replace `path\to\install.wim` with the actual path to install.wim.

> If you are using an ISO file, it is located in the sources folder inside the ISO. Mount the ISO with Windows Explorer and then copy the path to it.
> Alternatively, use one of the install.esd files from the Google Drive at the top of this page. Touch doesn't seem to work on 23h2, so use 22h2.

```cmd
dism /apply-image /ImageFile:path\to\install.wim /index:1 /ApplyDir:X:\
```

##### Installing Drivers
EDIT THIS

##### Create Windows bootloader files
> Skip this step if you are only reinstalling/updating drivers
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

###### Configuring bootloader files
> Skip this step if you are only reinstalling/updating drivers
> Run these 4 commands seperately
```cmd
cd Y:\EFI\Microsoft\Boot
```
```cmd
bcdedit /store BCD /set "{default}" testsigning on
```
```cmd
bcdedit /store BCD /set "{default}" nointegritychecks on
```
```cmd
bcdedit /store BCD /set "{default}" recoveryenabled no
```

##### Unassign disk letters
> So that they don't stay there after disconnecting the device
```cmd
diskpart
```

##### Select the Windows volume of the phone
> Use `lis vol` to find it, it's the one named "Windows"
```diskpart
select volume <number>
```
##### Unassign the letter X
```diskpart
remove letter x
```

##### Select the ESP volume of the phone
> Use `list volume` to find it, it's the one named "ESP"
```diskpart
select volume <number>
```
##### Unassign the letter Y
```diskpart
remove letter y
```

##### Exit diskpart
```diskpart
exit
```

## Boot into Windows
> Make sure you are using a command window in platform tools for the next steps
> 
##### Reboot to fastboot
```cmd
adb reboot bootloader
```

##### Boot the UEFI
> Make sure the UEFI is placed in the platform-tools folder, otherwise specify the path to the image file
```cmd
fastboot boot xiaomi-raphael.img
```

Your device will now reboot and set up Windows. This will take some time. It will eventually reboot, when it does, reboot to fastboot and boot the UEFI again.

##### Setting up Windows
> You will have to run the limited setup because Wi-Fi does not work during boot.

To do this, open the accessibility menu and open the on-screen keyboard, then press SHIFT + F10 to open CMD where you will run
```cmd
oobe/bypassnro
```
Your device will now reboot, reboot back to Windows using fastboot one final time and finish setup. Make sure to press the "I don't have internet" button during setup.

After windows finishes booting, press the restart button to boot back to Android.

#### It is recommended to set up a dualboot method now.
> To do this, proceed to the [dualboot guide](dualboot-en.md)

## Finished!
