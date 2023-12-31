<img align="right" src="https://raw.githubusercontent.com/graphiks/woa-raphael/65c0ee06045c13d1ef0f5f88aa687c50274ef7f5/raphael.png" width="350" alt="Windows 11 Running On A Redmi 9T Pro">


# Running Windows on the Redmi K20 Pro / Mi 9T Pro

## Optional post-install stuff
> All of these are optional, but enabling USB host mode is recommended otherwise non-powerered USB devices will not work.

### Enabling USB Host mode
> This makes USB work properly. If USB doesn't work, you may have to plug it in before boot.

##### Opening the command prompt as an administrator
> This is self explanatory, this opens the command prompt as administrator

- Go to the start menu
- Search command prompt
- Hold the command prompt application and run it as administrator
- Approve any UAC dialogs

##### Enabling USB host mode
> This edits the registry key to tell the USB Controller to put the device into host mode

- In the command prompt put ```reg add "HKLM\SYSTEM\CurrentControlSet\Enum\ACPI\QCOM0597\0\Device Parameters" /v RoleSwitchMode /t REG_DWORD /d 1```
- Reboot your phone

## Finished!




