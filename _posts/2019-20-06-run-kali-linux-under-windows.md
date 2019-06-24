---
layout: post
title: Run Kali Linux on Windows 10
date:   2019-06-20 18:00
description: |
 How to run Kali Linux on windows 10 using WSL.
 > 1. WSL Installation
 > 2. Install Kali linux with the Windows Store
 > 3. If you forgot your password
 > 4. GUI installation
 > 5. How to change your xrdp port
 > 6. Whitelist Kali in Windows Security
 > 7. Install kali tools
tags: Kali
image: assets/images/2019-20-06-run-kali-linux-under-windows.jpg
---

## 1.WSL Installation

To run linux application without a virtual machine, the best way is to install WSL. It is the acronym for Windows Subsystem for Linux.
This fonctionality of windows can run a linux shell natively under Windows and can launch the most of linux apps, like apt-get or vim.


To install WSL, it's relatively easy. Just copy paste this line in your powershell with the admin right :

>Powershell (admin)
{:.filename}
{% highlight powershell %}

Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

{% endhighlight %}

![img]({{ 'assets/images/powershell-wsl-command.jpg' | relative_url }}){: .center-image }*Installation of WSL in powershell*

After doing this you need to reboot your computer.

The currently version of WSL is 1.0 but Microsoft announce the version 2.0 with a better compatibility with the linux app for the end of the year.
The 2.0 version can run docker or nmap for example. It's not possible currently with 1.0 version.

## 2.Install Kali linux with the Windows Store

Just go to the windows store and search for kali linux.

![img]({{ 'assets/images/get-kali-windows-store.jpg' | relative_url }}){: .center-image }*Kali linux in the windows store*

Just click get and install it.

At the first launch, kali invite you to create a new user.

![img]({{ 'assets/images/kali-create-user.jpg' | relative_url }}){: .center-image }*First run in Kali linux*

You're now in Kali Linux !

## 3.If you forgot your password

If you forgot your password, you can run the kali bash with the user root without password. Just launch the powershell and change the default user as it :

>Powershell (admin)
{:.filename}
{% highlight cmd %}

kali config --default-user root

{% endhighlight %}

Launch Kali Linux and change the password for you user (p1erre for me)

>Bash
{:.filename}
{% highlight bash %}

passwd p1erre

{% endhighlight %}

Finally change the default user to p1erre.

>Powershell (admin)
{:.filename}
{% highlight cmd %}

kali config --default-user p1erre

{% endhighlight %}

## 4.GUI installation

Many tutos on the net doesn't work to accomplish this. This is the right way to install gui for kali Linux in WSL.
First, we need to update the source and the distribution. When you perform this, you can verify if your packets manager is configured to install the kali-rolling packages.

>Bash
{:.filename}
{% highlight bash %}

sudo apt-get update && sudo apt-get upgrade
sudo apt-get install xfce4
sudo apt-get install xrdp

{% endhighlight %}

During this installation you need to configure your keyboard.
After all of this is done, you have to launch the xrdp daemon and connect to it with the windows remote desktop app.

>Bash
{:.filename}
{% highlight bash %}

sudo /etc/init.d/xrdp start

{% endhighlight %}

![img]({{ 'assets/images/kali-linux-gui.jpg' | relative_url }}){: .center-image }*Kali linux GUI*

## 5.How to change your xrdp port

If your xrdp port is used yet, you can change it before launch the xrdp service.

>Bash
{:.filename}
{% highlight bash %}

sudo nano /etc/xrdp/xrdp.ini

{% endhighlight %}

Change the configuration line port to the desired port and restart the xrdp server.

>Bash
{:.filename}
{% highlight bash %}

sudo /etc/init.d/xrdp restart

{% endhighlight %}

## 6.Whitelist Kali in Windows Security

Some utils of Kali are considerated by windows defender as malwares or hacktools. You need to whitelist the directory in the windows defender config.
You need to find where this tools are installed.

C:\Users\ `_username_` \AppData\Local\Packages\ `_Kali*_`

![img]({{ 'assets/images/windows_security_exclusion.jpg' | relative_url }}){: .center-image }*Configure exclusion in windows security*

## 7.Install kali tools

>Bash
{:.filename}
{% highlight bash %}

apt-cache search kali-linux

{% endhighlight %}

Install the required metapackage do you want for your usage.

![img]({{ 'assets/images/kali_linux_metapackages.jpg' | relative_url }}){: .center-image }*List of Kali linux metapackages*
