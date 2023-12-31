<img align="right" <img align="right" src="https://raw.githubusercontent.com/graphiks/woa-raphael/65c0ee06045c13d1ef0f5f88aa687c50274ef7f5/raphael.png" width="350" alt="Windows 11 Running On A Redmi 9T Pro">


# Running Windows on the Redmi K20 Pro / Mi 9T Pro

## Reinstall guide
> This guide is used whenever you want to update or change your windows and / or driver installation.

### Prerequisites
- [TWRP](https://dl.twrp.me/raphael/twrp-3.7.0_9-0-raphael.img.html) (should already be installed)
- [DriverUpdater](https://github.com/WOA-Project/DriverUpdater/releases/tag/v1.9.0.0)
- [Drivers]() EDIT THIS
- [UEFI]() EDIT THIS

#### Reinstalling Windows
> If you have come here from the [troubleshooting page](troubleshooting-en.md) because you need to reinstall drivers, you can skip to "Reinstalling drivers" if you do not wish to re-apply the Windows image (which takes a long time)

```cmd
fastboot boot <twrp.img>
```

> If you already have TWRP installed, just hold the power and vol+ buttons at startup

> You will need to disable MTP in Mount
#### Execute script

```cmd
adb shell msc.sh
```

### Assign letters to disks

#### Start the Windows disk manager

> Once the X3 Pro is detected as a disk

```cmd
diskpart
```


### Assign `X` to Windows volume

#### Select the Windows volume of the phone
> Use `list volume` to find it, it's the one named "WINVAYU"

```diskpart
select volume <number>
```

#### Assign the letter X
```diskpart
assign letter=x
```

#### Exit diskpart
```diskpart
exit
```


### Check what type of panel you have

```cmd
adb shell cat /proc/cmdline
```
> Look for `msm_drm.dsi_display0` almost at the bottom

> If your device is `Tianma`, `msm_drm.dsi_display0` will be `dsi_j20s_36_02_0a_video_display`

> If your device is `Huaxing`, `msm_drm.dsi_display0` will be `dsi_j20s_42_02_0b_video_display`

### Install Drivers

> Replace `<vayudriversfolder>` with the actual location of the drivers folder
> Replace `<paneltype>` with the actual panel type (tianma/huaxing)

```cmd
.\driverupdater.exe -d <vayudriversfolder>\definitions\Desktop\ARM64\Internal\vayu_<paneltype>.txt -r <vayudriversfolder> -p X:
```


### Boot with Windows bootable UEFI image

```
fastboot flash boot <uefi.img>
```

## Finished!
