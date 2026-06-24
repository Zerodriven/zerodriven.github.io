---
layout: single
date: 2026-06-24
categories:
classes: wide
keywords:
  - WSL
  - Docker
  - Ubuntu
  - Windows11
title: Installing Ubuntu, Docker and Portainer via WSL on WIndows 11
---
Install WSL

Upgrade to WSL2

```powershell
wsl --set-default-version 2
```

Install Ubuntu

```bash
wsl --install -d Ubuntu
```

Go through the relevant prompts of setting up your root user, password, and disabling data collation

When you're at the terminal and everything stops moving, run the following commands to upgrade and update everything, you'll need to enter your sudo password.

```bash
sudo apt upgrade
```

Update everything

```bash
sudo apt update
```

Pro tip: Merge them

```bash
sudo apt update && sudo apt upgrade -y
```

Now we're onto following Docker's documentation: [Install Docker Engine on Ubuntu | Docker Docs](https://docs.docker.com/engine/install/ubuntu/)
Set up Dockers' APT repo:

```bash
sudo apt update
sudo apt install ca-certificates curl
```

You may get asked to do the following command at this point, do this after reading what it does.

```bash
sudo apt autoremove
```

Continue

```bash
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

**This is where I ran into an issue. THIS BIT IS REALLY IMPORTANT: DON'T DO THIS - IF YOU DO PLEASE READ A BIT FURTHER DOWN AS TO WHY IT BREAKS. THIS IS INTENTIONAL.**

Instead of the following

```bash
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
```

I did:

```bash
sudo nano /etc/apt/sources.list.d/docker.sources
```

I then **pasted** in the rest (There is something obviously wrong with doing this.. What could it be)

```
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
```

Then run 

```bash
sudo apt update
```

You will then see this problem:

```bash
Ign:47 https://download.docker.com/linux/ubuntu "${UBUNTU_CODENAME:-$VERSION_CODENAME}")/stable $(dpkg Packages
Ign:48 https://download.docker.com/linux/ubuntu "${UBUNTU_CODENAME:-$VERSION_CODENAME}")/stable --print-architecture) Packages
```

**This is caused because when you manually copy and pasted the config, the codename and version were not dynamically applied.**

To fix it:

```bash
sudo rm /etc/apt/sources.list.d/docker.sources
```

Enter the following command properly, then hit return, the run the update:

```bash
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
```

```bash
jason@Desktop:/etc/apt/sources.list.d$ sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: noble
Components: stable
Architectures: amd64
Signed-By: /etc/apt/keyrings/docker.asc
jason@Desktop:/etc/apt/sources.list.d$ sudo apt update
Hit:1 http://security.ubuntu.com/ubuntu noble-security InRelease
Hit:2 http://archive.ubuntu.com/ubuntu noble InRelease
Hit:3 http://archive.ubuntu.com/ubuntu noble-updates InRelease
Get:4 https://download.docker.com/linux/ubuntu noble InRelease [48.5 kB]
Hit:5 http://archive.ubuntu.com/ubuntu noble-backports InRelease
Get:6 https://download.docker.com/linux/ubuntu noble/stable amd64 Packages [58.1 kB]
Fetched 107 kB in 0s (353 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
All packages are up to date.
```

**Now we get to the fun bit of actually installing docker..**

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Then verify it's running:

```bash
 sudo systemctl status docker
 
  docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: enabled)
     Active: active (running) since Wed 2026-06-24 08:37:23 BST; 3s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 15964 (dockerd)
      Tasks: 17
     Memory: 33.9M (peak: 34.2M)
        CPU: 445ms
     CGroup: /system.slice/docker.service
             └─15964 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Jun 24 08:37:22 Desktop dockerd[15964]: time="2026-06-24T08:37:22.892439581+01:00" level=info msg="Restoring containers>
Jun 24 08:37:22 Desktop dockerd[15964]: time="2026-06-24T08:37:22.927623820+01:00" level=info msg="Deleting nftables IP>
Jun 24 08:37:22 Desktop dockerd[15964]: time="2026-06-24T08:37:22.951663889+01:00" level=info msg="Deleting nftables IP>
Jun 24 08:37:23 Desktop dockerd[15964]: time="2026-06-24T08:37:23.181241494+01:00" level=info msg="Loading containers: >
Jun 24 08:37:23 Desktop dockerd[15964]: time="2026-06-24T08:37:23.187944871+01:00" level=info msg="Docker daemon" commi>
Jun 24 08:37:23 Desktop dockerd[15964]: time="2026-06-24T08:37:23.188515510+01:00" level=info msg="Initializing buildki>
Jun 24 08:37:23 Desktop dockerd[15964]: time="2026-06-24T08:37:23.333221966+01:00" level=info msg="Completed buildkit i>
Jun 24 08:37:23 Desktop dockerd[15964]: time="2026-06-24T08:37:23.338641637+01:00" level=info msg="Daemon has completed>
Jun 24 08:37:23 Desktop dockerd[15964]: time="2026-06-24T08:37:23.338723408+01:00" level=info msg="API listen on /run/d>
Jun 24 08:37:23 Desktop systemd[1]: Started docker.service - Docker Application Container Engine.
```

Now run the hello-world image to make sure everything is running happily!

```bash
jason@Desktop:/etc/apt/sources.list.d$  sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete
d5e71e642bf5: Download complete
Digest: sha256:96498ffd522e70807ab6384a5c0485a79b9c7c08ca79ba08623edcad1054e62d
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

```

There you go. Ubuntu installed via WSL2 on Windows 11, with Docker running.

Next post will be getting portainer running!