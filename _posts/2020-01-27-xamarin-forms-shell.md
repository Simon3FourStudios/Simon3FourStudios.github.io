---
layout: post
title: "Xamarin.Forms Shell: Getting Started"
date: 2020-01-27
author: Simon
image: /assets/img/2020/01/27/XFShell1024x683.png
image_thumb: /assets/img/2020/01/27/XFShell240x160.png
image_alt_text: An image of an Android and iOS app, built using Xamarin.Forms Shell
image_credits:  
tags: xamarin xamarin.forms shell
---

This is a quick guide to getting started with Xamarin.Forms Shell. I'll show you how to create an app using Xamarin.Forms Shell, add a Flyout menu with an image header and add a new page. I'm going to assume that you are already familiar with Xamarin.Forms and Visual Studio 2019 or Visual Studio for Mac.

Shell was added to Xamarin.Forms in v4.0 and was released in May 2019. From the [Release Notes](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/release-notes/4.0/4.0.0), Xamarin describes Shell as *"... a simplified way to express the structure and navigation for your application in a single file. No more dealing with different page types to handle setting up complicated navigation. It supports flyout menu, bottom tabs, top tabs, and an integrated search handler. A new URI based navigation routing system has been implemented in addition to the existing push/pop navigation service. Now you can route to any point in your application, no matter how deep, and handle navigation events to perform custom logic such as canceling the back action."*

The idea is that instead of using MasterDetailPage, TabbedPage or NavigationPage as the basis for your app, you can configure Shell to handle all of these different layout styles.

In addition to this, the pages within your app can be navigated-to using URIs, giving a route to every page in your app. This means that you could, for example, store the current page when the app shuts down and restore to that page at start up. This also allows you to provide deep links into a page in your app from a notification.

So let's get started.

Create a new project, using the Xamarin.Forms Shell template:

*VS 2019*

![An image showing the Create New Project dialog in Visual Studio 2019, with Mobile App (Xamarin.Forms) selected](/assets/img/2020/01/27/vs2019-proj-template.png)

![An image showing the Configure New Project dialog in Visual Studio 2019](/assets/img/2020/01/27/vs2019-proj-config.png)

![An image showing the Select a Template dialog in Visual Studio 2019, with Shell selected](/assets/img/2020/01/27/vs2019-proj-shell.png)


*VS for Mac*

![An image showing the Choose a Template page of the New Project dialog in Visual Studio for Mac, with Shell Forms App selected](/assets/img/2020/01/27/vsmac-proj-template.png)

![An image showing the first Configure page of the New Project dialog in Visual Studio for Mac](/assets/img/2020/01/27/vsmac-proj-shell.png)

![An image showing the second Configure page of the New Project dialog in Visual Studio for Mac](/assets/img/2020/01/27/vsmac-proj-config.png)

Build and run the app, to make sure that everything is working. This should give you a simple list view and an About page, with a Tab Bar at the bottom of the screen, allowing you to switch between the two pages.

![An animation showing the Android app switching between pages using the tab bar](/assets/img/2020/01/27/XFShellDemoAndroid1.gif)

![An animation showing the iOS app switching between pages using the tab bar](/assets/img/2020/01/27/XFShellDemoiOS1.gif)



We'll now add a flyout menu and use that to switch between pages.


In AppShell.xaml, find the &lt;TabBar&gt; section:

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

Replace &lt;TabBar&gt; with &lt;FlyoutItem&gt;, including the Title and FlyoutDisplayOptions properties:
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

Run the app and you should now see a hamburger menu which expands when tapped.

![An animation showing the Android app switching between pages using the flyout menu](/assets/img/2020/01/27/XFShellDemoAndroid2.gif)

![An animation showing the iOS app switching between pages using the flyout menu](/assets/img/2020/01/27/XFShellDemoiOS2.gif)

We'll also add a header to the flyout:

* Add a new 'Controls' folder under your Xamarin.Forms shared code project.
* Within this folder, add a new XAML ContentView called 'FlyoutHeader.xaml'.
* In 'AppShell.xaml', add a namespace for the new Controls namespace to the &lt;Shell&gt; tag:
{% highlight xml %}
{% raw %}
xmlns:controls="clr-namespace:XFShellDemo.Controls"
{% endraw %}
{% endhighlight %}
* Add the new Flyout Header control to the &lt;Shell.FlyoutHeader&gt; property, between &lt;Shell.Resources&gt; and &lt;FlyoutItem&gt;:
{% highlight xml %}
{% raw %}
<Shell.FlyoutHeader>
    <controls:FlyoutHeader />
