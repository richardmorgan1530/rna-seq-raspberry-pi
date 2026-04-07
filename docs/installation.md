# Installation Guide

This guide describes how to install and configure the software required
to run the **RNA-seq Analysis on Raspberry Pi** system on a **Raspberry Pi 5**
using **Raspberry Pi OS 64-bit Lite (headless)**.

The system uses:

-   Raspberry Pi OS Lite
-   Apache2 web server
-   JupyterLab
-   external USB SSD storage
-   bioinformatics tools for RNA-seq analysis

------------------------------------------------------------------------

# Hardware Platform

Tested configuration:

| Component | Specification |
|---|---|
| Single board computer | Raspberry Pi 5 |
| Operating system | Raspberry Pi OS Lite (64-bit) |
| System storage | microSD card (32 GB) |
| Data storage | External USB SSD (e.g. 1 TB) |
| Network | Ethernet or WiFi |

------------------------------------------------------------------------

# Install Raspberry Pi OS (Headless)

Download the latest version of **Raspberry Pi Imager** from:

https://www.raspberrypi.com/software/

Insert your microSD card and select:

**Raspberry Pi OS (Other) → Raspberry Pi OS Lite (64-bit)**

This version has **no desktop environment**, which reduces system
overhead and improves stability for server-based applications.

------------------------------------------------------------------------

# Configure Customisations

Before flashing the OS, apply OS customisation settings in Raspberry Pi Imager.

-   Set hostname e.g.: `raspberrypi`
-   Set username and password
-   Configure WiFi if required
-   Enable SSH (**Use password authentication** for first setup)
-   Do not enable Raspberry Pi Connect unless specifically required

Write the SD card and, when complete, insert it into the Raspberry Pi.

For simplicity, on first boot of a fresh installation, connect a monitor,
keyboard and mouse to the Raspberry Pi.

Boot the Raspberry Pi.

Login to the Raspberry Pi.

In future you can remove the monitor, keyboard and mouse and instead
connect via SSH using terminal apps such as PuTTY, Windows Terminal etc...

PuTTY: https://putty.org/index.html

Example from PuTTY Terminal using the hostname you previously set:

<p align="left">
  <img src="../images/PuTTY-login.png" width="421"><br>
  Click 'Open'
</p>

<p align="left">
  <img src="../images/PuTTY-login-security-alert.png" width="421"><br>
  Click 'Yes'
</p>

<p align="left">
  <img src="../images/PuTTY-login-username.png" width="421"><br>
  Input the username e.g. 'pi'
</p>

<p align="left">
  <img src="../images/PuTTY-login-password.png" width="421"><br>
  Input password
</p>

<p align="left">
  <img src="../images/PuTTY-login-success.png" width="421"><br>
  Login success!
</p>

------------------------------------------------------------------------

# Update the System

Once connected via SSH, update the OS:
```
sudo apt update
sudo apt upgrade -y
```

# Install Apache2 Web Server

Install Apache2:
```
sudo apt install apache2 -y
```
Verify the service is running:
```
sudo systemctl status apache2
```
Among the text you should see something similar to:
```
Active: active (running)
```
------------------------------------------------------------------------

# Test the Web Server

If you set your hostname to raspberrypi previously, then open a browser
on your local network and navigate to:
```
http://raspberrypi.local
```
Otherwise replace raspberrypi above with the hostname you chose.

Or alternatively if you know the IP address of your Raspberry Pi, for example:
```
http://192.168.1.50
```
You should see the default Apache page:
```
Apache2 Debian Default Page
```

------------------------------------------------------------------------

# Web Root Directory

The default web root is:
```
/var/www/html
```

Example file:
```
/var/www/html/index.html
```

For this project, the external USB SSD will later be mounted within the web-accessible directory structure.

