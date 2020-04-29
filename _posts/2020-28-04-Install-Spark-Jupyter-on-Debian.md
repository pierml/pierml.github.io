---
layout: post
title: Install Spark and Jupyter on Debian 10
date:   2020-04-28 16:00
description: |
 Install Apache Spark and Jupyter Notebooks on Debian 10.
 > 1. Installation of Apache Spark
 > 2. Installation of Jupyter Notebooks
 > 3. Launch PySpark
 > 4. Redirect ports for containers or virtual machines
tags: [Data Science, Spark]
image: assets/images/2020-04-28-Install-spark-jupyter-debian.jpg
---

## 1.Installation of Apache Spark

This is the second part for the installation of a local and a standalone data science platform with Apache Hadoop, Apache Spark and Jupyter Notebooks.
It is mandatory to do the primary part before this one.
For the previous part of installation it is [here](/2020/03/Install-Hadoop-HDFS-on-Debian/){:target="_blank"}

>Bash (root)
{:.filename}
{% highlight bash %}

cd /opt/
wget http://apache.crihan.fr/dist/spark/spark-3.0.0-preview2/spark-3.0.0-preview2-bin-hadoop3.2.tgz
tar xvf spark-3.0.0-preview2-bin-hadoop3.2.tgz
chown -R hadoop spark-3.0.0-preview2-bin-hadoop3.2
echo 'SPARK_HOME=/opt/spark-3.0.0-preview2-bin-hadoop3.2' >> /etc/environment
source /etc/environment

{% endhighlight %}

This script download Apache Spark, untar it and add an environment variable with the right path.
We installed Apache Hadoop 3, so we have to download Spark 3 version with the prebuild for our Hadoop.

![Download Apache Spark]({{ 'assets/images/download-apache-spark.png' | relative_url }}){: .center-image }*Download Apache Spark*

With the hadoop user, add spark binaries to your path.

>Bash (hadoop)
{:.filename}
{% highlight bash %}

su hadoop
echo 'export PATH=$PATH:$SPARK_HOME/bin' >> ~/.bashrc
echo 'export PATH=$PATH:$SPARK_HOME/sbin' >> ~/.bashrc
source ~/.bashrc

{% endhighlight %}

First start spark daemon.

>Bash (hadoop)
{:.filename}
{% highlight bash %}

start-master.sh
start-slave.sh spark://127.0.0.1:7077

{% endhighlight %}

Verify if all is working with these commands

>Bash (root)
{:.filename}
{% highlight bash %}

jps
ss -tunelp

{% endhighlight %}

Finally, start the spark shell.

>Bash (hadoop)
{:.filename}
{% highlight bash %}

spark-shell.sh

{% endhighlight %}

![Spark Shell]({{ 'assets/images/spark-shell.png' | relative_url }}){: .center-image }*Spark Shell*

## 2.Installation of Jupyter Notebooks

>Bash (root)
{:.filename}
{% highlight bash %}

update-alternatives --install /usr/bin/python python /usr/bin/python3.7 1
apt-get install python3-pip
pip3 install notebook

{% endhighlight %}

>Bash (hadoop)
{:.filename}
{% highlight bash %}

jupyter notebook --ip=127.0.0.1

{% endhighlight %}

![Jupyter Notebook]({{ 'assets/images/jupyter.png' | relative_url }}){: .center-image }*Jupyter Notebook*

## 3.Launch PySpark

In the previous part, we installed Python3 as the default python on our machine. So, we can launch PySpark now.

>Bash (hadoop)
{:.filename}
{% highlight bash %}

pyspark

{% endhighlight %}

![PySpark Shell]({{ 'assets/images/pyspark.png' | relative_url }}){: .center-image }*PySpark Shell*

## 4.Redirect ports for containers or virtual machines

Jupyter Notebooks : 8888
HDFS : 9870
Spark : 8580
yarn : 8088
hdfs ipc : 9000
