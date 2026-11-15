# My Windows 11 install routine

2024 October
(last updated 2026 November)


## Introduction

This document details my personal procedure to set up a Windows 11 system. This is a work in progress. Everything in this document has been confirmed to work properly on my systems, with exceptions noted.


## With a fresh install, use a local account

The following comes from [an article on pureinfotech.com](https://pureinfotech.com/bypass-internet-connection-install-windows-11/). I have used this procedure and can comfirm that it works well.

1. On the “Oops, you’ve lost internet connection” or “Let’s connect you to a network” page, use the "Shift + F10" keyboard shortcut.

2. In Command Prompt, type the OOBE\BYPASSNRO command to bypass network requirements on Windows 11 and press Enter.

3. The computer will restart automatically, and the out-of-box experience (OOBE) will start again.

4. Quick note: You will need to select the region and keyboard settings again to get to the network connection page.

5. Click the “I don’t have internet” option.

6. Click the “Continue with limited setup” option.

7. Click the Accept button (if applicable).


## Install WinGet

WinGet is now included by default in Win 11 Home and Pro. Documentation and download is on [learn.microsoft.com](https://learn.microsoft.com/en-us/windows/package-manager/winget/)

Use a previously exported JSON list of apps to install everything.

```
winget export -o apps.json
winget import -i apps.json
```

Don't forget to install PowerShell 7

```winget install Microsoft.PowerShell```

Verify the install with ```$PSVersionTable.PSVersion```


## Install WSL

See [How to install Linux on Windows with WSL](https://learn.microsoft.com/en-us/windows/wsl/install) on Microsoft Learn. To install debian use an admin PowerShell: ```wsl --install -d debian```


## Move taskbar to left side of screen

1. Download [ExplorerPatcher](https://github.com/valinet/ExplorerPatcher) and run it.
2. Go to Settings and choose "Primary taskbar location on screen: left"
3. Then click "Restart File Explorer"


## Install Intel Arc Control

[Download from Intel's website](https://www.intel.com/content/www/us/en/products/docs/discrete-gpus/arc/software/arc-control.html)


## Optional: Install Phone Link

If you have an iPhone you can connect it to Windows 11 by using the Phone Link app. Learn how to install and set up the Phone Link app [here](https://www.microsoft.com/en-us/windows/sync-across-your-devices)


## Debloat stuff

I haven't been using debloat scripts or apps on Windows 11 other than [O & O Shutup 11](https://www.oo-software.com/en/shutup10), so that's the only debloater I can vouch for. Here are two others I've tried in the past and seem to work well:

* https://github.com/Raphire/Win11Debloat
* https://christitus.com/windows-tool/

Sometimes the debloat tools will have to be run again after a Windows update.


## Remove ads from File Explorer

In File Explorer, open the "Options" and select the "View" tab, and deselect "Show sync provider notifications"


## Settings that can speed up Windows 11


### Disable file indexing

Right-click on Local Disk (C:) drive in File Explorer -> Properties -> Uncheck "Allow files on this drive to have content indexed in addition to file properties"


### Services to disable

win+r then `services.msc`

* Connected User Experience and Telemetry
* Device Management Wireless Application Protocol (WAP) Push message Routing Service
* Program Compatibility Assistant Service
* Windows Biometric Service
* Windows Search
* Windows Error Reporting Service
* Diagnostic Policy Service

This list of services to disable is taken from [this video by Brett In Tech](https://www.youtube.com/watch?v=RMS4-05vQxY). Note it may be best to prefer "Manual" over "Disabled", as this requests the service not start unless requested, which saves resources without breaking dependencies. Don’t disable services you don’t understand, especially anything related to security, networking, Windows Update, or the Windows Defender family.

Another tool to view services:

win+r then `msconfig`

Although `msconfig` can be used to disable services, it's best used for troubleshooting -- it only does on/off with no Delayed or Manual option. It maintains a record of all services disabled and can easily restore to previous state.

