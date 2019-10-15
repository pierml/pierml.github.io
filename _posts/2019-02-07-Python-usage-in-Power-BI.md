---
layout: post
title: Python usage in Power BI
date:   2019-07-02 14:00
description: |
 The different usage of Python in Power BI desktop.
 > 1. Install Python and prerequisite
 > 2. Import data in PowerBI Desktop with Python
 > 3. Fonctionnality of pandas library for import
 > 4. Modify data in PowerBI Desktop with Python

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
pip install xlrd

{% endhighlight %}

Pandas is a library for data analysis and Matplotlib is for visualisation of graph.
Xlrd is not mandatory but it is important for import excel files with a python script.

![img]({{ 'assets/images/python-option_powerbi.jpg' | relative_url }}){: .center-image }*Python option in power BI Desktop*

You can choose your python environnement in the option. The default is perfect, but if you have multiple python envirnonnement like conda or other, you can choose here the one you want.
You can choose too, your python script file editor, let the defaut option it will choose the defaut editor for .py script.

## 2.Import data in PowerBI desktop with Python

Launch PowerBI and click Get data

![img]({{ 'assets/images/get-data-python-script.jpg' | relative_url }}){: .center-image }*Get data in power BI Desktop*

>Python
{:.filename}
{% highlight python %}

stock = pandas.read_excel("C:\\Users\\P1erre\\Desktop\\stock.xlsx")

{% endhighlight %}

This script can import an excel in powerquery. Note, it is important to double the backslash for accessing to the file.
PowerQuery detect automatically the pandas dataframe and name it with the variable name (stock in my example)

## 3.Fonctionnality of pandas library for import

With the pandas library you have a lot of connector. This is a quick list of what you can import :

![img]({{ 'assets/images/pandas-connectors.jpg' | relative_url }}){: .center-image }*Pandas connectors*

## 4.Modify data in PowerBI Desktop with Python

It is possible to modify a dataset from powerquery in Python. The variable named dataset is used to access it.

![img]({{ 'assets/images/run-python-script.jpg' | relative_url }}){: .center-image }*Run python script*

>Python
{:.filename}
{% highlight python %}

final = pandas.DataFrame(dataset.loc[:,'Date'])

{% endhighlight %}

This python script return only the date column of the dataset.
