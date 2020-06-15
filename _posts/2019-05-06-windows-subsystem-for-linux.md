---
layout: post
title: "Windows Subsystem for Linux"
date: 2019-05-06
author: Simon
image: /assets/img/2019/05/06/wsl800x450.png
image_thumb: /assets/img/2019/05/06/wsl284x160.png
image_alt_text: The Linux penguin next to the Windows 10 logo
image_credits:  
tags: linux windows ubuntu
---

The Windows Subsystem for Linux (WSL) provides a way of running Linux executables natively on Windows. It is available for 64-bit versions of Windows 10 and Windows Server 2019.

WSL was introduced in Windows 10 v1607 Anniversary Update in 2016, initially with only a Ubuntu image available to install. The v1709 Fall Creators Update made images available to download from the Microsoft Store and added SUSE as an install option. Currently, there are images available for popular Linux distributions, such as Ubuntu, SUSE, openSUSE, Debian, Fedora and Kali. In addition to these, a couple of other distributions are available, Alpine and Pengwin.

Pengwin, according to the Store and website, is based on Debian and built on work by Microsoft Research. It's a 'paid for' distribution, currently on sale at £8.95 instead of £15.95, and installs a number of developer tools by default.

WSL is not totally new tech. Windows NT had subsystem support from the start (1993), originally to support POSIX and OS/2.  The subsystems work by providing a binary compatible layer between the Windows kernel and the non-Windows application that is being run. The layer translates the calls between the two such that the application isn't aware that it's not running natively.

The Linux subsystem was originally created by MS to support Project Astoria, a technology to enable Android apps to run on Windows 10 Mobile. MS cancelled the project, apparently as it worked too well and was concerned that it would undermine its own UWP app platform.

In this example, I'm showing an install of the Ubuntu image. I would imagine that the other images work in a similar way.

First, enable WSL support in Windows. This can be done in two ways, either with PowerShell or through the control panel.

PowerShell:
Open PowerShell as Administrator and run
```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

Control Panel:

![The Windows Features control panel](/assets/img/2019/05/06/controlpanel.png)

Open the Start menu and start typing 'Turn Windows features on or off'.
Once it appears, click on the icon to launch its control panel.
Scroll down to 'Windows Subsystem for Linux' and click it to enable, if it's not already.
Hit ok and the feature is installed, requiring a reboot to complete.

Once the system has rebooted, head to the MS Store to download your Linux image.

![Ubuntu page in the Microsoft Store](/assets/img/2019/05/06/ubuntu1.png)

![Downloading Ubuntu from the Microsoft Store](/assets/img/2019/05/06/ubuntu2.png)

Launch and wait for the setup to complete.

![First launch of Ubuntu](/assets/img/2019/05/06/ubuntu3.png)

Enter your new username and password.

![Ubuntu setting user](/assets/img/2019/05/06/ubuntu4.png)

Welcome to Linux on Windows.

![Ubuntu installed](/assets/img/2019/05/06/ubuntu5.png)

###### What's lined up for WSL in the future? 
According to [this post](https://devblogs.microsoft.com/commandline/shipping-a-linux-kernel-with-windows/), an upcoming version of Windows 10 will ship with a full custom-built Linux kernel. This promises to improve the performance of Linux binaries running on WSL.
