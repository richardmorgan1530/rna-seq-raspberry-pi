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

Example from PuTTY Terminal using the hostname you previously set:

<p align="center">
  <img src="images/PuTTY-login.png" width="602"><br>
</p>
