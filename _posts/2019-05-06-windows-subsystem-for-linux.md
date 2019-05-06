---
layout: post
title: "Windows Subsystem for Linux"
date: 2019-05-06
author: Simon
image: /assets/img/2019/03/05/ruby-logo1024×683.png
image_thumb: /assets/img/2019/03/05/ruby-logo160x160.png
image_alt_text: The logo of the Ruby computer language
image_credits: The Ruby logo is Copyright © 2006, Yukihiro Matsumoto
tags: linux windows ubuntu
---

The Windows Subsystem for Linux (WSL) provides a way of running Linux executables natively on Windows. It is available for 64-bit versions of Windows 10 and Windows Server 2019.

WSL was introduced in Windows 10 v1607 Anniversary Update in 2016, initially with only a Ubuntu image available to install. The v1709 Fall Creators Update made images available in the Microsoft Store and added SUSE as an install option. Currently, there are images available for popular Linux distributions, such as Ubuntu, SUSE, openSUSE, Debian, Fedora and Kali. In addition to these, a couple of other distributions are available, Alpine and Pengwin.

Pengwin, according to the Store and website, is based on Debian and built on work by Microsoft Research. It's a 'paid for' distribution, currently on sale at £8.95 instead of £15.95, and installs a number of developer tools by default.

WSL is not totally new tech. Windows NT had subsystem support from the start (1993), originally to support POSIX and OS/2.  The subsystems work by providing a binary compatible layer between the Windows kernel and the non-Windows application that is being run. The layer translates the calls between the two such that the application isn't aware that it's not running natively.

The Linux subsystem was originally created by MS to support Project Astoria, a technology to enable Android apps to run on Windows 10 Mobile. MS cancelled the project, apparently as it worked too well and was concerned that it would undermine its own UWP app platform.

In this example, I'm showing an install of the Ubuntu image. I would imagine that the other images work in a similar way.

First, enable WSL support in Windows. This can be done in two ways, either with Powershell or through the control panel.

Open PowerShell as Administrator and run:
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

Control Panel:
Open the Start menu and start typing 'Turn Windows features on or off'.
Once it appears, click on the icon to launch its control panel.
Scroll down to 'Windows Subsystem for Linux' and click it to enable, if it's not already.
Hit ok and the feature is installed, requiring a reboot to complete.

Once the system has rebooted, head to the MS Store to download your Linux image.

