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


