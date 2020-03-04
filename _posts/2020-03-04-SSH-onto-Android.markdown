---
layout: post
title:  "Run Linux on Android and SSH onto Your Device"
date:   2020-03-04 21:25:00 +0100
categories: jekyll update
---
# What is Termux?

*It's not a full-fledged Linux distro, but certainly enough to have some fun with!*

![screenshot](screenshot.png)

With [Termux](https://play.google.com/store/apps/details?id=com.termux&hl=en) Linux environment, you can run bash shell on your Android phone without rooting it. It's great for cloning git repositories to your phone, writing simple automation scripts with Android functionalities, and more.

With the plug-in [Termux:Widget](https://play.google.com/store/apps/details?id=com.termux.widget), you also get a nifty box on the homescreen to run your favorite scripts with one click without having to open the app.

Also, [Termux:API](https://play.google.com/store/apps/details?id=com.termux.api&hl=en) lets you access Android sensors like the accelerometer or light sensor and control device functions like calling, the flashlight or vibration.

# Steps to SSH into the Termux Terminal

#### 1. Install Termux Linux Environment

- From Google Play Store, install [Termux](https://play.google.com/store/apps/details?id=com.termux&hl=en)

#### 2. Starting an SSH Server on Termux

- Open Termux app
- Set password for SSH access with the command `passwd`
  - Alternatively, use `ssh-keygen` to create a keyfile for more security
- Run `pkg install openssh`
- Run `sshd -d` to start an SSH server in debug mode
- To make this easier, you can create a shell script to do this and run it from [Termux:Widget](https://play.google.com/store/apps/details?id=com.termux.widget) on the home screen

#### 3. Access Termux from Computer via SSH

- From your computer, run `ssh -p 8022 <androids_ip_address>`
  - Look up ip address via Android settings -> about phone -> IP address
  - Alternatively from Windows, use [Putty](https://www.putty.org/) on port 8022
- Enter password configured in step 2
- You should now be connected!
- Note that [Termux:API](https://play.google.com/store/apps/details?id=com.termux.api&hl=en) functions do not work over sshd
  - This is due to permissions changes for background apps in Android 10 and is a real shame.

