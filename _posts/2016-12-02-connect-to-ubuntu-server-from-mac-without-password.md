---
layout: post
title: Connect to Ubuntu Server from Mac without password
date: 2016-12-02 15:20
author: bradleygmayne
comments: true
categories: [admin, certs, Linux, Linux, RSA, ssh, ubuntu]
---
I recently wiped my home server after running [OpenMediaVault](http://www.openmediavault.org/) for about 6 months. OMV is a turn key Debian based linux distro that functions like a NAS but has easy to install plugins for tons of open-source software. The plug-ins range from web servers to HTPC media applications. I liked the ease of use but I missed being able to jump in the command line and make quick changes and not have to worry about breaking apps and folder structure that was used by OMV. So I've gone back to Ubuntu Server because it was a quick install and it's a distro I have a lot of experience administrating.

In the interest of quick installation of my HTPC applications I used the [AtoMiC Toolkit](https://github.com/htpcBeginner/AtoMiC-ToolKit) script from the good folks at [htpcbeginner.com](http://www.htpcbeginner.com/).

So after a quick install and making the decision that I was going to keep my server local and just VPN into my home network to access my media remotely the next step was to setup SSH certs. SSH Certificates allow a user to connect to a secure remote session with another device, a server in this case, without the need of usernames or passwords. Even though I am keeping my network local this method is safe enough to use on a public facing server as well. The certificate you create will be a 2048 bit RSA cert and is commonly used throughout the internet. You can check out this sites write-up on the security of 2048 RSA versus 4096 - [So you're making an RSA key for HHTPS certificate, what key size do you use?](https://certsimple.com/blog/measuring-ssl-rsa-keys) The article makes the point that a 2048 RSA certificate creates 2^112 possibilities if trying to brute force crack the key. Enough background, on to the method.

First on your Mac you'll need to create your RSA key. When asked for a passphrase enter a password and write it down. You'll need this in a moment on your linux server.

```
sudo ssh-keygen -t rsa 2048
Enter file in which to save the key (/home/<strong>your_username</strong>/.ssh/id_rsa (Hit Enter)
Enter passphrase (empty for no passphrase)
Enter same passphrase again:
```

Now we need to retrieve the cert data from the id_rsa.pub file on your Mac. After entering the command in the terminal you'll most likely need to maximize the window so you can grab all of the info in the file. It will be one really long line. Hit **control-x** to exit nano.

```
sudo nano /Users/**your_username**/.ssh/id_rsa.pub
```

After copying the long line from your terminal you need to login to your linux server. SSH in or open a terminal window and type:


```
sudo nano /home/**your_username**/.ssh/authorized_keys
```

This will create a new file so there will not be any text here to replace. Now paste in the data from your Mac terminal file and make sure it is all in one long line. Hit **control+x** and then **y** to save the file. Head back over to your Mac terminal and ssh into your linux box. You should be asked for the passphrase you entered earlier.

Hope this helps someone out and makes your Admin work a little easier.

