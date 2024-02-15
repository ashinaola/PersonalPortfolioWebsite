---
layout: post
type: posts
title: comparing containers and virtual machines
date: 2024-02-14
categories: [DevOps]
---
Containers and virtual machines (VMs) have been used to be able to configure and deploy applications in seperate environments which offer a level of consistency across different hardware components.  This allows for the same application to be deployed across a distributed environment and offer a consistent outcome which simplifies the process of deploying applications.  Both VMs and containers are now normally utilized in a lot of software developer jobs and it is one of the most mentioned buzz words.  Virtualbox is an example of software which can be used to interact with VMs, while Docker is one that is used to interact with containers.  Both can be used as an example to be able to compare the experience of these technologies and explore the limitations of both.

### a light introduction: virtual machines
Virtual machines have been utilized for a while, with the idea coming out of the need to run multiple operating systems on a singular host.  The main idea which drives virtual machines is virtualization.  Just like how virtual machines were used to run multiple operating systems on a single host, virtualization was used to divide resources offered on a mainframe.  In very broad terms, virtualization is the process of creating a virtual version of something such as a machine or memory.  The process is able to abstract the function of the physical object such as a storage device or a network resource.  Virtualization is used in different scenarios, but it is one of the main drivers behind cloud computing.  As previously mentioned, one way to take advantage of this is through the use of Virtualbox.

There are many types of virtualizations ranging from hardware virtualizations to storage virtualizations.  With Virtualbox, desktop environments can be initiated in order to be able interact with an isolated operating system (OS) environment.  As previously mentioned, the operating system which the VM is running on is called the host OS while the VM is the guest OS.  By abstracting the hardware components of the computer, the user is able to have an isolated environment.  In the case of hardware virtualization, the VM would attempt to duplicate the full experience of using the hardware that is available.  Desktop virtualization allows for users to seperate the desktop environment from the hardware component, which would mean users can interact with desktop environments that are set up on another computer.  

#### composition of an virtual machine

### a light introduction: containers

#### composition of an container

### use cases

#### limitations of virtual machines

#### limitations of containers

