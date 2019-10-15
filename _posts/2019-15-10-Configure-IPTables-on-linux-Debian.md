---
layout: post
title: Configure iptables on Debian 9
date:   2019-10-15 17:30
description: |
 How to configure iptables on Linux Debian 9.
 > 1. Introduction
 > 2. To reload your config after a reboot
 > 3. Configure your rules
 > 4. Reload your configuration
tags: Debian iptables
image: assets\images\2019-15-10-Configure-IPTables-on-linux-Debian.jpg
---

## 1.Introduction

IPTables is the software on all linux distribution to configure your firewall.
You can check your IPV4 configuration with the command :

>Bash
{:.filename}
{% highlight bash %}

sudo iptables -L

{% endhighlight %}

![img]({{ 'assets/images/iptables00.png' | relative_url }}){: .center-image }*IPTables Rules*

In this situation we can see that all is permitted on this server.
For IPV6 the command is ip6tables.

## 2.How to reload your config after a reboot

If you want to keep your firewall configuration after a reboot you need to install iptables-persistent package otherwise your rules will be forgotten.

>Bash
{:.filename}
{% highlight bash %}

sudo apt-get install iptables-persistent

{% endhighlight %}

![img]({{ 'assets/images/iptables01.png' | relative_url }}){: .center-image }*Installation of iptables-persistent*

![img]({{ 'assets/images/iptables02.png' | relative_url }}){: .center-image }*Installation of iptables-persistent*

Answer yes for each question if you want to record your currently configuration.

## 3.Configure your own rules

>Bash
{:.filename}
{% highlight bash %}

vim /etc/iptables/rules.v4
vim /etc/iptables/rules.v6

{% endhighlight %}

## 4.Reload your configuration
