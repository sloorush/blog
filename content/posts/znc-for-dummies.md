+++
title = "How to set up a ZNC bouncer for dummies"
date = "2021-09-13T15:06:35+05:30"
author = "r-ush"
authorTwitter = "_r_ush_" #do not include @
cover = "img/znc.jpg"
tags = ["znc", "irc", "chat"]
keywords = ["znc", "irc", "linux"]
description = "A small direct tutorial to configure a ZNC bouncer to be connected to IRC 24x7"
showFullContent = false
draft = false
+++

> IRC, IRC, How old are you IRC? IRC was created by Jarkko Oikarinen in August 1988

## Introduction

ZNC is an IRC network bouncer software. ZNC comes with various modules and features that can cater to your usage requirements.

![ZNC](https://nixfaq.org/wp-content/uploads/2020/08/word-image-5.png)

We will be configuring ZNC with the web interface enabled here. In the web interface, you can create, edit, configure, and remove users from your ZNC instance.

## step1

get a system that runs 24/7

## step 2

install znc, for ubuntu, it should look something like this

```shell=
sudo apt-get install znc
```

## step 3

```shell=
znc --makeconf
```

## step 4

refer to the config shown in [this](https://www.youtube.com/watch?v=MRY6UyZuPNw) video by Justin for simplicity, you might want to modify some stuff based on your needs.

## step 5

- If you accidentally started ZNC at the end of the setup, you should kill it now with

```shell=
pkill znc
```

## step 6(optional, but good to have)

Now we'll set up systemd to supervise ZNC for us.

Create a file `/etc/systemd/system/znc.service` using

```shell=
touch /etc/systemd/system/znc.service
```

and open it with vim or nano or any text editor

```shell=
vim /etc/systemd/system/znc.service
```

with the contents:

```
[Unit]
Description=ZNC - IRC Bouncer
Requires=nss-user-lookup.target
After=network-online.target nss-user-lookup.target

[Service]
User=<YOUR_USER>
ExecStart=/usr/bin/znc --foreground
ExecReload=/bin/kill -HUP $MAINPID
Restart=on-failure
KillSignal=SIGINT
SuccessExitStatus=2

[Install]
WantedBy=multi-user.target
```

Make sure to change <YOUR_USER> to your username!

Reload systemd and start znc:

```shell=
sudo systemctl daemon-reload
sudo systemctl enable znc
sudo systemctl start znc
```

ZNC should now be running (and will start/restart automatically). You can see detailed information with

```shell=
sudo systemctl status znc.
```

## step 7

Now the basic setup for znc is done!

Your ZNC web interface should be available at: http://<droplet_ip>:<specified_port> or if you used SSL https://<droplet_ip>:<specified_port>, you can sign in with your user and password to configure ZNC further. More help on configuring ZNC further can be found over [here](https://wiki.znc.in/ZNC).

## step 8

If you can now access the web interface.

You can connect to your ZNC account via an IRC client of your choice by trying /server <droplet_ip> <specified_port> <user>:<pass> within your client, however this command is client dependent.

## References

- https://www.youtube.com/watch?v=MRY6UyZuPNw
- https://www.ocf.berkeley.edu/docs/staff/tips/staffvm/znc/
- https://dangerous.tech/znc-docker-a-containerized-irc-bouncer/
- https://psychogun.github.io/docs/linux/ZNC-bouncer/
- https://www.digitalocean.com/community/tutorials/how-to-install-znc-an-irc-bouncer-on-an-ubuntu-vps
