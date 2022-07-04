---
title: "Docker"
permalink: "/docker"
layout: default
---


## Docker

### Introduction

Docker is a container tool which is increasingly used nowadays for developing and deploying software. It is an open-source platform that allows to build, ship and distribute software containers into an environment, reliably.  
\
Containerization is the process of creating an isolated environment without virtual hardware, except when the kernel of the host OS is different from the one of the containter.  
\
It is similar to OS-level virtualization, since the containers are created just above the OS kernel and share it through the Docker Engine. In case the docker container is used in Linux, the Linux OS acts as the default Docker Host. When it it used in another OS, like Windows, it relies on a lightweight virtual machine.  
\
A container is then a standard unit of software with all the code and dependencies packed, so that the application runs quickly and reliably in different environments, being agnostic to the OS or different machines.  
\
There is also the security aspect, the containers can share information between them, but only in a read-only fashion, however, every container shares the Kernel of the host, which may turn the system vulnerable if a security breach is found in the operating system, providing a way to the containers.

### Instalation

To install Docker, go to the [website](https://docs.docker.com/get-docker/) and follow the steps as provided for your scenario. Since I am using Debian from WSL, I will follow the instructions [installing from the repository](https://docs.docker.com/engine/install/debian/#install-using-the-repository).  
\
For that we do: `sudo apt-get update` followed by  
`sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release` and then add the GPG keys with `sudo mkdir -p /etc/apt/keyrings` and then ` curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg`. Finally, use `echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null` to set up the repository.  
  \
  Now we can install the Docker Engine using `sudo apt-get update` and `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin`.  
\
Verify that the Docker Engine is installed correctly by running `sudo docker run hello-world`. For some reason, docker does not start on debian on WSL2 so I followed [these](https://github.com/microsoft/WSL/discussions/4872#discussioncomment-99164) instructions to get it running. Now you can run the hello world docker image.  
\
Docker Compose can also be installed with `sudo apt-get install docker-compose-plugin` and then check if it was installed correctly with `docker compose version`.

### Creating and Removing Containers

To understand how Docker works, we will be running a lightweight image of Linux that requires just about 5 Mb of disk space. By executing the next command, a new instance of linux can be acessed: `docker run -it -d --name alpine_linux alpine`.  
The “run” command downloads the image from the Docker Hub (in case no
image exists in the local registry) and starts running a container. The "-it" flag gives an interactive TTY. This means that the output of the Docker container is piped into the shell and the input of the shell to the container. The "--name" flag names the container, and it's important for easy indentification and organization. The last parameter is the image that will be run as containter "-'alpine'".  
\
Use `docker images` to see the docker images downloaded.  
\
To check if the container is online: `docker ps -a` and to enter the container use: `docker exec -it alpine_linux sh`. Now the shell will open for the container and we can execute simple Linux commands. To exit the container just write `exit`.  
\
To remove a container there are 2 ways (a safe way):  
`docker stop alpine_linux`  and `docker rm alpine_linux`  
And an unsafe way:
`docker rm -f alpine_linux`
Since this is kinda of a test environment, the unsafe command can be used, since it's less time consuming and does not pose any harm.

### Container with volumes

There is an option when starting a container for creating one or more volumes. This makes possible to mount a folder from the host into the container, but there are some considerations to have:  
If the directory does not exist in host, the content and directories of the container will be created and copied there. Otherwise, the content and directories of the container will be overwritten. Afterwards, any change made by the container in that mount will be reflected on the host, and any changes made by host in those directories will be reflected in the container. This makes development easier since there is no need to enter the container to make changes.  
\
Use `docker run -it -d --name alpine_linux -v DIRECTORY_FULL_PATH:/test alpine` to run a container with a volume attached and then enter the container with `docker exec -it alpine_linux sh`. Now create a file inside the folder "test" named 1.txt and `exit` the container. If you go to the location we mounted the container, the file should be there.  

### Dockerfiles

A dockerfile is a set of instructions to make a Docker image. This is useful to create an image of a program to be run in different environments.  
For example, an image from a Debian based image with a web server (in this case, Apache) can be created without much effort, by just making a file named "Dockerfile" with the following content:

        FROM debian:stretch
        RUN apt-get update
        RUN apt install apache2 -y --no-install-recommends
        EXPOSE 80 
        CMD apachectl -D FOREGROUND
        
These commands pull a image of Debian from Docker Hub, update Debian repositories, and install Apache with no interactivity. After that,we expose the port 80 to allow HTTP connections and lastly the Apache Web Server is started.  
\
By using the `docker build . -t first:docker` command, we can create an automatic build that executes several commands in succession. The flag "-t" is used to name the image "first:docker".  
The image can now be run with `docker run -it -d -p 8081:80 --name apache first:docker`, where the "-p" flag indicates that any request on port 8081 from the local machine should be redirected to port 80 of the container (port mapping).  
\
Try accessing the webpage by typing ‘http://localhost:8081’ in a web browser.  
![Apache on ](https://user-images.githubusercontent.com/105322822/177061977-d0034c36-b2d1-47d4-bd86-dae7af88cba7.png)

### Docker-Compose

Docker-Compose allows to configure a file that runs several contains sequentially. Real-life scenarios usually require the launch of dozens of containers, so it would be harder to do it one by one.  
For this example, create a folder "site" where files will be stored, and outside the folder create a file named "docker-compose.yml". Docker-Compose will use this file, which has the following content:

        version: '3.0' 
        services: 
          php5:
            image: php:5.4.38-apache 
            ports: 
              - "8082:80" 
            network_mode: bridge
            volumes:
              - ./site:/var/www/html
          php7:
            image: php:7.3.5-apache-stretch
            ports:
              - "8083:80"
            network_mode: bridge
            volumes:
              - ./site:/var/www/html
              
Please note that this file **must** be indented with spaces and not tabs.  
\
The images used are provided from Docker Hub by PHP. Each one of these will redirect to the port 80 of the container, except that the local port is different.  
\
Inside the folder create a file named `index.php` with:

        <?php
          echo phpversion();
          echo "<p><p>";
          echo intdiv(10, 5);
        ?>
        
This will present one exclusive function of PHP7, which will serve to demonstrate the difference.  
\
To start the containers, execute: `docker compose up -d` (*warning* most forums I found are outdated and use `docker-compose`).  
The "-d" flag stands for detached (they will run in background). To see the results, you should access ‘http://localhost:8082’ and ‘http://localhost:8083’, respectively.  
\
To remove both containers simultaneously use: `docker compose down`

#### This page was written in 04/5/2022 and last updated in 04/07/2022.
