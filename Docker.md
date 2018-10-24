# Docker quickstart

## Install Docker

Install docker engine inside your Ubuntu, follow [this manual](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

## Verify installation

To verify the installation run a hello-world container

```
$ sudo docker run hello-world
```

You should see something similar to:

```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
d1725b59e92d: Pull complete 
Digest: sha256:0add3ace90ecb4adbf7777e9aacf18357296e799f81cabc9fde470971e499788
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

## Start a MySQL container

The simplest way to start a MySQL server inside a docker container is

```
$ docker run --name=mysql -p 3306:3306 -d -e MYSQL_ROOT_PASSWORD=root mysql
```

This will create a container named mysql (```--name=mysql```) with root password "root" and map the container's 3306 port to localhost 3306 port.

Make sure it's running:

```
$ docker ps
```

should give you

```
CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
2565e2f526a9        mysql                          "docker-entrypoint.s…"   2 seconds ago       Up 1 second         0.0.0.0:3306->3306/tcp   mysql
```

Now you should be able to connect to the MySQL server using MySQL Workbench and pointing it to localhost:3306.
