---
layout: post
type: posts
title: comparing containers and virtual machines
date: 2024-02-14
categories: [DevOps]
---
Containers and virtual machines (VMs) have been used to be able to configure and deploy applications in seperate environments which offer a level of consistency across different hardware components.  This allows for the same application to be deployed across a distributed environment and offer a consistent outcome which simplifies the process of deploying applications.  Both VMs and containers are now normally utilized in a lot of software developer jobs and it is one of the most mentioned buzz words.  Virtualbox is an example of software which can be used to interact with VMs, while Docker is one that is used to interact with containers.  Both can be used as an example to be able to compare the experience of these technologies and explore the limitations of both.

## a light introduction: virtual machines
Virtual machines have been utilized for a while, with the idea coming out of the need to run multiple operating systems on a singular host.  The main idea which drives virtual machines is virtualization.  Just like how virtual machines were used to run multiple operating systems on a single host, virtualization was used to divide resources offered on a mainframe.  In very broad terms, virtualization is the process of creating a virtual version of something such as a machine or memory.  The process is able to abstract the function of the physical object such as a storage device or a network resource.  Virtualization is used in different scenarios, but it is one of the main drivers behind cloud computing.  As previously mentioned, one way to take advantage of this is through the use of Virtualbox.

There are many types of virtualizations ranging from hardware virtualizations to storage virtualizations.  With Virtualbox, desktop environments can be initiated in order to be able interact with an isolated operating system (OS) environment.  As previously mentioned, the operating system which the VM is running on is called the host OS while the VM is the guest OS.  By abstracting the hardware components of the computer, the user is able to have an isolated environment.  In the case of hardware virtualization, the VM would attempt to duplicate the full experience of using the hardware that is available.  Desktop virtualization allows for users to seperate the desktop environment from the hardware component, which would mean users can interact with desktop environments that are set up on another computer.  

### types of virtual machines
Virtual machines are classified into two different categories and the two offer different experiences for the user, however they do offer the experience of virtualization.  One, the process VM, which offers something called a runtime environment which offers a seperate space within the host system that could allow for a process to run.  The other, the system VM, allows for users to interact with a guest OS.  Both are structurally and functionally different.

#### process virtual machines
An example of the process VM could be the Java Virtual Machine (JVM).  Process VMs offer an environment which allows for the application to execute in an environment.  In the example of JVM, the bytecode of the compiled Java program is executed in the JVM.  This feature is what allows for Java code to be able to be compiled in different platforms regardless of the underlying hardware.

One of the main features of process VMs is their ability to be stood up and destroyed after the process has finished execution.  The virtual machine ensures a level of separation which results in a level of consistency across different systems.  This is because the VM offers a seperate environment for the process to be able to run in.    

#### system virtual machines

## a light introduction: containers

### composition of an container

## use cases

### limitations of virtual machines

### limitations of containers

