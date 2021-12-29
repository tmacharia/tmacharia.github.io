---
title: How to Setup Docker on Windows 10
date: '2021-12-29 21:56:47'
layout: post
author: tmacharia
comments: true
tags:
- docker
---

## Prerequisites

1. Check that your machine matches the sytem requirements [https://docs.docker.com/desktop/windows/install/](https://docs.docker.com/desktop/windows/install/).
2. Confirm that Hyper-V is enabled under windows features.

## Install steps
-------------
1. Use this link for direct download of Docker Desktop Installer 
	   [https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe)
2. Double click the installer once downloaded.
3. Once installation completes, open start menu & launch Docker Desktop.
4. If starting the docker engine fails due to virtualizations issues, enable the following under windows features.
	- Virtual Machine Platform
	- Windows Subsystem for Linux
	- Hyper-V
	- Virtualization enabled in BIOS: Check if its enabled in Task Manager > Perfomance > CPU
		- If Task Manager says Virtualization is disabled yet you've enabled in BIOS, 
		  Open an administrative console prompt, and Run `bcdedit /set hypervisorlaunchtype auto` then Restart.

	For more elaborate instructions & further reading, check out [https://docs.docker.com/desktop/windows/troubleshoot/#virtualization](https://docs.docker.com/desktop/windows/troubleshoot/#virtualization)

## Further Configuration(InComplete)
----------------------------------
1. To change docker native images location on Windows 10, use the following links
	- [https://docs.docker.com/config/daemon/#docker-daemon-directory](https://docs.docker.com/config/daemon/#docker-daemon-directory)
	- [https://stackoverflow.com/a/69164422/3499361](https://stackoverflow.com/a/69164422/3499361)
