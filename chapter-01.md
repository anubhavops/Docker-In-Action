# Chapter 01

> Docker isn’t a programming language, and it isn’t a framework for building software. Docker is a tool that helps solve common problems such as installing, removing, upgrading, distributing, trusting, and running software. It’s open source Linux software, which means that anyone can contribute to it and that it has benefited from a variety of perspectives. It’s common for companies to sponsor the development of open source projects. In this case, Docker Inc. is the primary sponsor. You can find out more about Docker Inc. at https://docker.com/company/.

> Docker is an open source project for building, shipping, and running programs. It is a command-line program, a background process, and a set of remote services that take a logistical approach to solving common software problems and simplifying your experience installing, running, publishing, and removing software. It accomplishes this by using an operating system technology called containers.

```
docker run dockerinaction/hello_world
```

![01fig01_alt](https://user-images.githubusercontent.com/95487264/179221451-feef57fc-c35e-4a95-82b1-9dc460aae4dd.jpg)


![image](https://user-images.githubusercontent.com/95487264/179221609-5df74d96-8950-489e-aff8-add0f6b8e6ef.png)



## Running software in containers for isolation 

Containers and isolation features have existed for decades. Docker uses Linux namespaces and cgroups, which have been part of Linux since 2007. Docker doesn’t provide the container technology, but it specifically makes it simpler to use. To understand what containers look like on a system, let’s first establish a baseline. Figure 1.3 shows a basic example running on a simplified computer system architecture.


![image](https://user-images.githubusercontent.com/95487264/179342638-38273b18-d596-4825-9ac6-c003981f9892.png)
 
Notice that the command-line interface, or CLI, runs in what is called user space memory, just like other programs that run on top of the operating system. Ideally, programs running in user space can’t modify kernel space memory. Broadly speaking, the operating system is the interface between all user programs and the hardware that the computer is running on.

You can see in figure 1.4 that running Docker means running two programs in user space. The first is the Docker engine. If installed properly, this process should always be running. The second is the Docker CLI. This is the Docker program that users interact with. If you want to start, stop, or install software, you’ll issue a command by using the Docker program.

![image](https://user-images.githubusercontent.com/95487264/179342658-9fde9222-c199-44b3-b0cd-040327bb8159.png)

Figure 1.4 also shows three running containers. Each is running as a child process of the Docker engine, wrapped with a container, and the delegate process is running in its own memory subspace of the user space. Programs running inside a container can access only their own memory and resources as scoped by the container.

Docker builds containers using 10 major system features. Part 1 of this book uses Docker commands to illustrate how these features can be modified to suit the needs of the contained software and to fit the environment where the container will run. The specific features are as follows:

- PID namespace— Process identifiers and capabilities
- UTS namespace— Host and domain name
- MNT namespace— Filesystem access and structure
- IPC namespace— Process communication over shared memory
- NET namespace— Network access and structure
- USR namespace— User names and identifiers
- chroot syscall—Controls the location of the filesystem root
- cgroups— Resource protection
- CAP drop— Operating system feature restrictions
- Security modules— Mandatory access controls
