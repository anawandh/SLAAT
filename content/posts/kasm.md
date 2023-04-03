---
title: KASM on AWS
description: Using KASM
date: 2023-03-27
draft: false
---

KASM is a powerful virtual desktop which can allow you to create a virtual desktop. We can use it with AWS to allow multiple people to work on a virtual environment.

## What is KASM?
KASM allows you to be able to host a virtual desktop which users can use. This allows us to be able to work on virtual containers which have things like browsers and VS Code, without having them on our devices. KASM provides a Virtual Desktop Interface and can be deployed with a DevOps approach.
> Click here to go to the official [KASM site](https://www.kasmweb.com/).

## What are benefits of KASM?
KASM uses many familiar concepts and allow for a very powerful interface.
- Uses Docker: The Docker containers are streamed to the workspaces. We have built familiarity with Docker, and this also helps make the workspace efficient.
- Customizable: KASM has a vast library and has various tools in the Developer API which allow for a lot of customization in relation to the workspace.
- Desktop access: Allows a desktop to be accessed from any browser, which will allow us to be able to bridge the technological divide and hopefully not require your own computer for AP Computer Science Principles and Computer Science A. This will allow students to use school issued chromebooks to complete work.
- Security: KASM is a secure platform and has 2 factor authentication and prevents data loss. Additionally, it handles multiple security features, making for a robust platform to use.

## Setting Up KASM

1. You always want to have your EC2 Instance on AWS. Given the logins provided by the CSP teachers, you can set up an EC2 Instance. 
2. Make sure that Docker is installed
```
sudo install docker
```
3. Next, you will need to install KASM. The docker image needs to be downloaded and create a KASM container.
```
sudo docker pull kasmweb/core:latest
sudo docker run -p 443:443 -p 3389:3389 kasmweb/core:latest
```
