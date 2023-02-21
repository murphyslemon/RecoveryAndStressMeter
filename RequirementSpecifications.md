Sakari Lukkarinen
# Hardware 2 project requirements
Version 2.4\
06 February 2023\
Prepared for the Hardware 1 & 2 courses\
School of ICT\
Metropolia University of Applied Sciences

## Revision history
Version | Date | Reason for changes | Author
------------- | ------------- | ------------- | -------------
2.1 | 27.1.2023 | New version of the requirements specification using IEEE standard-based template | Sakari Lukkarinen
2.2 | 2.2.2023 | Changes based on requests, comments of the first change request meeting 30.1.2023. | Sakari Lukkarinen
2.3 | 5.2.2023 | Added missing hardware components, simplified the contents, use cases and functional requirements moved to Excel sheet | Joseph Hotckiss, Sakari Lukkarinen
2.4 | 6.2.2023 | Changes based on review meeting | Joseph Hotchkiss, Keijo Länsikunnas, Saana Vallius, Miguel Cheneuer, Sakari Lukkarinen

## Document approval
This document has been accepted and approved by the project teacher and management team:

Name | Title | Date
------------- | ------------- | -------------
Joseph Hotchkiss | Senior Lecturer  Project teacher | 6.2.2023
Keijo Länsikunnas | Senior Lecturer  Project teacher | 6.2.2023
Saana Vallius | Senior Lecturer\  Project teacher | 6.2.2023
Sakari Lukkarinen | Senior Lecturer  Project teacher  Project requirements manager | 6.2.2023


