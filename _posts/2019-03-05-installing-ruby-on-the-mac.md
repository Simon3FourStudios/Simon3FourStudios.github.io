---
layout: post
title: "Installing Ruby on the Mac"
date: 2019-03-05
author: Simon
image: /assets/img/2019/03/05/ruby-logo1024×683.png
image_thumb: /assets/img/2019/03/05/ruby-logo160x160.png
image_alt_text: The logo of the Ruby computer language
image_credits: The Ruby logo is Copyright © 2006, Yukihiro Matsumoto
tags: general ruby website github
---


Building my website requires Ruby, Gems, Bundler and Jekyll. It took me a little while to work out how these 4 things fit together.

MacOS comes with a version of Ruby installed. Unfortunately, this version is quite old and is installed under the `/Library` folder, which is a protected system folder. This means that when installing Gems, those want to install under that folder too and the only way to do that is to do so using superuser privileges, using `sudo`.

If you follow the instructions on GitHub Pages for installing Jekyll, it will install it using the built in version of Ruby (assuming that you haven't already installed a different version).

After much searching around the web, I found a guide on [how to install Ruby for the Mac](https://usabilityetc.com/articles/ruby-on-mac-os-x-with-rvm/). This makes use of a package manager, Homebrew, and RVM, a version manager for Ruby.

Package managers are common in the Linux world, as a way of installing software and making sure that all of the dependant libraries are also installed. Most Mac apps come as complete packages, that are either installed via the App Store or as dmg files.

When dealing with apps installed through the Terminal, things get a little more complicated, and this is where the Mac becomes more similar to Linux, when installing software through the shell.

With Ruby, it is possible to have many versions installed at once. It's possible to build against any version installed, but the OS has a concept of a default version which it will use. RVM allows you to manage these different versions of Ruby and to select which version should be used as the default.

When I originally installed Jekyll, I was using the built-in MacOS version of Ruby, which, because it is installed under `/Library`, meant that I had to `sudo` install it, meaning that any updates or Gem installs also needed to be `sudo`ed. This eventually caused some issues, where I could no longer properly access the Gems properly and I could no longer build my website. This is what lead to my hunt for the best way to install Ruby, Gems, Bundler and Jekyll onto my Mac.

The guide in the above link works fine. I had an issue though, when it came to installing Jekyll. Because my previous install had used sudo, the Bundler cache folders were created with superuser privileges. These folders are located under the Home directory, in a hidden folder called '.bundle'. The dot hides the folder.

To remove the folder, I opened a Terminal window and from my Home folder, entered:
	`sudo rm -d -r .bundle`

This removes the folder and any subfolders within it. I then navigated back to my website repository folder and ran 'bundle install'. This time Jekyll installed without a problem and I was once again able to build my website.
