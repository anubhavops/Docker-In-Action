# Chapter 01 WELCOME TO DOCKER

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

Docker uses those to build containers at runtime, but it uses another set of technologies to package and ship containers.

## Shipping containers

You can think of a Docker container as a physical shipping container. It’s a box where you store and run an application and all of its dependencies (excluding the running operating system kernel). Just as cranes, trucks, trains, and ships can easily work with shipping containers, so can Docker run, copy, and distribute containers with ease. Docker completes the traditional container metaphor by including a way to package and distribute software. The component that fills the shipping container role is called an image.

The example in section 1.1.1 used an image named dockerinaction/hello_world. That image contains single file: a small executable Linux program. More generally, a Docker image is a bundled snapshot of all the files that should be available to a program running inside a container. You can create as many containers from an image as you want. But when you do, containers that were started from the same image don’t share changes to their filesystem. When you distribute software with Docker, you distribute these images, and the receiving computers create containers from them. Images are the shippable units in the Docker ecosystem.

Docker provides a set of infrastructure components that simplify distributing Docker images. These components are registries and indexes. You can use publicly available infrastructure provided by Docker Inc., other hosting companies, or your own registries and indexes.

## Getting help with the Docker command line

Open a terminal, or command prompt, and run the following command:

```
docker help
```

Running docker help will display information about the basic syntax for using the docker command-line program as well as a complete list of commands for your version of the program. Give it a try and take a moment to admire all the neat things you can do.


## Summary 

This chapter has been a brief introduction to Docker and the problems it helps system administrators, developers, and other software users solve. In this chapter you learned that:

- Docker takes a logistical approach to solving common software problems and simplifies your experience with installing, running, publishing, and removing software. It’s a command-line program, an engine background process, and a set of remote services. It’s integrated with community tools provided by Docker Inc.
- The container abstraction is at the core of its logistical approach.
- Working with containers instead of software creates a consistent interface and enables the development of more sophisticated tools.
- Containers help keep your computers tidy because software inside containers can’t interact with anything outside those containers, and no shared dependencies can be formed.
- Because Docker is available and supported on Linux, macOS, and Windows, most software packaged in Docker images can be used on any computer.
- Docker doesn’t provide container technology; it hides the complexity of working directly with the container software and turns best practices into reasonable defaults.
- Docker works with the greater container ecosystem; that ecosystem is rich with tooling that solves new and higher-level problems.
- If you need help with a command, you can always consult the docker help subcommand.
