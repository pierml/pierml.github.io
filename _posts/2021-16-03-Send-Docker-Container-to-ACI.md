---
layout: post
title: Send Docker to Azure Container Instance
date:   2021-03-16 12:00
description: |
 About the Python virtual environment
 > 1. Create a context to your Azure environment
 > 2. Start your containers with a Docker-Compose file
 > 3. Delete your Azure context
tags: [Azure,Docker]
image: assets/images/2021-16-03-Send-Docker-Container-to-ACI.jpg
---

## 1.Create a context to your Azure environment

You can execute directly on Azure your containers. The name of the service is Azure Container Instance and it have been created to execute short-lived containers. If you want to execute long-lived containers like an nginx or a database, the fare are very expensive (1€ by day by container) and I think it's better to use Azure Kubernetes Services or Cloud App service. 

On your local machine you have just to create a new context for your docker environment and connect it to your Azure account.

>Powershell
{:.filename}
{% highlight powershell %}
docker login azure
docker context create aci [my aci context] \
    --resource-group [your ressource group] \
    --location [your location]
docker context ls
docker context use [my aci context]
{% endhighlight %}

## 2.Start your containers with a Docker-Compose file

To start your containers the command is lightly different.
On your local environment you use the syntax "docker-compose up". For your Azure environment it's "docker compose up" 

>Powershell
{:.filename}
{% highlight powershell %}
docker compose up
docker ps
docker compose down
{% endhighlight %}

## 3.Delete your Azure context

You can delete your Azure context on your local machine with this command.

>Powershell
{:.filename}
{% highlight powershell %}
docker context rm [my aci context]
{% endhighlight %}

Source:
[https://docs.docker.com/cloud/aci-integration/](https://docs.docker.com/cloud/aci-integration/){:target="_blank"}
[https://docs.microsoft.com/fr-fr/azure/container-instances/tutorial-docker-compose](https://docs.microsoft.com/fr-fr/azure/container-instances/tutorial-docker-compose){:target="_blank"}