</Shell.FlyoutHeader>
{% endraw %}
{% endhighlight %}

Run the app and you'll see the ContentView default text appearing at the top of the Flyout.

![An image showing the Android app with a header in the flyout menu](/assets/img/2020/01/27/vs2019-flyout-header1.png)

![An image showing the iOS app with a header in the flyout menu](/assets/img/2020/01/27/vsmac-flyout-header1.png)


As the FlyoutHeader is just a plain old ContentView, we can design it however we want. Let's replace the default text with an image:
* Add a png image to your iOS and Android projects.
- I used an image that was 404x350 pixels.
- Add the png to the project in the .Android/Resources/drawable folder.
- Add the png to the project in the .iOS/Resources folder.
* Open the FlyoutHeader.xaml file and replace the default &lt;StackLayout&gt; and &lt;Label&gt;:
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
* Within the &lt;ContentView&gt; tag, add the property:
{% highlight xml %}
{% raw %}
HeightRequest="200"
{% endraw %}
{% endhighlight %}


![An image showing the Android app with an image header in the flyout menu](/assets/img/2020/01/27/vs2019-flyout-header2.png)

![An image showing the iOS app with an image header in the flyout menu](/assets/img/2020/01/27/vsmac-flyout-header2.png)


We can simplify the view hierarchy of the &lt;FlyoutItem&gt;. As our &lt;Tab&gt; only contain a single &lt;ShellContent&gt;, we can remove the &lt;Tab&gt; and let the implicit conversion operators handle the &lt;ShellContent&gt;:
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
* Your MyPage class should look something like this:
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
* In MyPage.xaml, set the &lt;ContentPage&gt; Title property:
{% highlight xml %}
{% raw %}
Title="{Binding Title}"
{% endraw %}
{% endhighlight %}
* Add png icons (32x28 pixels) to the Android and iOS resource folders, like before. These will be used on the Flyout menu and TabBar.
* Finally, add the new menu item into the Flyout/TabBar, between 'Browse' and 'About':
{% highlight xml %}
{% raw %}
<ShellContent Title="My Page" Icon="tab_ThreeFourStudiosTriangles.png" ContentTemplate="{DataTemplate local:MyPage}" />
{% endraw %}
{% endhighlight %}

![An image showing the Android app with the new menu item in the flyout menu](/assets/img/2020/01/27/vs2019-new-page-flyout.png)
![An image showing the Android app with the newly added page](/assets/img/2020/01/27/vs2019-new-page.png)

![An image showing the iOS app with the new menu item in the flyout menu](/assets/img/2020/01/27/vsmac-new-page-flyout.png)
![An image showing the iOS app with the newly added page](/assets/img/2020/01/27/vsmac-new-page.png)

Finally, let's add some routing navigation. We'll save the current page in settings at shutdown and restore to that page at startup.

First, we need to name the routes within the shell. The &lt;FlyoutItem&gt;, &lt;Tab&gt; and &lt;ShellContent&gt; all have a Route property, so we'll name those in the AppShell.xaml:
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

Next, we'll use the Xamarin.Essentials Preferences to store the current page route when the app shuts down and to navigate to that page when the app restarts. You can find the current page route by using the Shell.Current.CurrentState.Location property. You can navigate to a page using Shell.Current.GoToAsync(). In App.xaml.cs:
{% highlight csharp %}
{% raw %}
.
.
.
using Xamarin.Essentials;
.
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

![An animation showing the Android app starting up with the About page active](/assets/img/2020/01/27/XFShellDemoAndroid3.gif)

![An animation showing the iOS app starting up with the About page active](/assets/img/2020/01/27/XFShellDemoiOS3.gif)

There's more to Shell than what I have covered here, including adding top tabs within a page and the ability to add search functionality to the top of a page.

See the official Microsoft documentation of Shell here:
[https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/shell/](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/shell/)

You can find the source code to this project on GitHub here:
[https://github.com/Simon3FourStudios/XFShellDemo](https://github.com/Simon3FourStudios/XFShellDemo)
