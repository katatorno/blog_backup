---
title: ""Devgar" - the learning curve"
datePublished: Fri Mar 07 2025 11:28:51 GMT+0000 (Coordinated Universal Time)
cuid: cm7yp03wn000309l43gqpao5a
slug: devgar-the-learning-curve
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1741346316056/7dac7782-6b1f-4f51-b106-b4dbab529591.webp
tags: raspberry-pi, buildroot, yocto

---

Following ambition is not always the best strategy. Sometimes, the mountain you need to climb is simply too steep. I didn't realize what kind of technology I was trying to tackle alone, in a short time, with additional problems that I put on my own shoulders.

What did I want to do? I wanted to create a containerized environment with Yocto inside. I wanted to build an application for **Raspberry Pi** that would run **Home Automation** and to which I could connect **sensors** via some yet undefined protocol.

The simplest solution was to use a ready-made distribution — **Raspberry Pi OS**. However, it is not widely used in professional projects. I wanted to learn what appears most frequently in job offers and, at the same time, solve my engineering problem. So, I decided on **Yocto**.

The first few days I struggled with container-related problems, which, of course, I had created myself. Then, after verifying that everything worked without the container, I started focusing on the configuration and managed to create the first image to upload.

But here came another fundamental problem — I had never had the pleasure of playing with Raspberry Pi before. I know what UART is and how it works; I built an image that should contain a full console, connected the device to a USB adapter, inserted the card, and what happened? Nothing. Silence. What's going on? I have no clue!

![My new learning curve](https://cdn.hashnode.com/res/hashnode/image/upload/v1741346867583/b1c32a0c-8c93-4283-b915-94038b5da5a8.png align="center")

**A mountain must be conquered in stages!** I’ll start simple — I’ll install Raspberry Pi OS. I will check if the UART console is enough to play with this system. If so, I will install a Home Automation server, try to connect the first sensor, and link it to my system.

**What's next?** I guess it’s time for Buildroot. I will try to do exactly the same but by creating my own image. Only after completing these two stages will I start working with Yocto. I’ve lost a lot of time and energy, but I think I’ve already learned a lot. In the next post, I will try to describe my interactions with this operating system.