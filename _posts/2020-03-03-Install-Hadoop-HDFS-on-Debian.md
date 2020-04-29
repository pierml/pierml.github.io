---
layout: post
title: Install Hadoop on Debian 10
date:   2020-03-11 16:00
description: |
 Install Hadoop HDFS on Debian 10.
 > 1. Installation of Java
 > 2. Installation of Hadoop
 > 3. Create a group and an hadoop user
 > 4. Configure SSH passwordless
 > 5. Issue with Java 13
 > 6. Launch HDFS
tags: [Data Science, Hadoop]
image: assets/images/2020-11-03-Install-Apache-Hadoop-Debian.jpg
---

## 1.Installation of Java
In this post, I'm going to install hadoop in a single node on pseudo-distributed mode.

First, we need to install Java from the official Oracle Java 13 repository and after we add a variable JAVA_HOME required for Hadoop.

>Bash (root)
{:.filename}
{% highlight bash %}

apt install -y gnupg2 software-properties-common
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EA8CACC073C3DB2A
add-apt-repository ppa:linuxuprising/java
apt update
apt install -y oracle-java13-installer
echo 'JAVA_HOME=/usr/lib/jvm/java-13-oracle' >> /etc/environment
source /etc/environment
java --version

{% endhighlight %}

We have to accept the oracle license twice, one for adding the repository and another time when you install java.

![Oracle License]({{ 'assets/images/Oracle-license.png' | relative_url }}){: .center-image }*Oracle license*

If java --version return the version of Java, it's good !

![Java Version]({{ 'assets/images/Java-version.png' | relative_url }}){: .center-image }*Java version*

## 2.Installation of Hadoop

Let's go to the hadoop website to download the latest version of Haddop. Currently, it's the version 3.2.1

![Apache Hadoop Website]({{ 'assets/images/Apache-Hadoop.png' | relative_url }}){: .center-image }*Apache Hadoop Website*

Download the latest version with the wget command, untar it and add a HADOOP_HOME environnement variable.

>Bash (root)
{:.filename}
{% highlight bash %}

cd /opt
mkdir data
wget https://archive.apache.org/dist/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz
tar -xvzf /opt/hadoop-3.2.1.tar.gz
echo 'HADOOP_HOME=/opt/hadoop-3.2.1' >> /etc/environment
source /etc/environment
echo $HADOOP_HOME

{% endhighlight %}

Configure each configuration files of the different components of hadoop

## core-site.xml

>Bash (root)
{:.filename}
{% highlight bash %}

nano /opt/hadoop-3.2.1/etc/hadoop/core-site.xml

{% endhighlight %}

Set the ip of your machine.

>Xml configuration
{:.filename}
{% highlight xml %}

<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://0.0.0.0:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/opt/data/</value>
        <description>Where Hadoop will place all of its working files</description>
</property>
</configuration>

{% endhighlight %}

## hdfs-site.xml

>Bash (root)
{:.filename}
{% highlight bash %}

nano /opt/hadoop-3.2.1/etc/hadoop/hdfs-site.xml

{% endhighlight %}

We are on a local single machine so the replication need to be one.

>Xml configuration
{:.filename}
{% highlight xml %}

<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>

{% endhighlight %}

## mapred-site.xml

>Bash (root)
{:.filename}
{% highlight bash %}

nano /opt/hadoop-3.2.1/etc/hadoop/mapred-site.xml

{% endhighlight %}

Configure mapreduce to use Yarn.

>Xml configuration
{:.filename}
{% highlight xml %}

<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>

{% endhighlight %}

## yarn-site.xml

>Bash (root)
{:.filename}
{% highlight bash %}

nano /opt/hadoop-3.2.1/etc/hadoop/yarn-site.xml

{% endhighlight %}

>Xml configuration
{:.filename}
{% highlight xml %}

<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>

{% endhighlight %}


## 3.Create a group and an hadoop user

For security reason, we create a new user hadoop, autorize this user to use hadoop and we add hadoop directory to the path.

>Bash (root)
{:.filename}
{% highlight bash %}

/usr/sbin/adduser hadoop
chown -R hadoop /opt/hadoop-3.2.1
chown -R hadoop /opt/data

{% endhighlight %}

>Bash
{:.filename}
{% highlight bash %}

su hadoop
echo 'export PATH=$PATH:$HADOOP_HOME/bin' >> ~/.bashrc
echo 'export PATH=$PATH:$HADOOP_HOME/sbin' >> ~/.bashrc
source ~/.bashrc
hadoop version

{% endhighlight %}

## 4. Configure SSH passwordless

Hadoop need to use SSH passwordless. Configure it.

>Bash
{:.filename}
{% highlight bash %}

ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys

{% endhighlight %}

## 5. Issue with Java 13

There is an issue with the Java 13, thank to Stack overflow for the solution.
It seems a java library is missing.

>Bash
{:.filename}
{% highlight bash %}

cd /opt/hadoop-3.2.1/share/hadoop/yarn
wget https://repo1.maven.org/maven2/javax/activation/activation/1.1.1/activation-1.1.1.jar

{% endhighlight %}

## 6. Launch HDFS

First, format the namenode filesystem. The HDFS filesystem is creating in the /opt/data folder of our linux.
Finally, launch HDFS and Yarn.

>Bash
{:.filename}
{% highlight bash %}

hdfs namenode -format
start-dfs.sh
start-yarn.sh
jps

{% endhighlight %}

![Hadoop Java Daemon]({{ 'assets/images/hadoop-java-daemon.png' | relative_url }}){: .center-image }*Hadoop Java daemon*

Take care that all java daemons are started.

![Hadoop configuration website]({{ 'assets/images/hadoop-configuration-website.png' | relative_url }}){: .center-image }*Hadoop configuration website*

The configuration website of Hadoop is in port 9870. [http://localhost:9870/](http://localhost:9870/){:target="_blank"}

Source:
[https://hadoop.apache.org/](https://hadoop.apache.org/){:target="_blank"}
[https://stackoverflow.com/questions/48735869/error-failed-to-retrieve-data-from-webhdfs-v1-op-liststatus-server-error-wh](https://stackoverflow.com/questions/48735869/error-failed-to-retrieve-data-from-webhdfs-v1-op-liststatus-server-error-wh){:target="_blank"}
[https://www.oracle.com/java/technologies/javase-downloads.html](https://www.oracle.com/java/technologies/javase-downloads.html){:target="_blank"}
