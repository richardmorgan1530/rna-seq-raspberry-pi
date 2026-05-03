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

Use Raspberry Pi Imager v2.0.7 or higher only, as lower versions have issues.

Insert your microSD card and select:

**Raspberry Pi OS (Other) → Raspberry Pi OS Lite (64-bit)**

This version has **no desktop environment**, which reduces system
overhead and improves stability for server-based applications.

------------------------------------------------------------------------

# Configure Customisations

Before flashing the OS, apply OS customisation settings in Raspberry Pi Imager.

-   Set hostname: `raspberrypi`
-   Set username: `pi`
-   Set password: choose a password
-   Configure WiFi
-   Enable SSH (**Use password authentication**)
-   Do not enable Raspberry Pi Connect unless specifically required

Write the SD card and when complete, insert it into the Raspberry Pi.

Power ON the Raspberry Pi.

------------------------------------------------------------------------

Connect via SSH using terminal apps such as PuTTY, Windows Terminal etc...

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
<p align="left">
  <img src="../images/Apache2-default.png" width="421">
  <br>
  Web Server success!
</p>
------------------------------------------------------------------------

# Install FileZilla

Install FileZilla on your Laptop/PC for easy file transfer to your Raspberry Pi

Download the latest version of **FileZilla** from:

https://filezilla-project.org/

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
The 'Apache2 Debian Default Page' in the screenshot above is the file located at /var/www/html/index.html

When you open http://raspberrypi.local in a browser, you are opening the file /var/www/html/index.html

This index.html page is visible to all PCs connected to the local area network, at the address http://raspberrypi.local

------------------------------------------------------------------------

# View Web Root Directory in FileZilla

Open FileZilla Software

Connect to the Raspberry Pi:
```
Host: raspberrypi.local
Username: pi
Password: your passowrd
Port: 22
```
Click on: Quickconnect

<p align="left">
  <img src="../images/FileZilla-login(2).png" width="800">
</p>

FileZilla above shows the Raspberry Pi root directory in the right hand side pane i.e. "Remote site"

To navigate to the /var/www/html folder, first click on the folder icon next to the forward slash '/' at the top of the folder tree

Scroll down to the bottom of the tree, to the folder named 'var' and double click to open it

Then 'www', then 'html' and you should see the index.html file i.e. 'Apache2 Debian Default Page'

<p align="left">
  <img src="../images/FileZilla-login(3).png" width="800">
</p>

------------------------------------------------------------------------

# Create a web-accessible directory to mount the USB SSD

Folder structure is /var/www/html/usb

Create the directory:
```
sudo mkdir -p /var/www/html/usb
```
Set permissions:
```
sudo chown -R pi:www-data /var/www/html
sudo chmod -R 775 /var/www/html
```
Click the refresh button in FileZilla to view this new usb folder

<p align="left">
  <img src="../images/FileZilla-login(4).png" width="800">
</p>

------------------------------------------------------------------------

# Mount USB SSD for Jupyter Lab and NCBI File Downloads:

This example uses a 1TB USB SSD (important) connected to the Raspberry Pi via externally powered USB hub.

For Raspberry Pi requirements, its best to format the USB SSD using ext4 formatting.

Raspberry Pi headless operating system is very minimal and therefore doesnt automatically mount any attached 
USB hard drives right out of the box, so you need to configure auto mount as follows:

Insert the USB SSD into the Raspberry Pi USB port and identify the USB SSD ID:

```
lsblk -o NAME,SIZE,FSTYPE,LABEL,UUID,MOUNTPOINT,MODEL
```
<p align="left">
  <img src="../images/mount-USB-SSD-ID.png" width="800">
</p>

In the example shown in the screenshot above you can see the UUID next to sda1

If your SSD is formatted as anything other than ext4 then partition and format as follows:

