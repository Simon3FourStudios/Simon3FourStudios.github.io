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

In this post, I'll show you how to create an app using Xamarin.Forms Shell, add a Flyout menu with an image header and add a new page.
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



We'll now add a flyout menu and use that to switch between pages.

In AppShell.xaml, find the <TabBar>  section:
{% highlight xml %}
{% raw %}
<TabBar>
    <Tab Title="Browse" Icon="tab_feed.png">
        <ShellContent ContentTemplate="{DataTemplate local:ItemsPage}" />
    </Tab>
    <Tab Title="About" Icon="tab_about.png">
        <ShellContent ContentTemplate="{DataTemplate local:AboutPage}" />
    </Tab>
</TabBar>
{% endraw %}
{% endhighlight %}

Replace <TabBar> with <FlyoutItem>, including the properties:
{% highlight xml %}
{% raw %}
<FlyoutItem Title="XFShell Demo"
            FlyoutDisplayOptions="AsMultipleItems">
    <Tab Title="Browse" Icon="tab_feed.png">
        <ShellContent ContentTemplate="{DataTemplate local:ItemsPage}" />
    </Tab>
    <Tab Title="About" Icon="tab_about.png">
        <ShellContent ContentTemplate="{DataTemplate local:AboutPage}" />
    </Tab>
</FlyoutItem>
{% endraw %}
{% endhighlight %}

*Image of flyout with image*

We'll also add a header image to the flyout:

* Add a new 'Controls' folder under your Xamarin.Forms shared code project.
* Within this folder, add a new XAML ContentView called 'FlyoutHeader.xaml'.
* In 'AppShell.xaml', add a namespace for the new Controls namespace to the <Shell> tag:
{% highlight xml %}
{% raw %}
xmlns:controls="clr-namespace:XFShellDemo.Controls"
{% endraw %}
{% endhighlight %}
* Add the new Flyout Header control to the <Shell.FlyoutHeader> property, between <Shell.Resources> and <FlyoutItem>:
{% highlight xml %}
{% raw %}
<Shell.FlyoutHeader>
    <controls:FlyoutHeader />
</Shell.FlyoutHeader>
{% endraw %}
{% endhighlight %}

Run the app and you'll see the ContentView default text appearing at the top of the Flyout.

*Image of flyout with default text in header*

As the FlyoutHeader is just a plain old ContentView, we can design it however we want. Let's replace the default text with an image:
* Add a png image to your iOS and Android projects.
- I used an image that was 404x350 pixels.
- Add the png to the project in the .Android/Resources/drawable folder.
- Add the png to the project in the .iOS/Resources folder.
* Open the FlyoutHeader.xaml file and replace the default StackLayout and Label:
{% highlight xml %}
{% raw %}
<ContentView.Content>
    <Grid BackgroundColor="White">
        <Image Aspect="AspectFit"
                Source="the_name_of_your_png" />
    </Grid>
</ContentView.Content>
{% endraw %}
{% endhighlight %}
* Within the ContentView tag, add:
{% highlight xml %}
{% raw %}
HeightRequest="200"
{% endraw %}
{% endhighlight %}

*Image of flyout with header image*


We can simplify the view hierarchy of the <FlyoutItem>. As our <Tab> only contain a single <ShellContent>, we can remove the <Tab> and let the implicit conversion operators handle the <ShellContent>:
{% highlight xml %}
{% raw %}
<FlyoutItem Title="XFShell Demo"
            FlyoutDisplayOptions="AsMultipleItems">
    <ShellContent Title="Browse" Icon="tab_feed.png" ContentTemplate="{DataTemplate local:ItemsPage}" />
    <ShellContent Title="About" Icon="tab_about.png" ContentTemplate="{DataTemplate local:AboutPage}" />
</FlyoutItem>
{% endraw %}
{% endhighlight %}



Let's add a new page.
* Under the Views folder, add a new View derived from ContentPage, named MyPage.xaml.
* Under the ViewModels folder, add a new class named MyViewModel.cs.
* Edit MyViewModel.cs and derive the class from BaseViewModel, then add a constructor and set Title = "My Page":
{% highlight csharp %}
{% raw %}
class MyViewModel : BaseViewModel
{
    public MyViewModel()
    {
        Title = "My Page";
    }
}
{% endraw %}
{% endhighlight %}
* In MyPage.xaml.cs, add a 'using' to reference the ViewModels namespace, add a reference to MyViewModel and set the BindingContext and MyViewModel reference to a new MyViewModel object.
* Your MyPage class should look like this:
{% highlight csharp %}
{% raw %}
.
.
.
using XFShellDemo.ViewModels;
.
.
.
public partial class MyPage : ContentPage
{
    MyViewModel viewModel;
    
    public MyPage()
    {
        InitializeComponent();

        BindingContext = viewModel = new MyViewModel();
    }
}
{% endraw %}
{% endhighlight %}
* In MyPage.xaml, set the ContentPage Title parameter:
{% highlight xml %}
{% raw %}
Title="{Binding Title}"
{% endraw %}
{% endhighlight %}
* Add png icons to the Android and iOS resource folders, like before. These will be used on the Flyout and TabBar.
* Finally, add a new item into the Flyout/TabBar:
{% highlight xml %}
{% raw %}
<ShellContent Title="My Page" Icon="tab_ThreeFourStudiosTriangles.png" ContentTemplate="{DataTemplate local:MyPage}" />
{% endraw %}
{% endhighlight %}

*Images of flyout with new page item and new page itself*

Finally, let's add some routing navigation. We'll save the current page in settings at shutdown and restore to that page at startup.

First, we need to name the routes within the shell. The <FlyoutItem>, <Tab> and <ShellContent> all have a Route property, so we'll name those in the AppShell.xaml:
{% highlight xml %}
{% raw %}
<FlyoutItem Route="root" Title="XFShell Demo"
            FlyoutDisplayOptions="AsMultipleItems">
    <ShellContent Route="browse" Title="Browse" Icon="tab_feed.png" ContentTemplate="{DataTemplate local:ItemsPage}" />
    <ShellContent Route="my_page" Title="My Page" Icon="tab_ThreeFourStudiosTriangles.png" ContentTemplate="{DataTemplate local:MyPage}" />
    <ShellContent Route="about" Title="About" Icon="tab_about.png" ContentTemplate="{DataTemplate local:AboutPage}" />
</FlyoutItem>
{% endraw %}
{% endhighlight %}

Next, we'll use the Xamarin.Essentials Preferences to store the current route when the app shuts down and to navigate to that route when the app restarts. In App.xaml.cs:
{% highlight csharp %}
{% raw %}
.
.
using Xamarin.Essentials;
.
.
protected override void OnStart()
{
    var myRoute = Preferences.Get("my_route", "");

    if (myRoute != "")
    {
        Shell.Current.GoToAsync(myRoute);
    }
}

protected override void OnSleep()
{
    var myRoute = Shell.Current.CurrentState.Location.ToString();
    Preferences.Set("my_route", myRoute);
}
{% endraw %}
{% endhighlight %}

Now, when you restart the app, it will return to the page it was on when it was shutdown.

*Image of the app starting on the About page*