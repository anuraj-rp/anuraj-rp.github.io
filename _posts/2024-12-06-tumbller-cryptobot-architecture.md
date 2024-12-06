---
title: "Tumbller Cryptobot Architecture?"
date: 2024-12-06
author_profile: true
classes: wide
categories:
- robotics
tags:
  - cryptobotics
  - robotics
---

Two weeks ago I was at Devcon 7 in Bangkok and had a small demo with our small yakrover cryptobot tumbller there. Let's have a look at the architecture of the setup to understand how the tumbller cryptobot works.

### Hardware 

Tumbller is a robotics educational learning kit Elegoo. It runs on an Arduino Nano and does not have WiFi. To add WiFi to the Tumbller we decided to use an Arduino Nano ESP32 because it has the same pinout as Arduino Nano. But the problem was that the Tumbller PCB runs on 5V and Nano ESP32 on 3.3V. We designed a custom plugin board to fit on the Tumbller PCB that would voltage level translator in between the MCU and PCB board. We got the plugin board manufactured from JLCPCB in China. Here is a 3D render of the plugin board we designed.

<video width="560" height="315" controls>
  <source src="/assets/videos/2024-11-29-cyptobot-tumbler-plugin.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

The video stream from our YakRover weekly meetings where I explain the entire process of PCB design and manufacturing for Tumbller Plugin.

<iframe width="560" height="315" src="https://www.youtube.com/live/7VkJM0gVBCo?feature=shared&t=105" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


We also put a camera ESP32 on the robot. The camera is basically ESP32-CAM devkit. Each of our tumbller had two ESP32 microcontrollers. Both the ESP32 MCU connected to the same wifi access point. Let's call the ESP32 MCU controlling the tumbller robot motion tumbller-esp32-s3 and the camera ESP32 as tumbller-esp-cam. Each of the ESP32 MCU exposed functionality or affordance of the robot on the local network as a http REST endpoints.


### Software



The tumbller-esp32-s3 exposes the motion and motor control affordance of the cryptobot via five endpoints. The endpoints `/move/forward`, `/move/backward`, `/move/left`, `/move/right` and `/move/stop` control the movements for forward, backward, left, right and stop respectively.

The tumbller-esp-cam exposes the camera image via the `/getImage` endpoint so that when a GET request is sent to the endpoint it would return a image taken by the camera. 

The server for frames-v1 is written in python. The frames-v1 server, tumbller-esp32-s3 and the tumbller-esp-cam need to on the same network or VPN. We used tailscale to put all three on the same VPN. The ESP32s can be exposed on the tailscale VPN with tailscale subnets. If the frames server is running locally on a computer without DNS name then ngrok can be used to expose to the outside world. The payment gate for the rovers is generated using the awesome __Paybot__ farcaster bot by Rob Recht and Richard Sun. They helped us a lot in setting up the payment gate quickly with their farcaster bot. 