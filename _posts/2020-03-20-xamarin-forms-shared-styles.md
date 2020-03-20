---
layout: post
title: "Xamarin.Forms: Sharing Styles across Light and Dark Themes"
date: 2020-01-27
author: Simon
image: /assets/img/2020/01/27/XFShell1024x683.png
image_thumb: /assets/img/2020/01/27/XFShell240x160.png
image_alt_text: An image of an Android and iOS app, built using Xamarin.Forms Shell
image_credits:  
tags: xamarin xamarin.forms themes styles dark light
---

With the latest releases of iOS and Android bringing OS support for Dark and Light modes, I set out to discover how to handle this within a Xamarin.Forms app. I found some great articles by both the Xamarin team and the community, explaining how to add themes to your app and switch between them and also how to detect which theme is active in your OS. Having read these articles, there was one aspect that I hadn't seen covered anywhere, so I thought I'd share my findings below.

A quick note, I won't be going into depth about how to fully implement themes in your app, as this has been covered elsewhere by others. I've added [links](#heading-links-section) to the web pages that I found useful at the bottom of this article.

{% comment %}
1. Overview of how themes are handled in XF, by switching between separate resource dictionaries, comparing against statically defined colors, etc.
2. Explain Styles and how this removes the need to define the same colours in every control that you use.
3. The styles can be added to each resource dictionary, but this creates duplication.
4. James Montemagno has a technique for merging together the app's original resource dictionary with the theme resources. Seems a bit clunky and also has some duplication.
5. Explain the merged dictionaries feature, using the themes dictionaries with a separate styles dictionary.
6. Seems to work! Let me know if there is something not right with this technique!
{% endcomment %}

## links section ##

[David Ortinau: Modernizing iOS Apps for Dark Mode with Xamarin](https://devblogs.microsoft.com/xamarin/modernizing-ios-apps-dark-mode-xamarin/)
[Brandon Minnick: Check for Dark Mode in Xamarin.Forms](https://codetraveler.io/2019/09/11/check-for-dark-mode-in-xamarin-forms/)
[James Montemagno: Hanselman.Forms](https://github.com/jamesmontemagno/Hanselman.Forms)
[Hussain Abbasi: How To Support Dark Mode In Xamarin.Forms](https://intelliabb.com/2019/11/02/how-to-support-dark-mode-in-xamarin-forms/)
