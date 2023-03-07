# Stressmeter 9000

**Team 2:** Team Stress-A-Lot

**Project Manager:** Sakari Lukkarinen

**Team Members:**
- Chad Clusker
- Igor Rynty
- Joona Rantala
- Francesco Natanni 
 
First year hardware project\
School of ICT\
Metropolia University of Applied Sciences

**Version History**
Version | Description | Date | Authors
------------- | ------------- | ------------- | -------------
1.0 | Created structure for the project plan. Added instructions for what should be included in the different parts of the document. | 31.1.2023 | Saana Vallius
1.1 | Review meeting. Notes are shown with yellow. | 6.3.2023 | Joseph Hotckiss, Keijo Länsikunnas, Saana Vallius, Miguel Cheneuer, Sakari Lukkarinen
1.2 | Updated commented parts according to what was decided in the review meeting. Changed the name of the document. | 7.3.2023 | Saana Vallius
1.3 | Removed mentions of adding teachers to Teams workspace. | 9.2.2023 | Saana Vallius
1.4 | Initiated structuring the project plan. | 9.2.2023 | CC, IR, FN, JR
1.5 | Finished up the “Schedule” & “Project Description” sections. | 16.2.2023 | CC, IR, FN, JR
1.6 | Finalized the remaining sections. | 3.3.2023 | CC, IR, FN, JR

[Introduction](#introduction)

[Project Description](#project-description)

[Communication](#communication)

[Version Control](#version-control)

[Schedule](#schedule)

[Goals](#goals)

## Introduction

The purpose of this document is to describe the project plan for “Stressmeter 9000” to be conducted during the first term of 2023 Hardware courses of school of ICT at Metropolia University of Applied Sciences. The planning for the project was done during the Hardware 1 course and the project itself will be carried out during the Hardware 2 course in March, April and May. The project’s main objective is to make a working portable heart rate monitor which works wirelessly and records data in real time. 
In order to do this, we will learn about the necessary hardware and software related to our project in order to carry it out successfully and have a functioning system.


## Project Description

Stressmeter 9000 is a portable device that uses photoplethysmography (PPG) technology to measure heart rate. The data is obtained using a Crowtail Pulse sensor 2.0 and then pre-processed by the Raspberry Pi Pico so that it can be sent to our server for HRV analysis. Once the data is finalized it will be stored in a database and a live view will be shown on an OLED display. In Figure 1 we can see how all the device components work in conjunction with each other. 

![Project Architecture Diagram](/Images/Project_arichitecture.png)
Figure 1. Project Architecture 

All hardware components and software tools that will be used to complete this project are listed below: 

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
    Digital rotary knob with push button. 

- **Raspberry Pi 4**\
    A computer that will be used to host our Web Server and for data storing purposes. 

- **ASUS RT-AX53U**\
    A 2x2 dualband WiFI router. 

The hardware components in the heart rate monitor device work together to measure the user's heart rate and display it in real-time. The Raspberry Pi Pico microcontroller reads the heart rate data from the Crowtail Pulse Sensor v2.0 and displays it on the OLED display. The user can interact with the device using the rotary knob to navigate the interface and select different options. The Raspberry Pi 4 is used to host the web server that stores the user's heart rate data and allows them to access it remotely. The ASUS RT-AX53U router connects the device to the internet, enabling remote access and analysis of the heart rate data. The protoboard is used to connect all the components together to create a functioning heart rate monitor device.

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

The software tools used in the heart rate monitor device work together to enable the device to measure, store, and analyse the user's heart rate data. MicroPython is used to program the Raspberry Pi Pico microcontroller to read the heart rate data from the Crowtail Pulse Sensor v2.0 and display it on the OLED display. Ulab is used to speed up mathematical operations on arrays. Apache 2 is used to create a custom web server that allows users to access and analyse their heart rate data remotely. Kubios Cloud is used to analyse the user's heart rate variability data, and MariaDB is used to store the user's heart rate data in a database. All of these software tools work together to create a functioning heart rate monitor device that can measure, store, and analyse the user's heart rate data.

## Communication

To ensure that our project work goes smoothly we will communicate with each other on a regular basis. In order to do that we will be using a combination of Microsoft Teams, Discord, GitHub and in-person meetings for all our communication purposes. Our own private Discord server as well as Microsoft Teams are used for online communication, GitHub for file sharing and storage and lastly, we use our in-person meetings to check up on team progress and evaluate next steps. The work on the project will be done as a combination of work from home and in-person meetings. For our meeting notes we will be using a specific channel in our Discord server for storing them.

## Version Control

We will be handling version control by primarily using GitHub. Additionally, we will be pushing each major update to our private GitLab repository which is accessible to our project coordinator. For document and material storage we will be using our Microsoft Teams, Discord server as well as GitHub.  

## Schedule

We as a team have agreed to keep a consistent schedule by having weekly meetings in which we evaluate what we have accomplished so far and what we plan to do next. After the planning stage is complete, we are aiming to invest more time in implementing Stressmeter 9000 by increasing the number of scheduled meetings. 

Below Figure 2 shows the estimated schedule for the project plan and the first stages of development.

![GANTT Project Schedule](/Images/GANTT.png)
Figure 2. GANTT Project Schedule


## Goals

Our team's goal is to better understand hardware systems by developing our own functional hardware system. The system must satisfy the guidelines set by the [Requirement Specifications Document](https://github.com/murphyslemon/RecoveryAndStressMeter/blob/main/RequirementSpecifications.md). We hope to attain a better understanding of how to implement various hardware components such as a protoboard, Raspberry Pi Pico, Crowtail Pulse Sensor and an OLED display. Additionally, we are looking to improve our software skills by utilizing the knowledge obtained previously in our software courses.

We will maintain a healthy and cooperative atmosphere within the team. Our team has not worked together previously so we look forward to improving our interpersonal communication skills and learning from each other.
