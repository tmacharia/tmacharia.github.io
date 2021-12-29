---
title: How to Install MongoDB on Docker
date: '2021-12-29 22:04:40'
layout: post
author: tmacharia
comments: true
tags:
- docker
- mongo
excerpt_separator: "<!--more-->"
image: assets/mongo-on-docker-blog-banner.jpg
---

![]({{ 'assets/mongo-on-docker-blog-banner.jpg' | relative_url }})
For fast & experimental use of MongoDB, running it on docker is a pretty effective way. After use, you can easily just delete the instance. Here's a procedure to setup a mongo instance on docker locally & test connection, & browse it.
<!--more-->
## Install steps

1. Find the latest version of MongoDB image on docker hub. Use this link [https://hub.docker.com/mongo](https://hub.docker.com/_/mongo) to go its default page.
2. Click on tags on the page and find the latest release tag matching your OS architecture e.g linux or windows. Once you find one, copy the docker command on the right of the release.
3. Open a terminal or prompt to pull/download the image. See example below.
    ```bash
    docker pull mongo
    ```
4. When pulling the image completes, you should be able to see it on your local docker dashboard under images.
5. Click run image, and an optional settings dialog will appear. Specify a container name and a localhost port for accessing the mongo instance; You can use the default & known MongoDB port `27017`. See the figure below.
![]({{ 'assets/run-mongo-image.png' | relative_url }})
6. If you now switch over to Containers/Apps, you will see the mongo docker container running.

## Test Connection & Usage

Now we need a client to test the docker instance and also for browsing & exploring the database.

The fastest & easiest tool by far is [MongoDB for VS Code](https://code.visualstudio.com/docs/azure/mongodb) extension.
![]({{ 'assets/mongo-vs-code-extension.png' | relative_url }})

1. Install the extension. You should see the mongo logo added to the bottom of the left sidenav of VS code.
2. Click on it, and a mongo panel will launch with a button for adding a connection. 
3. Click on "Add connection" and select open form, specify host & port as shown in the figure below to match our running docker container instance. Click connect and thats it.
![]({{ 'assets/connect-to-mongo-vs-code.png' | relative_url }})

Everything else from here is pretty straight forward & easy to follow, but in case you get stuck, refer to the link above for step-by-step procedures.
