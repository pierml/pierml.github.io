---
layout: post
title: Python usage in Power BI
date:   2019-07-02 14:00
description: |
 The different usage of Python in Power BI desktop.
 > 1. Install Python and prerequisite
 > 2. Import data in PowerBI Desktop with Python
 > 3. Fonctionnality of pandas library
 > 4. Modify data in PowerBI Desktop with Python
 > 5. Visualize data with Python
tags: Python PowerBI
image: assets/images/2019-02-07-python-usage-in-powerbi.jpg
---

## 1.Install Python and prerequisite

First, we need to install the Python runtime on our laptop.
Simply go to [https://www.python.org/downloads/](https://www.python.org/downloads/){:target="_blank"}, download the installation and run it.

![img]({{ 'assets/images/download-python.jpg' | relative_url }}){: .center-image }*Python website*

Before open PowerBi Desktop, you need to install some python package to execute script in it.

>Powershell (admin)
{:.filename}
{% highlight cmd %}

pip install pandas
pip install matplotlib

{% endhighlight %}

Pandas is a library for data analysis and Matplotlib is for visualisation of graph.

## 2.Import data in PowerBI desktop with Python

Launch PowerBI and click Get data

![img]({{ 'assets/images/get-data-python-script.jpg' | relative_url }}){: .center-image }*Get data in power BI Desktop*
