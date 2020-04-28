---
layout: post
title: Install Jekyll on WSL
date:   2020-03-01 16:00
description: |
 Installation of Jekyll using WSL.
 > 1. Jekyll introduction
 > 2. Installation of ruby
 > 3. Installation of Jekyll
 > 4. Use Jekyll
tags: [Web Development, Jekyll]
image: assets/images/Jekyll-installation-on-WSL.jpg
---

## 1. Jekyll introduction

After a fresh installation of Windows, I needed to reinstall Jekyll in order to continue the development of my personal website. Jekyll is a popular framework written in ruby used to create a static pages website.

![Jekyll website]({{ 'assets/images/Jekyll-website.png' | relative_url }}){: .center-image }*Jekyll website*

## 2. Installation of ruby

The first thing to do is to install ruby and some tools to compile different plug-in of Jekyll.

>Bash
{:.filename}
{% highlight bash %}

sudo apt-get install ruby-full build-essential zlib1g-dev

{% endhighlight %}

## 3. Installation of Jekyll

Once is done, we can install Jekyll with the gem command. After we launch the compilation of different tools.

>Bash
{:.filename}
{% highlight bash %}

gem install bundler jekyll
bundle install

{% endhighlight %}

## 4. Use Jekyll

To use Jekyll, it's a good idea to install git, in order to work with github page which is free for hosting a static website.

![Jekyll is powered by github]({{ 'assets/images/jekyll-github.png' | relative_url }}){: .center-image }*Jekyll is powered by github*

>Bash
{:.filename}
{% highlight bash %}

sudo apt-get install git
git config --global user.name "Pierre Mesnil"
git config --global user.email pierre.mesnil@outlook.com

{% endhighlight %}

The command to use for create a new website :

>Bash
{:.filename}
{% highlight bash %}

jekyll new my-awesome-site
cd my my-awesome-site
git init

{% endhighlight %}

Finally, it's time to code !

![Jekyll server launch in WSL]({{ 'assets/images/wsl_jekyll_serve.png' | relative_url }}){: .center-image }*Jekyll server launch in WSL*

>Bash
{:.filename}
{% highlight bash %}

code .
bundle exec jekyll serve

{% endhighlight %}

Source:
[https://jekyllrb.com/](https://jekyllrb.com/){:target="_blank"}
