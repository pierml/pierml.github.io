---
layout: post
title: Python virtual environment
date:   2021-03-07 16:00
description: |
 About the Python virtual environment
 > 1. Introduction and requirements
 > 2. Create a virtual environment on your project
 > 3. Generate requirement.txt
 > 4. Install a new environment from a requirement.txt file
 > 5. Create and remove a virtual environment in Jupyter Notebooks
tags: [Python]
image: assets/images/2021-07-03-Python-Virtual-Environment.jpg
---

## 1.Introduction and requirements

Virtualenv is a tool to install in Python to create virtual environment. It's a good idea to create this at the beginning of a project because it permit to install python packages in another environment than your principal one. All new package are installed in the wanted directory and you can install just used packages by your program. You can reinstall easily your solution in another server or in a new container very fastly.

To create a new virtual environment, you need to install the virtualenv package from Pypi.

>Powershell
{:.filename}
{% highlight powershell %}
pip install virtualenv
{% endhighlight %}

## 2.Create a virtual environment on your project

When you start a new Python project, just create the new environment.

In this example, you create a new environment, activate it and install a new package.
The package pandas is installed in the .venv subdirectory and not in your general python installation.

>Powershell
{:.filename}
{% highlight powershell %}
python -m venv .venv
./.venv/Scripts/activate.ps1
pip install pandas
deactivate
{% endhighlight %}

You can delete the .venv directory and recreate one if you think you have installed wrong python packages in your program. You restart with a blank file.

## 3.Generate requirement.txt

You can easily generate a file to export all packages used by your solution. You'll can reinstall all this package in another computer.

>Powershell
{:.filename}
{% highlight powershell %}
pip freeze > requirements.txt
{% endhighlight %}

## 4.Install a new environment from a requirement.txt file

To recreate a virtual environment of a solution, you have just to type all this command in your favorite shell.

>Powershell
{:.filename}
{% highlight powershell %}
python -m venv .venv
./.venv/Scripts/activate.ps1
pip install -r requirements.txt
{% endhighlight %}

## 5.Create and remove a virtual environment in Jupyter Notebooks

To create a virtual environment in Jupyter Notebooks, the method is different.
This command create one and you can select it in the kernel menu of Jupyter Notebooks.

>Powershell
{:.filename}
{% highlight powershell %}
python -m venv .venv
./.venv/Scripts/activate.ps1
pip install jupyter
python -m ipykernel install --user --name=newEnvironment
{% endhighlight %}

You can delete a virtual environment with these commands too.
The first one list all the environment and the second one delete one of them.

>Powershell
{:.filename}
{% highlight powershell %}
jupyter kernelspec list
jupyter kernelspec uninstall newEnvironment
{% endhighlight %}