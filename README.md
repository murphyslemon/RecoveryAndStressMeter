# Stressmeter 9000
Team 2: Team Stress-A-Lot

Project Manager: Sakari Lukkarinen

Team Members:
- Chad Clusker
- Igor Rynty
- Joona Rantala
- Francesco Natanni 
 
First year hardware project\
School of ICT\
Metropolia University of Applied Sciences

## Introduction
This document describes the project plan for 'The recovery and stress meter project' to be conducted during the first term of 2023 Hardware courses at Metropolia University of Applied Sciences. The planning for the project is done during the Hardware 1 course and the project itself will be carried out during the Hardware 2 course in March, April and May 2023. 
The idea of this project is to make a portable heart rate monitor which works wirelessly and records data in real time. 
In order to do this, we will learn about the necessary hardware and software related to our project in order to carry it out successfully and have a functioning system.

## Project Description
### HARDWARE COMPONENTS:
- **Protoboard**\
    Passive protoboard specially designed for this project to help connect the other components to the Raspberry Pi Pico. 

- **Raspberry Pi Pico**\
    Dual-core ARM processor microcontroller having 246 kB SRAM and 2 MB on-board Flash. It also includes 2.4 GHz wireless LAN and 26 multifunction GPIO pins. 

- **Crowtail Pulse Sensor v2.0**\
    Optical heart rate sensor having LED, photodiode, analog amplifier, and analog signal output. Operating voltage 3-5 V. 

- **OLED Display**\
    SSD1306 compatible 128x64 monochrome organic LED-display. Communicates with I2C or UART-protocol. 

- **Rotary Knob**\
    - Digital rotary knob with push button. 

- **Raspberry Pi 4**\
    A computer that will be used to host our Web Server and for data storing purposes. 

- **ASUS RT-AX53U**\
    A 2x2 dualband WiFI router. 

### SOFTWARE TOOLS:
- **Raspberry Pi OS**\
    Operating system for the Raspberry Pi used in our server. 

- **Apache 2**\
    HTTP server software used to implement our own Web server for this project’s purposes. 

- **MicroPython**
    Language used to program the Raspberry Pi Pico microcontroller. 

- **Ulab**\
    A numpy-like module for MicroPython to speed up mathematical operations on arrays. 

- **Kubios Cloud**\
    A HRV (heart rate variability) analysis provider. 

- **MariaDB**\
    Database used to store our data. 

- **Thonny IDE**\
    Development environment for MicroPython. 

- **Wokwi**\
    A browser-based simulator for various boards, e.g. Arduino and Raspberry Pi Pico

![Project Architecture Diagram](/Images/Project_arichitecture.png)

## Communication
To ensure that our project work goes smoothly we will aim to communicate with each other on a regular basis. In order to do that we will be using a combination of Discord, GitHub and in-person meetings for all of our communication purposes. Our own private Discord server is used for online communication, GitHub for file sharing and storage and lastly we use our in-person meetings to check up on team progress and evaluate next steps. The work on the project will be done as a combination of work from home and in-person meetings. For our meeting notes we will be using a specific channel in our Discord server for storing them.

## Version Control

We will be handling version control by primarily using GitHub. Additionally, we will be pushing each major update to our private GitLab repository which is accessible to our project coordinator. For document and material storage we will be using our Discord server as well as GitHub. 

## Schedule
![GANTT Schedule](/Images/GANTT.png)

## Goals
Our teams goal is to better understand how hardware systems work by developing a fully functional system that we are satisfied with while maintaining a healthy and cooperative atmosphere within the team. We hope to attain a better understanding of how to implement various hardware components such as protoboard, Raspberry Pi Pico, Crowtail Pulse Sensor v2.0 and an OLED display. Additionally, we are looking to improve our practical software skills by utilizing the knowledge obtained previously. 
Our team has not worked together previously so we look forward to improving our interpersonal communication skills and learning from each other.


[def]: image