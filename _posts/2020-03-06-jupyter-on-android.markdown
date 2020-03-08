---
layout: post
title:  "Run a Jupyter Notebook Server on Android"
date:   2020-03-06 18:03:00 +0100
categories: jekyll update
tags: android
---
<!-- # View and Edit Jupyter files on Android -->

<img src="/assets/images/jupyter.png" alt="juypterLogo" width="60%">
<!-- ![jupyterLogo](/assets/images/jupyter.png) -->

# Why run a Jupyter notebook on your phone?
That's a very good question. Maybe you're in a hurry. Maybe you want to have a quick look at some files without taking out your laptop. Or maybe you're just bored in the bus on your way to work... 

#### Use Jupyter on Android via Termux
With the [Termux](https://termux.com/) app for Android you can install Python, [Jupyter](https://jupyter.org/) and a wide variety of Python packages from a Linux command line.

- Start off by installing Python with `pkg install python` to get Python 3.
- Then install Jupyter with `pip install jupyter`

The terminal will display a url on `localhost` with a port number and a key at the end of it. Copy this url into your browser, and voilá, Jupyter notebook!

  ![screenshot](/assets/images/jupyter_termux.png)

#### Note:
For a more extended tutorial on this subject, see this great article by [@leouieda](https://github.com/leouieda):
- [Running Jupyter and the Scipy stack on Android](https://www.leouieda.com/blog/scipy-on-android.html)

*The Jupyter logo was downloaded from the [Jupyter Design Github repository](https://github.com/jupyter/design)*
