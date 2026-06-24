---
layout: single
date: 2026-06-25
categories:
classes: wide
keywords:
  - WSL
  - Docker
  - Ubuntu
  - Windows11
title: Installing Ubuntu, Docker and Portainer via WSL on WIndows 11 (Part Two)
---
So in the previous post we installed WSL2, installed Ubuntu, and installed Docker. Now it's time to get Portainer running. 

Here's our reference: [
[Install Portainer CE with Docker on Linux | Portainer Documentation](https://docs.portainer.io/start/install-ce/server/docker/linux)

So we now have two options.

1. Docker Run (The easy version which is fire and forget)
2. Docker Compose (Which will allow us to store the yaml in code control and keep a history and do loads of fun other things)

**We're going to do both. Easy one first.**

# **Easy one**

```bash
docker volume create portainer_data

jason@Desktop:/$ docker volume create portainer_data
portainer_data
```

Run the following command:

```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts

Unable to find image 'portainer/portainer-ce:lts' locally
lts: Pulling from portainer/portainer-ce
62f9236e8b75: Pull complete
f31c7ae835a2: Pull complete
bdb478fcea5e: Pull complete
1ffd82f0f9ca: Pull complete
4f4fb700ef54: Pull complete
359cf24061dd: Pull complete
8c18fb05a80b: Pull complete
078618dfa08e: Pull complete
ca2b53202e73: Download complete
64deb36925ab: Download complete
Digest: sha256:d27f76194b719bfe2a34779d51798a7adf02510cfba69ebcb538267f75aa4f47
Status: Downloaded newer image for portainer/portainer-ce:lts
aeeb0e1ae445a28f411f21f2099b375c679334d66516704559eaf6856f9362d9
```

Then validate it installed with:

```bash
docker ps

jason@Desktop:/$ docker ps
CONTAINER ID   IMAGE                        COMMAND        CREATED          STATUS          PORTS                                                                                                NAMES
aeeb0e1ae445   portainer/portainer-ce:lts   "/portainer"   18 seconds ago   Up 17 seconds   0.0.0.0:8000->8000/tcp, [::]:8000->8000/tcp, 0.0.0.0:9443->9443/tcp, [::]:9443->9443/tcp, 9000/tcp   portainer
```

Awesome. Done.

# The less easy one

We have the option of downloading a pre-defined docker compose file or by manually creating one - We're just going to create it here (For the content...).

All compose.yaml does is define a set of instructions for docker to follow when you build it, it's very picky regarding spacing and the details are important.

(Note: I tried doing this in VIM but then I couldn't figure out VIM.. So Nano it is...)

```bash
jason@Desktop:/$ sudo nano portainer-compose.yaml
```

```yaml
services:
  portainer:
    container_name: portainer
    image: portainer/portainer-ce:lts
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - portainer_data:/data
    ports:
      - 9443:9443

  volumes:
    portainer_data:
      name: portainer_data

  networks:
    defaults:
      name: portainer_network
```

Save it. (Also feel free to use a YAML validator.. )

Run the following:

```bash
docker compose -f portainer-compose.yaml up -d
```

Then you see this:

```
jason@Desktop:~# docker ps
CONTAINER ID   IMAGE                        COMMAND        CREATED         STATUS         PORTS                                                                                                NAMES
7963585688a9   portainer/portainer-ce:lts   "/portainer"   8 seconds ago   Up 8 seconds   0.0.0.0:8000->8000/tcp, [::]:8000->8000/tcp, 0.0.0.0:9443->9443/tcp, [::]:9443->9443/tcp, 9000/tcp   portainer
```

So, why do this? Simple: Github, Azure DevOps, Version Control, CI/CD pipelines. The lot.
# The interface (Both lead here..)

Now lets log in. Open a browser and go to the following url: https://localhost:9443/

(Note: The port can be changed to whatever you wish that's not in use, look at the 2nd -p switch in the docker run command.)



![](/assets/p1.png)

Create a 12 character password, hit create user and bob is most certainly your uncle.

![](/assets/p2.png)

So... Now we're installed, what does this mean? Well, we can now look at all containers running in our environment. Click the "Get Started" button and go from there:

![](/assets/p3.png)

Click into your local, the first and only one!) and now you can see, manage, tweak, generally break the following:

- Stacks (Below)
- Images
- Networks
- Containers
- Volumes

```
A stack is a collection of services, usually related to one application or usage. For example, a WordPress stack definition may include a web server container (such as nginx) and a database container (such as MySQL).
```
[Stacks | Portainer Documentation](https://docs.portainer.io/user/docker/stacks)

![](/assets/p4.png)

So that's that. 

WSL installed.
Ubuntu installed.
Docker installed.
Portainer installed.

What's next? Probably a continuation of this where we install MySQL and SonarQube (Or maybe containerise an existing app.. Who knows how I'll feel when I write the next one)