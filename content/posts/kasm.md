---
title: KASM on AWS
description: Using KASM
date: 2023-03-27
draft: false
---

KASM is a powerful virtual desktop which can allow you to create a virtual desktop. We can use it with AWS to allow multiple people to work on a virtual environment.

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
