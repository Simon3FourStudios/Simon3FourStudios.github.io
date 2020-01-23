---
layout: post
title: "Xamarin.Forms Shell: Getting Started"
date: 2020-01-23
author: Simon
image: /assets/img/2020/01/03/hot-reload1024x683.png
image_thumb: /assets/img/2020/01/03/hot-reload240x160.png
image_alt_text: An image of a flame emoji next to a reload emoji
image_credits:  
tags: xamarin.forms shell
---

This is a quick guide to getting started with Xamarin.Forms Shell. I'm going to assume that you are already familiar with Xamarin.Forms and Visual Studio 2019 or Visual Studio for Mac.

Shell was added to Xamarin.Forms in v4.0 and was released in May 2019. From the [Release Notes](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/release-notes/4.0/4.0.0), Xamarin describes Shell as *"... a simplified way to express the structure and navigation for your application in a single file. No more dealing with different page types to handle setting up complicated navigation. It supports flyout menu, bottom tabs, top tabs, and an integrated search handler. A new URI based navigation routing system has been implemented in addition to the existing push/pop navigation service. Now you can route to any point in your application, no matter how deep, and handle navigation events to perform custom logic such as canceling the back action."*

Which sounds good, as I'm all for simplification.

The idea is that instead of using MasterDetailPage, TabbedPage or NavigationPage as the basis for your app, you can configure Shell to handle all of these different layout styles.

In addition to this, the pages within your app can be navigated-to using URIs, giving a route to every page in your app. This means that you could, for example, store the current page when the app shuts down and restore to that page at start up. This also allows you to provide deep links into a page in your app from a notification.

So let's get started.

Create a new project, using the Xamarin.Forms Shell template:

*VS 2019*

*VS for Mac*

Build and run the app, to make sure that everything is working. This should give you a simple list view and an About page, with a Tab Bar at the bottom of the screen, allowing you to switch between the two pages.

*Animated GIF showing switching between 2 pages*



We'll now add a flyout menu and use that to switch between pages. We'll also add a header image to the flyout.

*Image of flyout with header image*



Simplify the view hierarchy



Add a new page



Show URI navigation, saving the current page in settings and restoring to that page at startup.