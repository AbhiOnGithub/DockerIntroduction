# Introduction to Docker

Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers.
Containers are isolated from one another and bundle their own software, libraries and configuration files, they can communicate with each other through well-defined channels.
All containers are run by a single operating system kernel and therefore use fewer resources than virtual machines.

## Softwares to Download

Docker Desktop for Windows or Mac from <https://www.docker.com>
WSL2 in case of Windows only

## Lets start with running few commands

1. Find out the version of Docker in your Machine.

``` cmd/docker
docker –-version
```

In my machine I got following output

``` text
Docker version 19.03.12, build 48a66213fe
```

2. Running a "Helllo-World" container on Docker

``` cmd/docker
docker run hello-world
```

You will see something like this:
``` text
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete
Digest: sha256:4cf9c47f86df71d48364001ede3a4fcd85ae80ce02ebad74156906caff5378bc
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

3. Get list of Docker images present on your machine.
   
```cmd/docker
docker images
```
You should get following listing of Docker images or even with more images available
``` cmd/docker
REPOSITORY              TAG               IMAGE ID            CREATED             SIZE
hello-world            latest            bf756fb1ae65        8 months ago        13.3kB
```
4. Running a container 
Running of containers is managed with the Docker run command. To run a container in an interactive mode, first launch the Docker container.
``` cmd/docker
PS C:\Code> docker run -it centos /bin/bash

Unable to find image 'centos:latest' locally
latest: Pulling from library/centos
3c72a8ed6814: Pull complete
Digest: sha256:76d24f3ba3317fa945743bb3746fbaf3a0b752f10b10376960de01da70685fbd
Status: Downloaded newer image for centos:latest
[root@35312567e32f /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@35312567e32f /]# whoami
root
[root@35312567e32f /]# exit
exit
PS C:\Code>
```

5. Getting kist of all containers
here -a tells the docker ps command to list all of the containers on the system.

``` cmd/docker
PS C:\Code> docker ps -a
CONTAINER ID   IMAGE       COMMAND       CREATED              STATUS                  NAMES
35312567e32f   centos      "/bin/bash"   About a minute ago   Exited (0) 2 minutes    eager_neumann
4946e4d5d0e7   hello-world "/hello"      4 minutes ago        Exited (0) 4 minutes    cool_wing
```

6. Create our own Docker image using Google's GoLang Programming Language,run the following command inside the folder where dockerfile exists.

Directory structure
``` cmd
-HelloGoLang   (Directory)
    -dockerfile (Dockerfile) 
    -main.go    (GoLang program file)
```

``` cmd/docker
docker image build -t hello .

Sending build context to Docker daemon  3.584kB
Step 1/6 : FROM golang:1.15-alpine
 ---> b3bc898ad092
Step 2/6 : RUN mkdir /app
 ---> Running in 74d382908daa
Removing intermediate container 74d382908daa
 ---> a9b19afcb0cd
Step 3/6 : ADD . /app
 ---> 068f5dfc7625
Step 4/6 : WORKDIR /app
 ---> Running in 90bafd3d3fa5
Removing intermediate container 90bafd3d3fa5
 ---> e5e8111c6a2b
Step 5/6 : RUN go build -o main .
 ---> Running in 3ba47dbdb1e1
Removing intermediate container 3ba47dbdb1e1
 ---> b5446bc33dd4
Step 6/6 : CMD ["/app/main"]
 ---> Running in bf4143c74553
Removing intermediate container bf4143c74553
 ---> 602d87c8e6d2
Successfully built 602d87c8e6d2
Successfully tagged hello:latest
SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host. All files and directories added to build context will have '-rwxr-xr-x' permissions. It is recommended to double check and reset permissions for sensitive files and directories.
```

7. Again get list of Docker images present on your machine, you must see newly created hello image

```cmd/docker
docker images
```
You should get following listing of Docker images or even with more images available
``` cmd/docker
REPOSITORY              TAG               IMAGE ID            CREATED             SIZE
hello-world            latest            bf756fb1ae65        8 months ago        13.3kB
hello                  latest            602d87c8e6d2        5 minutes ago       302MB
```

1. Run the container using hello image just created by you

``` cmd/docker
docker run hello

hello world
```
