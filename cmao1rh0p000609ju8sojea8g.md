---
title: "Dedicated Linux for Raspberry - how easy it is!"
datePublished: Wed May 14 2025 14:39:43 GMT+0000 (Coordinated Universal Time)
cuid: cmao1rh0p000609ju8sojea8g
slug: dedicated-linux-for-raspberry-how-easy-it-is
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1747233542716/22964820-5f99-4987-a881-70654dc93b20.jpeg
tags: raspberry-pi

---

I managed to gather all the components to start my fun with embedded Linux. It wasn't much, and most of the components can be bought in any store - completely different than with classic embedded systems. Let me present you my "impressive" development-testing-educational kit

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747233176013/8e118658-8287-4af1-8968-e42caa3589ec.jpeg align="center")

My setup consists of a Raspberry Pi 4 Model B with 1 GB of RAM, a cute, mini, used 7-inch monitor, a classic HDMI cable with a micro HDMI adapter, and a standard USB-C charger.

After connecting everything, a screen appears informing me about the type of board, boot method, missing SD card, network interface information, and HDMI output connection. The board doesn't have the operating system that should be on the missing memory card. But other than that – everything works!

Let's go ahead and flash the dedicated operating system onto this device, which is Raspberry Pi OS. The easiest way will be to download the Raspberry Imager program – it prepares the SD card with the system. The program is very intuitive! I choose the board version, the system I want to install, and the storage device where I want to write the operating system – the SD card that will be inserted into the Raspberry. This is how it looks for me:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747233305098/978aeb7a-ae0a-409d-83b9-bdd43b5849f9.png align="center")

After confirming that I’m aware of the data removal from the card and accepting the use of personalized data, such as the Wi-Fi password for the system, everything happens automatically, and it looks like it's working! Now I'll insert the card into the Raspberry, plug in the mouse and keyboard, and see how it all works!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747233271653/88af8274-78ef-4b5d-bbb6-ad14ca2b130b.jpeg align="center")

After a few resets and obvious issues with setting up the display, the system booted up correctly!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747233395006/e77e93f3-63d8-4e03-8d08-c2482a60d34b.jpeg align="center")

After the Raspberry Pi has booted up correctly, you need to go through the standard configuration – setting the username and password, and entering the Wi-Fi password. For this reason, I’m a bit disappointed – it looked like the Raspberry Pi Imager program would “burn” the Wi-Fi password I use, but that didn’t happen. After a reset and logging in – everything works! In the embedded world, that’s not obvious – that’s why I’m happy!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1747233458116/0ca4db25-691f-4e45-9a24-8c093dd12d73.jpeg align="center")

The user interface is simple and clear, and I can see the option to launch communication buses and general system configuration – all through the graphical interface! In the next step, I’ll try to connect an air quality sensor to one of the interfaces and attempt to read basic parameters around the device