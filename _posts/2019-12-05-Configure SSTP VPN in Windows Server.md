---
layout: post
title: Configure an SSTP VPN
date:   2019-12-05 16:00
description: |
 How to configure an SSTP VPN on Windows Server 2016.
 > 1. Introduction
 > 2. Install the prerequisites
 > 3. Get a new certificate from let's encrypt
 > 4. Configure RRAS
 > 5. Configure a Windows 10 desktop
 > 6. Some commands to debug
tags: Windows
image: assets/images/2019-12-05-SSTP-VPN.jpg
---
## 1. Introduction

A good solution to access your corporate network while bypassing proxies or firewalls is to install a VPN SSTP. This one goes through port 443 which is the port of the HTTPS. So you can connect to it everywhere.
This post is the how to install it on a windows server 2012 R2 or 2016 (the tools are both the same). We use a free SSL certificate from let's encrypt for the link between client and server.

## 2. Install the prerequisites

Here, we need to install a new role on our distant windows server:
+ Remote access
    - Direct access and VPN (RAS)
    - Routing

When you select this components, IIS will automatically install itself.

To start, open the server manager, manage, add roles and feature.

<table class=".none"><tr><td markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-01.jpg' | relative_url }}){: .center-image }
1\. Select __*Active Directory Certificate Service*__ and __*Remote Access*__ and click __*Next*__...
</td><td markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-02.jpg' | relative_url }}){: .center-image }
2\. Check __*Certificate Authorithy*__ in __*AD CS Role Service*__. Click __*Next*__...
</td></tr></table>

You need to download the tool from let's encrypt to get new certificate.

![Install new server role]({{ 'assets/images/SSTP-VPN-03.jpg' | relative_url }}){: .center-image }

<p align="center" markdown="1">[Link to the let's encrypt tool on github](https://github.com/PKISharp/win-acme)</p>

Donwload the tool and unzip it in a folder of your choice.

## 3. Get a new certificate from let's encrypt

To get a new certificate from let's encrypt we use the command line with the wacs tool.

Open the cmd and type :

>Powershell (admin)
{:.filename}
{% highlight powershell %}

./wacs.exe --target manual --host pmlvpn.eastus.cloudapp.azure.com --certificatestore My

{% endhighlight %}

![Install new certificate]({{ 'assets/images/SSTP-VPN-04.jpg' | relative_url }}){: .center-image }

After that a new certificate will be installated in your personal certificate store.

## 4. Configure RRAS

Return to the server manager to start the maniulations.

<table><tr><td valign="bottom" markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-36.jpg' | relative_url }}){: .center-image }
1\. Open the RRAS configuration wizard...
</td><td valign="bottom" markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-37.jpg' | relative_url }}){: .center-image }
2\. Click __*Deploy VPN Only*__...
</td></tr><tr><td valign="bottom" markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-38.jpg' | relative_url }}){:width="400px"}
3\. Right click on your server name and Click __*Configure and Enable Routing...*__...
</td><td valign="bottom" markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-39.jpg' | relative_url }}){:width="400px"}
4\. Check __*Custom Configuration*__ and click __*Next*__...
</td></tr><tr><td valign="bottom" markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-40.jpg' | relative_url }}){:width="400px"}
5\. Check __*VPN Access*__ and optionnaly __*LAN Routing*__ to share internet connexion...
</td><td valign="bottom" markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-41.jpg' | relative_url }}){:width="400px"}
6\. Click __*Finish*__ and start the service...
</td></tr><tr><td valign="bottom" markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-42.jpg' | relative_url }}){:width="400px"}
7\. Right click on the server and select __*Properties*__...
</td><td valign="bottom" markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-43.jpg' | relative_url }}){:width="400px"}
8\. In __*Security*__ tab, select your certificate in __*Certificate*__...
</td></tr><tr><td valign="bottom" markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-44.jpg' | relative_url }}){:width="400px"}
9\. In __*IPV4*__ tab, check __*Static Address Pools*__ and add a new network...
</td><td valign="bottom" markdown="1">
![Install new server role]({{ 'assets/images/SSTP-VPN-45.jpg' | relative_url }}){:width="400px"}
10\. Click __*Apply*__ and click __*Yes*__ to restart the service...
</td></tr></table>

RRAS is now configurated.

## 5. Configure a Windows 10 desktop

* #### Authorize your user to access VPN on the server

Before the configuration of the windows client workstation , we have to autorize your user to connect to the VPN.

![Install new certificate]({{ 'assets/images/SSTP-VPN-05.jpg' | relative_url }}){: .center-image }

![Install new certificate]({{ 'assets/images/SSTP-VPN-06.jpg' | relative_url }}){: .center-image }

* #### Configure the client

![Configure VPN Client]({{ 'assets/images/SSTP-VPN-50.jpg' | relative_url }})

![Configure VPN Client]({{ 'assets/images/SSTP-VPN-51.jpg' | relative_url }})

![Configure VPN Client]({{ 'assets/images/SSTP-VPN-52.jpg' | relative_url }})


## 6. Some commands to debug

* #### Configure the server windows firewall

Just open the port 80 for the renew of the let's encrypt certificate and the port 443 for the VPN connexion.


* #### Check the SSL Certificate

To check the SSL certificate, we can use this commands :

>Powershell (admin)
{:.filename}
{% highlight powershell %}

netsh ras show sstp-ssl-cert
netsh http show sslcert

{% endhighlight %}

Source:
[https://github.com/PKISharp/win-acme](https://github.com/PKISharp/win-acme){:target="_blank"}
[https://dailysysadmin.com/KB/Article/1934/create-an-sstp-vpn-server-in-windows-server-2016/](https://dailysysadmin.com/KB/Article/1934/create-an-sstp-vpn-server-in-windows-server-2016/){:target="_blank"}
