# Chapter 02 - Chapter 2. Running software in containers

This chapter covers

- Running interactive and daemon terminal programs in containers
- Basic Docker operations and commands
- Isolating programs from each other and injecting configuration
- Running multiple programs in a container
- Durable containers and the container life cycle
- Cleaning up

## 2.1. Controlling containers: Building a website monitor 

Suppose a new client walks into your office and makes an outrageous request for you to build them a new website: they want a website that’s closely monitored. This particular client wants to run their own operations, so they’ll want the solution you provide to email their team when the server is down. They’ve also heard about this popular web server software called NGINX and have specifically requested that you use it. Having read about the merits of working with Docker, you’ve decided to use it for this project. Figure 2.1 shows your planned architecture for the project.


![image](https://user-images.githubusercontent.com/95487264/179449193-6e45080b-21ef-43bc-b54a-7bdc16918c20.png)


This example uses three containers. The first will run NGINX; the second will run a program called a mailer. Both of these will run as detached containers. Detached means that the container will run in the background, without being attached to any input or output stream. A third program named watcher will run as a monitoring agent in an interactive container. Both the mailer and watcher agent are small scripts created for this example. In this section, you’ll learn how to do the following:

- Create detached and interactive containers
- List containers on your system
- View container logs
- Stop and restart containers
- Reattach a terminal to a container
- Detach from an attached container

## 2.1.1. Creating and starting a new container

Docker calls the collection of files and instructions needed to run a software program an image.

In this example, we’re going to download and install an image for NGINX from Docker Hub. Remember, Docker Hub is the public registry provided by Docker Inc. The NGINX image is what Docker Inc. calls a trusted repository. 

```
docker run --detach --name web nginx:latest
```
After Docker has installed and started running NGINX, one line of seemingly random characters will be written to the terminal. 

That blob of characters is the unique identifier of the container that was just created to run NGINX. Every time you run docker run and create a new container, that new container will get a unique identifier. 

After the identifier is displayed, it might not seem like anything has happened. That’s because you used the --detach option and started the program in the background. 
Running detached containers is a perfect fit for programs that sit quietly in the background. That type of program is called a daemon, or a service. A daemon generally interacts with other programs or humans over a network or some other communication channel. 



Another daemon that your client needs in this example is a mailer. A mailer waits for connections from a caller and then sends an email. The following command installs and run a mailer that will work for this example:

```
docker run -d  --name mailer  dockerinaction/ch2_mailer
```

This command uses the short form of the --detach flag to start a new container named mailer in the background. 

## 2.1.2. Running interactive containers

A terminal-based text editor is a great example of a program that requires an attached terminal. It takes input from the user via a keyboard (and maybe mouse) and displays output on the terminal. It is interactive over its input and output streams. Running interactive programs in Docker requires that you bind parts of your terminal to the input or output of a running container.

To get started working with interactive containers, run the following command:

```
docker run --interactive --tty --link web:web --name web_test busybox:1.29 /bin/sh

```
**Creates a virtual terminal and binds stdin** 

The command uses two flags on the run command: --interactive (or -i) and --tty (or -t). First, the --interactive option tells Docker to keep the standard input stream (stdin) open for the container even if no terminal is attached. Second, the --tty option tells Docker to allocate a virtual terminal for the container, which will allow you to pass signals to the container. This is usually what you want from an interactive command-line program. You’ll usually use both of these when you’re running an interactive program such as a shell in an interactive container.

The command in the interactive container example creates a container, starts a UNIX shell, and is linked to the container that’s running NGINX. From this shell, you can run a command to verify that your web server is running correctly:

```
wget -O - http://web:80/
```

It’s possible to create an interactive container, manually start a process inside that container, and then detach your terminal. You can do so by holding down the Ctrl (or Control) key and pressing P and then Q. This will work only when you’ve used the --tty option.

To finish the work for your client, you need to start an agent. This is a monitoring agent that will test the web server as you did in the preceding example and send a message with the mailer if the web server stops. This command will start the agent in an interactive container by using the short-form flags:

```
docker run -it  --name agent  --link web:insideweb --link mailer:insidemailer dockerinaction/ch2_agent 
```

**Creates a virtual terminal and binds stdin**

When running, the container will test the web container every second and print a message like the following:

```
System up.
```
