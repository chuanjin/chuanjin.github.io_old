---
title: Host <--> Docker
date: 2016-11-25 11:23:06
tags: [Tools, Docker]
categories: R&D
---

A recent project, we have to send TCP and UDP data from Host to Docker, back and forth. Docker is great and it is easy to expose port to provide service inside Docker instance. For example:


```
docker run -itd --name my_instance -p 1111:2222 -p 8888:9999/udp my_image

```

<!--more-->

Here we map the TCP port 1111 from host to 2222 inside docker instance, and UDP port 8888 on host to 9999 in docker, and some help commands we use frequently such as

```
docker exec -it my_instance /bin/bash
Or
docker attach my_instance # Go into docker instance

docker ps # Check runing instances

docker ps -a # Check all instances

docker start instance_name # Start a docker instance

docker stop instance_name # Stop a docker instance

docker rm instance_name # Remove a docker instance

docker images # List images

docker rmi image_name # Remove a docker image

docker build -t image_name . # Build a image from Dockerfile in current directory

docker save -o image_name.tar image_name # Save image to a tar archive

docker load -i image_name.tar # Load an image from a tar archive

docker run --rm -it -v $PWD:/my_code -w /my_code image_name bash # share current directory with /my_code inside the container and auto remove it after exiting

docker COMMAND --help # Helpful information

```

Now we come to the TCP/UDP communication testing. Basically the command netcat/nc is good enough for make data coming through.

```
# TCP
nc -l 1234
echo "hi" | nc localhost 1234

# UDP
nc -ul 1234
echo "hi" | nc -4u localhost 1234


```

Normally this two pairs work perfectly for most testing purpse, just be careful for the port forwarding of docker. However there is an issue for macOS, and there is a [workaround](https://docs.docker.com/docker-for-mac/networking/#/use-cases-and-workarounds) suggested by Docker offical sites. In short, use the command below to attach an unused IP to lo0 interface

```
sudo ifconfig lo0 alias 192.168.0.111/24

# In case you want to realse the attach
sudo ifconfig lo0 -alias 192.168.0.111

# Two more useful command for check ports listening when debugging
netstat -lna | grep udp
lsof -i4 -P -a -n

```

