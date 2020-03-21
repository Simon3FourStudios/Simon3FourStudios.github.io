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

*A quick note: I won't be going into depth about how to fully implement themes in your app, as this has been covered elsewhere by others. I've added [links](#heading-links-section) to the web pages that I found useful at the bottom of this article and also a link to my project on GitHub, where you can see this in action.*

###How do we use themes in Xamarin.Forms?
The way we use themes is that instead of hard-coding our colours and styles in the controls we use, we define them in a ResourceDictionary and reference those definitions in the controls.

For example, instead of this:

{% highlight xml %}
{% raw %}
<ContentPage
    BackgroundColor="White">

    <Label
        Text="Welcome to Xamarin.Forms!"
        TextColor="Black" />
</ContentPage>
{% endraw %}
{% endhighlight %}

we create a light theme ResourceDictionary:

{% highlight xml %}
{% raw %}
<ResourceDictionary>
    <Color x:Key="PrimaryColor">Black</Color>
    <Color x:Key="PageBackgroundColor">White</Color>
</ResourceDictionary>
{% endraw %}
{% endhighlight %}

and a dark theme ResourceDictionary:

{% highlight xml %}
{% raw %}
<ResourceDictionary>
    <Color x:Key="PrimaryColor">White</Color>
    <Color x:Key="PageBackgroundColor">Black</Color>
</ResourceDictionary>
{% endraw %}
{% endhighlight %}

and then reference these using the DynamicResource markup extension in our ContentPage:

{% highlight xml %}
{% raw %}
<ContentPage
    BackgroundColor="{DynamicResource PageBackgroundColor}">
    
    <Label
        Text="Welcome to Xamarin.Forms!"
        TextColor="{DynamicResource PrimaryColor}" />
</ContentPage>
{% endraw %}
{% endhighlight %}

This way, the ContentPage remains the same, but by changing which ResourceDictionary is in use, by setting **Application.Current.Resources**, we can change the colours across that page.

###Styles
In Xamarin.Forms, we use styles to apply the same set of visual properties (colours, font sizes, etc.) to all instances of a particular control type. For example, we might want all of our buttons to have a grey background and white text. This reduces the amount of duplication in our code and enables us to change those properties in one place, rather than having to find and change every instance of that control.

For example, instead of this:

{% highlight xml %}
{% raw %}
<Button
    Text="Button 1"
    TextColor="{DynamicResource PrimaryColor}"
    BackgroundColor="{DynamicResource ButtonColor}" />
<Button
    Text="Button 2"
    TextColor="{DynamicResource PrimaryColor}"
    BackgroundColor="{DynamicResource ButtonColor}" />
<Button
    Text="Button 3"
    TextColor="{DynamicResource PrimaryColor}"
    BackgroundColor="{DynamicResource ButtonColor}" />
{% endraw %}
{% endhighlight %}

we can do this:

{% highlight xml %}
{% raw %}
<Style
    TargetType="Button">
    
    <Setter Property="TextColor" Value="{DynamicResource PrimaryColor}" />
    <Setter Property="BackgroundColor" Value="{DynamicResource ButtonColor}" />
</Style>

<Button Text="Button 1" />
<Button Text="Button 2" />
<Button Text="Button 3" />
{% endraw %}
{% endhighlight %}

The styles need to be part of the ResourceDictionary, as they are applied globally across the application, but this then creates duplication across the themes, meaning that if we want to change a particular style, we will need to go into each theme and change it.

###How do we avoid duplicating the styles?

{% comment %}

{% highlight xml %}
{% raw %}
{% endraw %}
{% endhighlight %}

xx1. Overview of how themes are handled in XF, by switching between separate resource dictionaries, comparing against statically defined colors, etc.
xx2. Explain Styles and how this removes the need to define the same colours in every control that you use.
xx3. The styles can be added to each resource dictionary, but this creates duplication.
4. James Montemagno has a technique for merging together the app's original resource dictionary with the theme resources. Seems a bit clunky and also has some duplication.
5. Explain the merged dictionaries feature, using the themes dictionaries with a separate styles dictionary.
6. Seems to work! Let me know if there is something not right with this technique!
{% endcomment %}

## links section ##

[David Ortinau: Modernizing iOS Apps for Dark Mode with Xamarin](https://devblogs.microsoft.com/xamarin/modernizing-ios-apps-dark-mode-xamarin/)
[Brandon Minnick: Check for Dark Mode in Xamarin.Forms](https://codetraveler.io/2019/09/11/check-for-dark-mode-in-xamarin-forms/)
[James Montemagno: Hanselman.Forms](https://github.com/jamesmontemagno/Hanselman.Forms)
[Hussain Abbasi: How To Support Dark Mode In Xamarin.Forms](https://intelliabb.com/2019/11/02/how-to-support-dark-mode-in-xamarin-forms/)
