---
layout: post
title: "XAML Hot Reload for Xamarin.Forms: What's it all about?"
date: 2020-01-03
author: Simon
image: /assets/img/2020/01/03/hot-reload1024x683.png
image_thumb: /assets/img/2020/01/03/hot-reload240x160.png
image_alt_text: A flame emoji next to a reload emoji
image_credits:  
tags: xamarin.forms xaml
---

XAML Hot Reload is a technology available to a number of XAML supporting platforms, including WPF, UWP, Uno and Xamarin.Forms. It speeds up development time, by removing the need to rebuild the app every time the XAML UI code is changed.

XAML Hot Reload for Xamarin.Forms was first announced in July 2019 at the Xamarin Developers Summit and the first preview was made available the following August. It was finally made generally available in the v16.4 update to Visual Studio 2019, where it is now enabled by default. At the time of writing, XAML Hot Reload for Xamarin.Forms is available in Visual Studio for Mac v8.3.11, but is still in preview and is disabled by default.

To enable Hot Reload in VS for Mac or in versions of VS2019 prior to 16.4 on Windows, do the following:

**VS for Mac**

![The Preferences dialog in Visual Studio for Mac, showing the Xamarin Hot Reload page](/assets/img/2020/01/03/hot-reload-settings-mac.png)

*Open 'Preferences...' under the Visual Studio menu, then under the Projects section, select Xamarin Hot Reload. Here you will find a checkbox to Enable Xamarin Hot Reload.*

**Visual Studio 2019**

![The Options dialog in Visual Studio 2019 for Windows, showing the Hot Reload page](/assets/img/2020/01/03/hot-reload-settings-win.png)

*Open 'Options...' under the Tools menu, then under the Xamarin section, select Hot Reload. Here you will find a checkbox to Enable XAML Hot Reload for Xamarin.Forms.*

To use Hot Reload, just build and run your app as usual. Note that you will need to be using Xamarin.Forms v4.1 or later. Make changes to the XAML of the currently active page, hit save and watch the page update with your changes.

It has been designed to be resilient, so typing mistakes in the XAML won't cause the app to crash. It will work with MVVM, as long as the binding isn't changed. Code and resource changes are not reloaded and some view state might be lost, during the reload.

In summary, Hot Reload should prove to be be very useful during the UI design phase of any Xamarin.Forms app, by speeding up what can be a frustrating process of having to rebuild the app each time a change to the UI needs to be tested.