## Contents
[1	Introduction](#1-introductionIn)
- [1.1	Purpose](#11-purpose)
- [1.2	Scope](#12-scope)
- [1.3	Definitions, acronyms, and abbreviations](#13-definitions-acronyms-and-abbreviations)
- [1.4	References](#14-references)
- [1.5	Overview](#15-overview)

[2	General description](#2-general-description)
- [2.1	Product perspective](#21-product-perspective)
    - [2.1.1	Stress	10](#211-stress)
    - [2.1.2	Detecting heart rate](#212-detecting-heart-rate)
    - [2.1.3	Heart rate variability](#213-heart-rate-variability)
    - [2.1.4	Recovery and stress indexes](#214-recovery-and-stress-indexes)
- [2.2	Product functions](#22-product-functions)
    - [2.2.1	The purpose](#221-the-purpose)
    - [2.2.2	Application concept](#222-application-concept)
    - [2.2.3	Operating principle](#223-operating-principle)
    - [2.2.4	Key features](#224-key-features)
- [2.3	Use, users, and application characteristics](#23-use-users-and-application-characteristics)
- [2.4	Development tools](#24-development-tools)

[3	Specific requirements](#3-specific-requirements)
- [3.1	User interfaces](#31-user-interfaces)
    - [3.1.1	OLED display](#311-oled-display)
    - [3.1.2	Rotary encoder](#312-rotary-encoder)
    - [3.1.3	Grove connectors](#313-grove-connectors)
    - [3.1.4	Heart rate sensor](#314-heart-rate-sensor)
    - [3.1.5	USB-port](#315-usb-port)
- [3.2	Use cases](#32-use-cases)
- [3.3	MicroPython modules and classes](#33-micropython-modules-and-classes)
    - [3.3.1	SSD1306](#331-ssd1306)
- [3.4	Non-functional requirements](#34-non-functional-requirements)

[4 Change management process](#4-change-management-process)

[5 References](#5-references)



## 1 Introduction 
This document is adapted from Software Requirements Specification Template prepared for Software Engineering Principles I course by A. David McKinnon, Washington State University, March 2005 [1]. The template is based upon the IEEE Guide to Software Requirements Specification (ANSI/IEEE Std. 830-1984) [2], and the SRS templates of Dr. Orest Pilskans (WSU, Vancover) and Jack Hagemeister (WSU, Pullman). 

This document should contain all the information needed by an engineering student team to adequately design and implement the product described by the requirements listed. 

### 1.1 Purpose 
The purpose of this document is to give the requirements for the hardware project for the first year ICT engineering students studying at Metropolia University of Applied Sciences. The intended audience of this document is both the students and the lecturers guiding the project.  

### 1.2 Scope 
In this project a heart rate detection and analysis system is to be produced. The aims for the project are:  
1. develop a heart rate detection algorithm that works on the device locally, 
2. to calculate heart rate variability (HRV) analysis,  
3. to send, store, and read HRV data to/from a server, 
4. build a connection to Kubios Cloud HRV analysis service to calculate more detailed HRV analysis, and  
5. show the estimated stress and recovery status indexes on the device.   

The device is intended to be used in home or office environments either by the end users themselves or together with health and wellbeing professionals such as physiotherapists, nurses, or medical doctors. 

The device detects the heart rate and its variability using a photoplethysmography (PPG). It measures optically blood volume changes in the microvascular bed of tissue. The change in volume is detected by measuring the light emitted by the light emitting diodes (LEDs), absorbed by the tissues, and detected with photodiodes. The heart rate can be measured from the peaks of the alternating signal presenting the volumetric blood changes in the tissue. 

### 1.3 Definitions, acronyms, and abbreviations 
Term | Definition
------------- | -------------
α | Slope of the linear interpolation of the spectrum in a log-log scale 
ANS | Autonomous nervous system 
BPM | Beat per minute 
ECG | Electrocardiogram 
IBI | Inter-beat-interval, measured from PPG signal, given in milliseconds (ms) 
HF | High frequency (0.15 - 0.4 Hz) 
HR | Heart rate, typically given in units of beat per minute (BPM) 
HRV | Heart rate variability, measures how variability there is  in the heart rate from beat to beat over a longer period, can be characterized by several parameters 
Hz | Hertz, cycles per second, unit for frequency 
LAN | Local area network 
LED | Light emitting diode 
LF | Low frequency (0.04 - 0.15 Hz) 
LF/HF | Ratio of LF/HF 
ms | millisecond 
NN interval | Time difference between two peaks either in ECG or PPG signal, either PPI or RRI (ms) 
NN50 count | Number of pairs of adjacent NN intervals differing more than 50 ms 
OLED | Organic light-emitting diode 
pNN50 | NN50 count divided by the total number of all NN intervals 
Poincaré plot | a type of recurrence plot used to quantify self-similarity in processes, usually periodic functions 
PPI | peak-to-peak interval, time difference between two pulse peaks in photoplethysmography signal measured in ms 
PPG | Photoplethysmography, optically detected heart pulse typically detected from peripheral blood circulation, like from finger, wrist, toe, or ear lobe 
PNS | Parasympathetic nervous system, part of autonomic nervous system 
PTSD | Post-traumatic stress disorder 
RMSSD | The square root of sum of squares of differences (ms) 
RRI | RR-interval, time difference between two R-peaks in ECG signal (ms) 
SD1 | Poincaré plot index, the first ellipse shape parameter estimated from the Poincaré plot 
SD2 | Poincaré plot index, the second ellipse shape parameter estimated from the Poincaré plot 
SDANN | Standard deviation of the average of NN intervals (ms)   
SDNN | Standard deviation of all NN intervals (ms) 
SI | Baevsky’s stress index 
SDSD | Standard deviation of differences between adjacent NN intervals measured in milliseconds (ms) 
SNS | Sympathetic nervous system, part of autonomic nervous system 
ULF | Ultra-low frequency (0 - 0.003 Hz) 
USB | Universal serial port 
WiFi | Wireless fidelity 
VLF | Very flow frequency (0.003 - 0.04 Hz) 

### 1.4 References 
A complete list of all documents referenced is provided at the end of this document in Chapter 5, References. 

### 1.5 Overview 
Chapter 2 describes the general factors that affect the product and its requirements. Chapter 3 gives the specific requirements that are used to guide the project’s design, implementation, and testing. Chapter 4 identifies and describes the process that will be used when project scope or requirements change. Chapter 5 lists all documents referenced in this document. 

## 2 General description 
In this section the general factors that affect the product and its requirements are described.  This section does not state specific requirements; it only makes those requirements easier to understand. 

### 2.1 Product perspective 
#### 2.1.1 Stress 
Stress is defined as “a physical, mental, or emotional factor that causes bodily or mental tension” [3]. According to the American Institute of Stress [4] [5]: 
* 77 % of people experience stress that affects their physical health 
* 73 % of people have stress that impacts their mental health 
* 48 % of people have trouble sleeping because of stress 
* 33 % of people report feeling extreme stress 
 
![Figure 1](/Images/RequirementsSpecifications/fig1.png)

Figure 1. Very high stress often affects the body. Many people get unpleasant feelings. Original from [6]. 

Physiological or mental imbalance can induce stress. Our autonomic nervous system (ANS) quickly responds with physiological changes through our sympathetic (SNS) and parasympathetic (PNS) nervous systems. During the stress response our body’s endocrine system releases hormones, and several changes in our physiological state occur. For example, heart rate (HR) can even double or triple and causes changes to HRV. [7] 

#### 2.1.2 Detecting heart rate 
The heart rate or pulse rate measures how often the heart beats and is given in units of beats per minute (BPM). Usually, the heart rate varies on the body’s physical need, but is also affected by physical fitness, stress of psychological status, diet, drugs, hormones, environment, diseases, and illnesses. The normal resting adult heart rate is 60-100 BPM. During sleep, a heart rate of 40-50 BPM is common and considered normal. [8]  

Heart rate variability (HRV) is the variation of the time intervals between heartbeats, and it is measured in units of seconds (s), or more commonly, in milliseconds (ms). Other terms used include RR interval (RRI) variability, where R corresponds to the peak of QRS-complex of electrocardiography (ECG), and Peak-to-Peak interval, if the HRV is measured optically.  Figure 2 visualizes heart HRV with R-R interval (RRI) changes. [9] 

![Figure 2](/Images/RequirementsSpecifications/fig2.png)
 
Figure 2. Heart rate variability (HRV) calculated from the R-R intervals (RRI) [9]. 

Heart rate variability can be detected with various methods. ECG is considered the golden standard for HRV measurement [9]. Other methods are photoplethysmography (PPG), which detects the heart rate variability optically, usually measured from fingers, wrists, forehead or earlobes, blood pressure or ballistocardiography, which measures small changes in body’s weight when the blood flows from the heart to the aorta.  

Figure 3 shows a typical fitness and wellness watch having an optical heart rate sensor [10]. The light emitting diodes (LEDs) and optical detectors are seen on the back of the watch. 
 
![Figure 3](/Images/RequirementsSpecifications/fig3.png)
 
Figure 3. An example of fitness and wellness watch having an optical heart rate sensor. [10] 

Figure 4 shows an example of photoplethysmography signal recorded with wrist worn pulse oximetry [11]. The device is shown on the left. The sensor is attached to the thumb. The PPG signal is shown on the right. The inter-beat-interval (IBI) is calculated from the negative peaks (the bottoms) of the PPG signal. It could be calculated also from the positive peaks (the maximum) or from the rising edges of the signal.  

![Figure 4](/Images/RequirementsSpecifications/fig4.png)

Figure 4. An example of photoplethysmography signal recorded with pulse oximetry used on the thumb. [11] 

#### 2.1.3 Heart rate variability 
At present there is no accepted standard for stress evaluation. However, several HRV variables change in response to stress. Usually, stress induces low parasympathetic nervous system activity, which is associated with variation of some HRV variables such as high-frequency (HF) band and an increase in the low-frequency (LF) band. [7] 

The European Society of Cardiology together with the North American Society of Pacing and Electrophysiology have defined and established the standards for the measurement, physiological interpretation, and clinical use of HRV [12]. The most used time-domain and frequency-domain measures of HRV are summarized in Table 1 and Table 2. 

Table 1. Selected time-domain measures of HRV [12]. 
<table>
  <thead>
    <tr>
      <th>Variable</th>
      <th>Unit</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
  <tr>
        <td align="center" colspan="3">Statistical measures</td>
    </tr>
    <tr>
      <td>SDNN</td>
      <td>ms</td>
      <td>Standard deviation of all NN intervals</td>
    </tr>
    <tr>
      <td>SDANN</td>
      <td>ms</td>
      <td>Standard deviation of the averages of NN intervals in all 5-minute segments of the entire recording</td>
    </tr>
    <tr>
      <td>RMSSD</td>
      <td>ms</td>
      <td>The square root of the mean of the sum of the squares of differences between adjacent NN intervals</td>
    </tr>
    <tr>
      <td>SDNN index</td>
      <td>ms</td>
      <td>Mean of the standard deviations of all NN intervals for all 5-minute segments of the entire recording</td>
    </tr>
    <tr>
      <td>SDSD</td>
      <td>ms</td>
      <td>Standard deviation of differences between adjacent NN intervals</td>
    </tr>
    <tr>
      <td>NN50 count</td>
      <td></td>
      <td>Number of pairs of adjacent NN intervals differing by more than 50 ms in the entire recording; three variants are possible counting all such NN intervals pairs or only pairs in which the first or the second interval is longer</td>
    </tr>
    <tr>
        <td align="center" colspan="3">Geometric measures</td>
    </tr>
    <tr>
      <td>pNN50</td>
      <td>%</td>
      <td>NN50 count divided by the total number of all NN intervals</td>
    </tr>
    <tr>
      <td>HRV triangular index</td>
      <td></td>
      <td>Total number of all NN intervals divided by the height of the histogram of all NN intervals measured on a discrete scale with bins of 7.8125 ms (1/128 seconds)</td>
    </tr>
    <tr>
      <td>TINN</td>
      <td>ms</td>
      <td>Baseline width of the minimum square difference triangular interpolation of the highest peak of the histogram of all NN intervals</td>
    </tr>
    <tr>
      <td>Differential index</td>
      <td>ms</td>
      <td>Difference between the widths of the histogram of differences between adjacent NN intervals measured at selected heights (e.g., at the levels of 1,000 and 10,000 samples)</td>
    </tr>
    <tr>
      <td>Logarithmic index</td>
      <td></td>
      <td>Coefficient φ of the negative exponential curve k · e−φt, which is the best approximation of the histogram of absolute differences between adjacent NN intervals</td>
    </tr>
  </tbody>
</table>

Table 2. Selected frequency-domain measures of HRV [12]. 

<table>
  <tr>
    <th>Variable</th>
    <th>Unit</th>
    <th>Description</th>
    <th>Frequency range</th>
  </tr>
  <tr>
    <td align="center" colspan="4">Analysis of short-term recordings (5 min)</td>
  </tr>
  <tr>
    <td>5-min total power</td>
    <td>ms2</td>
    <td>The variance of NN intervals over the temporal segment</td>
    <td>≈≤0.4 Hz</td>
  </tr>
  <tr>
    <td>VLF</td>
    <td>ms2</td>
    <td>Power in VLF range</td>
    <td>≤0.04 Hz</td>
  </tr>
  <tr>
    <td>LF</td>
    <td>ms2</td>
    <td>Power in LF range</td>
    <td>0.04–0.15 Hz</td>
  </tr>
  <tr>
    <td>LF norm</td>
    <td>n.u.</td>
    <td>LF power in normalized units LF/(total power-VLF)×100</td>
    <td></td>
  </tr>
  <tr>
    <td>HF</td>
    <td>ms2</td>
    <td>Power in HF range</td>
    <td>0.15–0.4 Hz</td>
  </tr>
  <tr>
    <td>HF norm</td>
    <td>n.u.</td>
    <td>HF power in normalized units HF/(total power-VLF)×100</td>
    <td></td>
  </tr>
  <tr>
    <td>LF/HF</td>
    <td></td>
    <td>Ratio LF/HF</td>
    <td></td>
  </tr>
  <tr>
    <td align="center" colspan="4">Analysis of entire 24 hours</td>
  </tr>
  <tr>
    <td>Total power</td>
    <td>ms2</td>
    <td>Variance of all NN intervals</td>
    <td>≈≤0.4 Hz</td>
  </tr>
  <tr>
    <td>ULF</td>
    <td>ms2</td>
    <td>Power in the ULF range</td>
    <td>≤0.003 Hz</td>
  </tr>
  <tr>
    <td>LF</td>
    <td>ms2</td>
    <td>Power in the VLF range</td>
    <td>0.003–0.04 Hz</td>
  </tr>
  <tr>
    <td>VLF</td>
    <td>ms2</td>
    <td>Power in the LF range</td>
    <td>0.04–0.15 Hz</td>
  </tr>
  <tr>
    <td>HF</td>
    <td>ms2</td>
    <td>Power in the HF range</td>
    <td>0.15–0.4 Hz</td>
  </tr>
  <tr>
    <td>α</td>
    <td></td>
    <td>Slope of the linear interpolation of the spectrum in a log-log scale</td>
    <td></td>
  </tr>
</table>

ULF = Ultra low frequency, VLF = Very low frequency, LF = Low frequency, HF = High frequency.  

Time-domain analysis measures variation in the intervals between successive cardiac cycles whereas frequency-domain analysis provides information how power is distributed as function of frequency. [7] 

#### 2.1.4 Recovery and stress indexes 
Based on the common measures of HRV, special indexes representing the parasympathetic and sympathetic cardiac activity have been developed. For example, Kubios HRV software is based on the following parameters to calculate PNS and SNS indexes [13]: 

* Mean RR interval 
* Root mean square of successive RR interval differences (RMSSD) 
* Poincaré plot index SD1 and SD2 in normalized units 
* Baevsky’s stress index (SI) 

Each parameter is compared to their normal population values and the values are then scaled with standard deviations (SD) of normal population and finally a proprietary weighting is applied to obtain the index values. These are illustrated in Figure 2 and Figure 3.  

![Figure 5](/Images/RequirementsSpecifications/fig5.png)

Figure 5. Parasympathetic nervous system (PNS) index. High positive values are interpreted as a good recovery of the test subject. [13] 

![Figure 6](/Images/RequirementsSpecifications/fig6.png)

Figure 6. Sympathetic nervous system (SNS) index. High negative values are interpreted as a low stress of the test subject. [13] 

Positive index values tell how many SDs above the normal population average values are, whereas a negative value tells the value is below normal values [13]. PNS index describes the parasympathetic tone and can be interpreted as the ability to recover from stress, as SNS index describes the sympathetic cardiac activity and can be interpreted as the current stress situation. An article “HRV analysis methods” gives a more detailed description of the analysis methods [14]. 

### 2.2 Product functions 
#### 2.2.1 The purpose 
The aim is to develop a working proof-of-concept of the recovery and stress meter. A suitable microcontroller board and additional components are used. The Raspberry Pi Pico was selected for that purpose, as the Raspberry Pi products are extensively supported by the manufacturers and by the user community. 

Metropolia University of Applied Sciences’ teaching personnel together with senior students have evaluated and selected the hardware components for the project. In addition, a special board for development of IoT devices with Raspberry Pi Pico is designed and tested by one of the senior lecturers. The background development and research results are openly available and readable in Theseus [15] [16] [17]. 

#### 2.2.2 Application concept 
The core of the proof-of-concept is Raspberry Pi Pico, a small and versatile microcontroller board designed for IoT devices. The device is adaptable to a wide range of applications in home, hobby, education, and industry. It is programmable both in C and MicroPython, of which MicroPython is used for this project. The device has a rich set of peripherals, including SPI, I2C, and programmable I/O state machines for custom peripheral support. It has also a wireless version, Raspberry Pi Pico W, having a fully certified wireless LAN module. [18] 

![Figure 7](/Images/RequirementsSpecifications/fig7.png)

Figure 7. Photograph of the development board with connected Raspberry Pi Pico board, OLED display and optical heart rate sensor. 

The development board is shown in Figure 7. To the bottom left the rotary switch and knob is shown. Above it is a 128x64 wide OLED display. At the upper left corner 3 LEDs and two of the three micro buttons are shown, which can be used for interacting with the development board. In the middle, the Raspberry Pi Pico board with soldered pins is shown. The Pico board is connected to the laptop or desktop through a USB-cable (black cable at the top of the figure). On the right, 4-pin Grove-connectors for connecting serial communication devices, like I2C sensors or analog input sensors, are shown. The optical heart rate sensor is connected to one of the Grove-connectors and Pico’s ADC_0 pin and is shown above the development board. The components used in the proof-of-concept product are listed in Table 3. 

Table 3. Component used in the proof-of-concept product. 

Component | Description | More info 
------------- | ------------- | -------------
Raspberry Pi Pico | Dual-core ARM processor microcontroller having 246 kB SRAM and 2 MB on-board Flash. It also includes 2.4 GHz wireless LAN and 26 multifunction GPIO pins. | [Raspberry Pi Pico series – Raspberry Pi](https://www.raspberrypi.com/products/raspberry-pi-pico/) 
Crowtail Pulse Sensor v2.0 | Optical heart rate sensor having LED, photodiode, analog amplifier, and analog signal output. Operating voltage 3-5 V | [Crowtail- Pulse Sensor 2.0 (elecrow.com)](https://www.elecrow.com/crowtail-pulse-sensor-p-1673.html)  
OLED display | SSD1306 compatible 128x64 monochrome organic LED-display. Communicates with I2C or UART-protocol. | [Sensors Modules SSD1306 Oled Display - Sensors Modules](https://www.electronicwings.com/sensors-modules/ssd1306-oled-display) , [Using a SSD1306 OLED display — MicroPython latest documentation](https://docs.micropython.org/en/latest/esp8266/tutorial/ssd1306.html) 
Protoboard | Passive protoboard specially designed for this project to help connect the other components to the Raspberry Pi Pico. | Joseph Hotchkiss, Project Engineer, Metropolia UAS 
Rotary knob | Digital rotary knob with push button. | Joseph Hotchkiss, Project Engineer, Metropolia UAS 

#### 2.2.3 Operating principle 
The heart rate is detected using the optical heart rate sensor (Pulse Sensor v2.0, Crowtail) [19]. The analog signal is converted into digital using Raspberry Pi Pico’s AD-converters. The heart rate is calculated using peak-detection algorithms for photoplethysmography (PPG) signals using Pico’s central processing unit (CPU). The operation can be controlled using the rotary switch and knob. Results and feedback to the user are shown on the OLED display. In addition, the extra LEDs can be used to indicate, for example, the quality of the signal or the data collection operations to the user. 

The data is preprocessed with Pico. Pico’s wireless connection can be used to send the data to a cloud server and return the analysis results to the development board and show them to the user. Figure 8 illustrates the cloud and web-server architecture of the system. 

![Figure 8](/Images/RequirementsSpecifications/fig8.png)

Figure 8. Illustration of the web-server architecture of the whole system. 

The development board acquires and records the optical heart pulse data and preprocesses the data as seen in Figure 8. All heart rate calculations can be also processed in the development board. The time stamped preprocessed pulse data is sent wirelessly to the base station which sends the data to the Web server. The data is stored in the webserver’s database where more analysis and reporting can be done. The health care professional interacts with the webserver through Web clients. 

#### 2.2.4 Key features 
The following Table 4. recaps the key features of the system. 

Table 4. Key features of the system. 

Key Feature | Description
------------- | -------------
HRV detection | PPG signal is detected using the optical pulse sensor and the heart rate variability is measured using the development board’s MCU. 
Display | The system has an OLED display capable of showing both text and graphics. 
Controls | The system has a rotary switch control knob with push button. The control knob can be used for controlling the operation of the system. 
MCU | The system contains an MCU with Flash and RAM memory and several peripheral connections enabling to process the detected PPG signal and calculate the inter-peak-interval variations. The raw HRV data (PPI) can be further analyzed using the system or sent wirelessly to a Cloud Server for further calculations. 
Wireless connection | The system contains a wireless WiFi transceiver. It gives the opportunity to send and receive data to WLAN and Cloud Servers. 
USB connection | The system contains a USB connection. The USB can be used to control, code, and download the executable files. In addition, it can be used to debug the code and download and upload data files between the development board and laptop. The USB-port can also be used to power the system, if necessary. 

### 2.3 Use, users, and application characteristics 
The final system is intended to be used for measuring the recovery and stress index based on HRV analysis detected optically from the finger, wrist, hand palm, arm, upper arm, chest, cheek, forehead, or earlobe.  

The system is intended to be used by a person, patient, customer, or healthcare professional aiming to measure the subject’s recovery and stress index. The information can be used to help understand the study subject’s current situation. The system is used in a normal home or office environment. 

The system can be used to analyze the psychophysiological state. HRV is related to emotional arousal, conditions of acute time pressure and emotional strain, and elevated anxiety state.  HRV has also been shown to be reduced in individuals reporting to worry more. In individuals with post-traumatic stress disorder (PTSD), HRV is reduced. [9] 

### 2.4 Development tools 
Thonny IDE for programming the Raspberry Pi Pico and MicroPython as a programming language are used for developing the software for the product.  

MicroPython is a special limited version of the newest Python versions [20]. It has less libraries and options than the normal desktop Python and uses some special libraries like machine, utime, urequests, ujson, etc., which are developed for embedded systems.  

Thonny IDE is a special Python IDE developed having focus on the embedded systems [21]. It is easy to get started with and comes with the Python 3.10 built in. In addition, it can be used to download the MicroPython firmware to embedded boards, like Raspberry Pi Pico, and you can start programming the Raspberry Pi Pico directly.  

Ulab is a special numpy-like module for MicroPython and its derivatives may be used for advanced algorithm development, like for pre-processing the photoplethysmographic signal. Ulab module is “meant to simplify and speed up common mathematical operations on arrays.” [22] It is an asset, especially when we start to implement heart rate detection algorithms.   

Wokwi is an online electronic simulator [23]. It can be used to simulate Raspberry Pi Pico, Arduino, ESP32, and boards, electronic parts, and sensors. Links for Raspberry Pi Pico simulator with MicroPython, SSM1306 OLED, and Hardware project simulator are provided for developing the system [24] [25] [26] . The hardware project simulator is based on the protoboard. The simulator contains all the same components as in the real protoboard, except the heart rate sensor. It can be used for learning and testing how the system works before using any real hardware.  

We have also a license for Kubios Cloud which is an Amazon Web Services (AWS) based cloud service using REST API interface [27]. The goal of this project is making a full HRV analysis based on the inter-beat-interval (IBI) calculations on Raspberry Pi Pico. The IBI data can be send first to a Webserver and from there to Kubios Cloud and get the HRV analysis results back. It is possible to get the full recovery and stress analysis results in the device.   

## 3. Specific requirements 
This section gives the requirements that are used to guide the project’s design, implementation, and testing. Attention has been paid to carefully organize the requirements presented, so that they may easily be accessed and understood.  Furthermore, the reader should notice, that this document is not the system design document. 

### 3.1 User interfaces 
The user can control the operation of the device using the rotary switch and knob. Results and user feedback are shown on the OLED display. In addition, the extra LEDs can be used to indicate, for example, the quality of the signal or the data collection operations to the user. 

#### 3.1.1 OLED display 
The OLED display has 128x64 pixels and can display both text and graphics as shown in Figure 9. The display is controlled by SSD1306 circuit which is embedded to the display. The SSD1306 compatible OLED display uses either a SPI or I2C interface. MicroPython documentation gives examples how to use the library [28]. A suitable SSD1306 MicroPython compatible library can be downloaded, for example, from here [29]. 

![Figure 9](/Images/RequirementsSpecifications/fig9.png)
 
Figure 9. SSD1306 compatible OLED-display used in the project. 

#### 3.1.2 Rotary encoder 
A rotary encoder is a device that will provide you with pulses to indicate the direction and speed of the rotation. The device has three outputs ROT A, ROT B, and Rot Switch. The Rot Switch behaves just like a standard push button tactile switch. When you press the knob in, the signal goes from high to low or low to high depending on how the encoder is wired up. Figure 10 illustrates the rotary encoder. 

![Figure 10](/Images/RequirementsSpecifications/fig10.png)

Figure 10. A rotary encoder with integrated push button switch. 

When you rotate the knob in one direction or the other, then the Rot A and Rot B will output a series of pulses out of phase of one another. In one direction Rot A phase will lead Rot B and when turning the other direction Rot A will trail Rot B. 

This means that we can essentially use one channel either Rot A or Rot B as a clock signal and then check the state of the other pin to identify the direction of the rotation. Let’s look at two examples. In both cases we will use Rot B as the clock and Rot A will indicate the direction of the turn.  

In Figure 11 you can see that when Rot B goes from low to high the value on Rot A is zero. In this case it is indicating Clockwise rotation. The more clock pulses per second indicates faster rotation of the encoder. 
 
![Figure 11](/Images/RequirementsSpecifications/fig11.png)
 
Figure 11. Illustration of the Rot A and Rot B signals, when the rotary knob is turned Clockwise direction. 

In Figure 12 the opposite case is true. When Rot B (clock signal) goes from low to high it can be observed that the state of the Rot A pin is high. This indicates Counter or Anti-clockwise rotation. The speed of rotation is indicated in the same way. 

![Figure 12](/Images/RequirementsSpecifications/fig12.png)

Figure 12. Illustration of the Rot A and Rot B signals when the rotrary knob is turned Anti-clockwise direction. 

#### 3.1.3 Grove connectors 
The hardware provides 6 modular, standardized Grove connectors for prototyping purposes [30]. The Grove connector is also compatible with Crowtail connectors and cables. The Grove connector and Grove cables are shown in Figure 13 and Figure 14. 

![Figure 13](/Images/RequirementsSpecifications/fig13.png)

Figure 13. A 4-pin 2.0 mm pitch DIP Grove female header [31]. 

![Figure 14](/Images/RequirementsSpecifications/fig14.png)

Figure 14. A 4-bin buckled Grove cables [31]. 

The Grove connector has 4 pins. One of the pins is the reserved for the operating voltage (Vcc) and the second for the ground. For digital connectors the remaining pins are usually the clock and data pin. If the connector is used for analog signals, the remaining pins are usually reserved for the analog inputs. 

#### 3.1.4 Heart rate sensor 
Crowtails pulse sensor v2.0 is connected through the Grove-connector to the Raspberry Pi Pico’s analog inputs [19]. The heart rate sensor is shown in Figure 15 and Figure 16.  

![Figure 15](/Images/RequirementsSpecifications/fig15.png)

Figure 15. Crowtail pulse sensor v2.0 shown from the back (component) side. 

![Figure 16](/Images/RequirementsSpecifications/fig16.png)

Figure 16. Crowtail pulse sensor v2.0 shown from the front (sensor) side. 

The electrical components of the heart rate sensor are soldered on the bottom side of the sensor PCB (Figure 15). The component side also includes the Grove-connector used for connecting the sensor to the protoboard. 

The finger (or other place location on which the heart rate is detected) is on the front side of the sensor PCB (Figure 16). In the middle of the board is a LED, which is used to transmit the light to the body tissue. Below the LED is an optical sensor, photodiode, which receives the reflected light and converts the signal to analog voltage. 

#### 3.1.5 USB-port 
The Raspberry Pi Pico has a micro-USB port that can be used to access the USB bootloader stored in the RP2040 boot ROM. It can also be used by user code, to access an external USB device or host ​[32]​.  Figure 17 shows the Raspberry Pi Pico board and its USB-port. 

![Figure 17](/Images/RequirementsSpecifications/fig17.png)
 
Figure 17. The Raspberry Pi Pico board [32]. 

### 3.2 Use cases 
The summary and details of use cases are described in Table X1 and Table X2 of the document Requirements specification (v1).xlsx (version 1.0, 5.2.2023). 

### 3.3 MicroPython modules and classes 
In this subchapter the required MicroPython modules and classes to develop the system are introduced. 

#### 3.3.1 SSD1306 
Micropython’s ssd1306 library is used to control the OLED display [33] [28]. A fork of the driver can be studied at Github [29]. Ssd1306 library relies on MicroPython-specific library FrameBuffer, which provides support for graphics primitives (fill, pixel, hline, vline, line, rect, ellipse, poly), drawing text (text), and other methods (scroll, blit) [34]. 

### 3.4 Non-functional requirements 
The non-function (quality) requirements are described in the document Requirements specifications (v1).xlsx (version 1.0, 5.2.2023), in Table X4. Non-functional requirements. 

## 4 Change management process 
Team members can suggest changes by discussing with the project teachers, sending emails, or directly reviewing and commenting this document. This document is maintained and updated by the project management team (project teachers).  

The project scope and requirements changes are reviewed regularly, minimum every second week, during the hardware 1 and 2 courses. The changes are approved by the project management team after change review meetings.  

## 5 References 
Reference Number | Reference
------------- | -------------
[1] | A. D. McKinnon, “Software Engineering Principles I,” Washington State University, March 2005. [Online]. Available: https://users.tricity.wsu.edu/~mckinnon/cpts322/. [Accessed 2 February 2023]. 
[2] | “IEEE Recommended Practice for Software Requirements Specifications,” IEEE Computer Society, 1998. [Online]. Available: https://www.cse.msu.edu/~cse870/IEEEXplore-SRS-template.pdf. [Accessed 2 February 2023]. 
[3] | C. P. Davis, “Medical Definition of Stress,” MedicineNet, 29 3 2021. [Online]. Available: https://www.medicinenet.com/stress/definition.htm. [Accessed 22 9 2022]. 
[4] | E. Patterson, “Stress Facts and Statistics,” The Recovery Village, 05 Sept 2022. [Online]. Available: https://www.therecoveryvillage.com/mental-health/stress/stress-statistics/. [Accessed 23 09 2022]. 
[5] | The American Institute of Stress, “What is Stress?,” The American Institute of Stress, [Online]. Available: https://www.stress.org/daily-life. [Accessed 23 09 2022]. 
[6] | WHO, “Doing What Matters in Times of Stress: An Illustrated Guide,” 29 April 2020. [Online]. Available: https://www.who.int/publications/i/item/9789240003927. [Accessed 23 09 2022]. 
[7] | H. Kim, E. Cheon, D. Bai, Y. LEE and B. Koo, “Stress and Heart Rate Variability: A Meta-Analysis and Review of the Literature,” Psychiatry Investig., vol. 15, no. 3, pp. 235-245, 2018.  
[8] | “Heart rate,” Wikipedia, [Online]. Available: https://en.wikipedia.org/wiki/Heart_rate. [Accessed 2 Dec 2022]. 
[9] | “Heart rate variability,” Wikipedia, [Online]. Available: https://en.wikipedia.org/wiki/Heart_rate_variability. [Accessed 2 Dec 2022]. 
[10] | “Polar Ignite 3,” Polar, [Online]. Available: https://www.polar.com/en/ignite3. [Accessed 02 Dec 2022]. 
[11] | P. H. Charlton, P. Kyriaccou, J. Mant and J. Alastruey, “Acquiring Wearable Photoplethysmography Data in Daily Life: The PPG Diary Pilot Study,” Eng. Proc., vol. 2, no. 20, 2020.  
[12] | M. Malik, J. T. Bigger, A. J. Camm, R. E. Kleiger, A. Malliani, A. J. Moss and P. J. Schwartz, “Heart rate variability: Standards of measurement, physiological interpretation, and clinical use,” European Heart Journal, vol. 17, no. 3, pp. 354-381, 1996.  
[13] | “HRV in Evaluating ANS Function,” Kubios Oy, [Online]. Available: https://www.kubios.com/hrv-ans-function/. [Accessed 24 11 2022]. 
[14] | “HRV Analysis Methods,” Kubios Oy, [Online]. Available: https://www.kubios.com/hrv-analysis-methods/. [Accessed 24 11 2022]. 
[15] | G. Zoltan, “Implementation of LoRaWAN : from end-device to application,” Metropolia University of Applied Sciences, Helsinki, 2021. 
[16] | E. Besic, “Implementation of first-year hardware theme project for ICT students,” Metropolia University of Applied Sciences, Helsinki, 2022. 
[17] | J. Piri, “Käsiproteesin ohjain – prototyypin kehitystyö,” Metropolia University of Applied Sciences, Helsinki, 2022. 
[18] | “Raspberry Pi Pico: Powerful, flexible microcontroller boards, available from $4,” Raspberry Pi Foundation, [Online]. Available: https://www.raspberrypi.com/products/raspberry-pi-pico/. [Accessed 25 11 2022]. 
[19] | “Crowtail - Pulse Sensor,” Electrow, 29 July 2022. [Online]. Available: https://www.elecrow.com/wiki/index.php?title=Crowtail-_Pulse_Sensor. [Accessed 28 Nov 2022].
[20] | D. George, “MicroPython,” George Robotics Limited, 2014-2023. [Online]. Available: https://micropython.org/. [Accessed 2 February 2023]. 
[21] | “Thonny - Python IDE for beginners,” University of Tartu, Cybernetica, and Raspberry Pi Foundation, 2014-2023. [Online]. Available: https://thonny.org/. [Accessed 2 February 2023]. 
[22] | Z. Vörös, “The ulab book, Revision f2dd2230,” Read the Docs, [Online]. Available: https://micropython-ulab.readthedocs.io/en/latest/index.html. [Accessed 2 February 2023]. 
[23] | “Wokwi - Simulate IoT Projects in Your Browser,” CodeMagic LTD, 2019-2023. [Online]. Available: https://wokwi.com/. [Accessed 2 February 2023]. 
[24] | “New MicroPython on Raspberry Pi Pico Project,” CodeMagic Ltd, 2019-2023. [Online]. Available: https://wokwi.com/projects/new/micropython-pi-pico. [Accessed 02 Feb 2023]. 
[25] | S. Lukkarinen, “Pico with SSD1306 v2 - Wokwi Arduino and ESP32 Simulator,” CodeMagic Ltd, 2019-2023. [Online]. Available: https://wokwi.com/projects/354671838787709953. [Accessed 02 Feb 2023]. 
[26] | S. Lukkarinen, “Hardware project simulator - Wokwi Arduino and ESP32 Simulator,” CodeMagic Ltd, 2019-2023. [Online]. Available: https://wokwi.com/projects/354682548125570049. [Accessed 02 Feb 2023]. 
[27] | “Kubios Cloud,” Kubios Oy, 2023. [Online]. Available: https://www.kubios.com/kubios-cloud/. [Accessed 2 February 2023]. 
[28] | P. S. a. c. Damien P. George, “Using a SSD1306 OLED display,” 01 Feb 2023. [Online]. Available: https://docs.micropython.org/en/latest/esp8266/tutorial/ssd1306.html?highlight=ssd1306. [Accessed 02 Feb 2023]. 
[29] | stlhemann, “micropython-ssd1306,” 16 Dec 2020. [Online]. Available: https://github.com/stlehmann/micropython-ssd1306. [Accessed 02 Feb 2023]. 
[30] | “Grove System,” Seeed Technology Co, Ltd., 2008-2021. [Online]. Available: https://wiki.seeedstudio.com/Grove_System/. [Accessed 02 Feb 2023]. 
[31] | “Grove accessories,” Seeed Studio, 2023. [Online]. Available: https://www.seeedstudio.com/Grove-Accessories-c-1969.html. [Accessed 02 Feb 2023]. 
[32] | Raspberry Pi Ltd, “Raspberry Pi Pico Datasheet - An RP2040-base microcontroller board,” 09 06 2022. [Online]. Available: https://datasheets.raspberrypi.com/pico/pico-datasheet.pdf. [Accessed 02 Feb 2023]. 
[33] | P. S. a. c. Damien P. George, “SSD1306 driver,” 01 Feb 2023. [Online]. Available: https://docs.micropython.org/en/latest/esp8266/quickref.html#ssd1306-driver. [Accessed 2 Feb 2023]. 
[34] | P. S. a. c. Damien P. George, “framebuf - frame buffer manipulation,” The MicroPython Documentation, 01 Feb 2023. [Online]. Available: https://docs.micropython.org/en/latest/library/framebuf.html. [Accessed 02 Feb 2023]. 
[35] | “Raspberry Pi Pico W datasheet,” Raspberry Pi Ltd, 30 Nov 2022. [Online]. Available: https://datasheets.raspberrypi.com/picow/pico-w-datasheet.pdf. [Accessed 02 Feb 2023]. 
[36] | Admin, “Getting Started with Raspberry Pi Pico W using MicroPython,” How to Electronics, 12 Jan 2023. [Online]. Available: https://how2electronics.com/getting-started-with-raspberry-pi-pico-w-using-micropython/. [Accessed 02 Feb 2023]. 
[37] | “Token endpoint,” Amaxon Web Services, Inc., 2023. [Online]. Available: https://docs.aws.amazon.com/cognito/latest/developerguide/token-endpoint.html. [Accessed 02 Feb 2023]. 