```
sudo parted -s /dev/sda mklabel gpt
sudo parted -s /dev/sda mkpart primary ext4 0% 100%
sudo mkfs.ext4 -F -L NCBI /dev/sda1
```
Check to ensure its correctly formatted to ext4:
```
lsblk -o NAME,SIZE,FSTYPE,LABEL,UUID,MOUNTPOINT,MODEL
```
Take note of the UUID and put the following line of code into the fstab file as follows

Update your Raspberry Pi fstab file so that the SSD automatically mounts when Raspberry Pi boots:
```
sudo nano /etc/fstab
```
Next mount the USB SSD to the location /var/www/html/usb

Add the following line of code:
```
UUID=YOUR_UUID_HERE  /var/www/html/usb  ext4  noatime,nofail,x-systemd.automount,x-systemd.device-timeout=10  0  2
```
see example below:
```
UUID=626d0262-7b39-4f72-b1fa-8ff172a5639b  /var/www/html/usb  ext4  noatime,nofail,x-systemd.automount,x-systemd.device-timeout=10  0  2
```
<p align="left">
  <img src="../images/mount-USB-SSD-fstab.png" width="800">
</p>

To exit press:
```
ctrl + x
```
Type y and Enter to save

------------------------------------------------------------------------

# Install Core Software

Install required packages:
```
sudo apt install python3 python3-pip python3-venv git default-jre fastqc wget unzip -y
```
You can see the USB SSD UUID next to sda1 in the example screenshot above.

------------------------------------------------------------------------

# Install SRA Toolkit (APT)

Install via package manager:
```
sudo apt install sra-toolkit -y
```
<p align="left">
  <img src="../images/sra-toolkit-install.png" width="800">
  <br>
  Click Enter to complete the install
</p>

Verify installation:
```
prefetch --version
fasterq-dump --version
```
------------------------------------------------------------------------

# Install Kallisto (APT)
```
sudo apt install kallisto -y
```
Verify: 
```
kallisto version
```
------------------------------------------------------------------------

# Install JupyterLab

Create the notebook directory, use the USB SSD as the working directory:
```
sudo mkdir -p /var/www/html/usb/jupyter
sudo chown -R pi:pi /var/www/html/usb/jupyter
```
This ensures:

- large FASTQ files are not stored on the SD card
- improved I/O performance
- reduced SD card wear
  
Create a dedicated venv (virtual environment) for JupyterLab (PEP 668 safe):
```
python3 -m venv /home/pi/jlab-venv
```
Upgrade pip + install JupyterLab:
```
/home/pi/jlab-venv/bin/pip install --upgrade pip
/home/pi/jlab-venv/bin/pip install jupyterlab ipykernel
```
(You will never need to manually “activate” this venv in daily use.)

------------------------------------------------------------------------

# Configure Apache reverse proxy for /usb/jupyter/

Enable Apache modules:
```
sudo a2enmod proxy proxy_http proxy_wstunnel rewrite headers
sudo systemctl restart apache2
```
Edit the Apache default site:
```
sudo nano /etc/apache2/sites-available/000-default.conf
```
Replace the current contents with the code below:
```
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        # --- Jupyter reverse proxy (STARTS HERE) ---
        ProxyRequests Off
        ProxyPreserveHost Off

        RewriteEngine On
        RewriteCond %{HTTP:Upgrade} =websocket [NC]
        RewriteRule /usb/jupyter/(.*)  ws://127.0.0.1:8888/usb/jupyter/$1  [P,L]

        ProxyPass        /usb/jupyter/ http://127.0.0.1:8888/usb/jupyter/
        ProxyPassReverse /usb/jupyter/ http://127.0.0.1:8888/usb/jupyter/

        <Directory /var/www/html/usb/jupyter>
                Options -Indexes
                Require all granted
        </Directory>
        # --- Jupyter reverse proxy (ENDS HERE) ---

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>
```
Reload Apache:
```
sudo systemctl reload apache2
```
------------------------------------------------------------------------
