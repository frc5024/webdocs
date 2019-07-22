---
layout: default
title: "Developing on Linux"
parent: "Guides"
permalink: /docs/guides/linux
authors: ['ewpratten']
---

# Developing robot code on a Linux host
Despite the fact that the tools provided by Autodesk, National Instruments, and FIRST do not natively support Linux, it is possible (and easier) to work with robots when using a Linux-based OS.

As of the 2019-2020 offseason, 100% of the 5024 programming team is developing with linux. This guide will outline the best practices that we have learned throughout the 2019 season (the first season we allowed the use of linux).

## Writing code
If you are only looking to write, build, and deploy code, minimal effort is required. Follow our [Installing Development Tools]({{site.baseurl}}/docs/guides/installing-tools) guide.

## Organization
It is always recocommended to organize your code, but here are a few tips for linux:
 - Put all FRC-related GIT repos in `~/frc/`
   - NEVER use `~/frc<year>` to store your code. This directory is only for use by WPIlib.
 - Use [symlinks](https://www.nixtutor.com/freebsd/understanding-symbolic-links/) to map directories to external drives

## Git via SSH
Tired of being asked for your password when pushing to GIT, or want to use 2FA?

GIT over SSH is for you. The need for a password, or Oauth token is replaced by your SSH key.

To set up GIT to use SSH, you first must generate an SSH key.
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
ssh-add ~/.ssh/id_rsa
```
When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.

Next, print out your public key with:
```
cat ~/.ssh/id_rsa.pub
```
And copy it to your clipboard. Now, go to your [SSH and GPG Settings](https://github.com/settings/keys), and add your key.

To test that your key was correctly added, try SSHing into GitHub.com:
```
ssh -T git@github.com
```

You should get the following message:
```
You've successfully authenticated, but GitHub does not provide shell access.
```

You can now clone GIT repos via ssh. Make sure to click the **Use SSH** button when you see the **Clone or Download** menu on GitHub.com.

### Circumventing our shop's firewall to use GIT
Due to the fact that we *usually* use our school's student wifi network for development, we are restricted by the school board's firewalls. The firewall does it's job perfectly, but has an unfortunate restriction. Port 22 (The port required by GIT) is blocked by default.

We will not cover the use of VPNs, or other circumvention methods, because we do not support full circumvention of the network. On the other hand, we are unable to properly do our job with the firewall's port restrictions.

We have discovered that the only network traffic allowed through the firewall is TCP data on ports 443 and 80. Conveniently, GitHub listens to SSH connections on port 443 as a backup.

To use GIT, all we need to do is redirect SSH traffic for GitHub.com through port 443. This can be done by adding the following info to `~/.ssh/config`.
```
Host github.com
	hostname ssh.github.com
	port 443
```

That's it. GIT should now work.

## Fixing SSH issues with multiple robots
Due to the fact that we have 2-3 operational robots at any given time, we are required to deploy code to all of them.

Ocationally, an issue can occur were, SSH will stop working due to the fact that our robots do not share the same SSH keys.

If you get a big warning message when deploying code to our robots, add the following lines to your `~/.ssh/config` file.

```
Host 10.50.24.2
	StrictHostKeyChecking no

Host frcvision.local
    hostname frcvision.local
	StrictHostKeyChecking no
```

## Running DriverStation
DriverStation and the National Instruments' tool suite do not support Linux in any way. To solve this problem, we can use [VirtualBox](https://www.virtualbox.org/). 

### Qdriverstation
You may have heard of the [Qdriverstation](https://frc-utilities.github.io/) project before. This used to be the go-to solution for controlling robots from Linux, but is no longer actively developed.

If you are really wanting a native DriverStation, you can trick a robot into responding to Qdriverstation by doing the following:
 - Connect to a robot
 - Launch Qdriverstation
 - Set the year to 2016
 - Open the status panel
 - Wait for "Robot Link" to light up
 - Quickly click "Reboot RIO"
   - This will send control data to the robot, and cause it to partially connect
 - 50% of the time, this will allow you to connect to, and enable the robot

As you can see, this is not at all stable, so a virtual machine is needed.

### Choosing an OS
Unless your host has a large amount of allocatable resources, Windows 7 is going to be your best bet for speed and reliability. 

An installation ISO can be downloaded from the [Archive.org](https://archive.org/details/Windows7X64WithAllUpdates2018) website. With this ISO, set up a VM normally, and install windows.

### Configuring VirtualBox
Now, we need to configure VirtualBox to allow DriverStation to interact with the network. 

Go to your **Machine Settings**, then **Network**, then set the network type to **Bridged Adapter**. This will allow the VM to have raw access to your network card, and communicate with a robot.

### What to install
Now, follow the windows section of our [Installing Development Tools]({{site.baseurl}}/docs/guides/installing-tools) guide, then finally, our [Installing DriverStation]({{site.baseurl}}/docs/guides/ni-update) guide.

You how have everything you need for FRC development and testing configured and enabled. Have fun!