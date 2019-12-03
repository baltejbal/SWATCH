# SWATCH
Implementing the Heartrate portion of a SmartWatch IOT project using the Adafruit Pulse Sensor and a Raspberry Pi 3 
# Build Instructions for using Pulse Rate Sensor on a Raspberry Pi 3B+
#### By Baltej Bal • For Hardware Production Technology CENG 317, Humber College School of Applied Technology

## Table of Contents
1. [Introduction](#Introduction)
2. [System Diagram](#System-Diagram)
3. [BOM/Budget](#Bill-of-Materials-and-Budget)
4. [Build Materials](#Build-Materials)
5. [Time Commitment](#Time-Commitment)
6. [PCB/Soldering](#pcb-design-files)

<br />

# Introduction
This project is to implement the Adafruit Pulse Sensor into a development platform. The Pulse Sensor is soldered on to a custom-designed PCB to allow for plug-and-play functionality with the Raspberry Pi 3 development platform. Firmware was written to interface with the connected sensor, and an enclosure was designed to hold the Pi and sensor assembly. 

The Pulse Sensor is a well-designed plug-and-play heart-rate sensor for Arduino with both I2C and SPI interfaces. It was chosen due intrests in the smartwatch project and it already exists in the modern day smartwatch's.  It can also be used by many who want to easily incorporate live heart rate data into their projects. It also includes an open-source monitoring app that graphs your pulse in real time. The Raspberry Pi 3 is an ARM-based 64-bit single board computer with a large developer community and support - a perfect development platform for integrating multiple sensors into a final working product.

Once complete, this project can be integrated alongside other sensors to provide more complex functionality and handle more applications. This project in particular is part of a multi-semester group project to integrate an accelerometer, pulse sensor and a temperature sensor alongside an appropriate enclosure and development platform in order to create a smartwatch device.

![sen-11574](https://cdn.shopify.com/s/files/1/0915/1182/products/11574-01_2048x.jpg?v=1473879996)
<br/>
(source of Image : https://elmwoodelectronics.ca/products/11574?variant=28163190211)

<br/>
You can buy Raspberry Pie from [here]( https://www.raspberrypi.org/products/raspberry-pi-3-model-b-plus/)
and  the sen-11574 pulse rate sensor from [here]( https://elmwoodelectronics.ca/products/11574?variant=28163190211).
<br/>
<br/>

# System Diagram
Image of prodect
<br/>

# Bill of Materials/Budget
A full list of materials along with a detailed view of costs can be downloaded form within this repository.[budget.docx](https://github.com/baltejbal/SWATCH/blob/master/budget.xlsx)<br/>
<br/>
The total cost of producing this project is heavily inflated due to the cost of the soldering kit that was supplied in the lab during
development. Any generic solding iron can be used for this project.</br>
<br/>
The total cost after removing the soldering kit is: **$ 129.51 CAD** after HST. This includes all the tools used in completing the project (eg. wirecutters, needlenose pliers, breadboard, etc.)</br>

Notable purchases include: Raspberry Pi 3B+ Kit ($74.29 CAD) and Sen-11574 Pulse Rate Sensor ($23.28 CAD).
</br>

# Time Commitment
This project was compleated over a 15 week semester with an average weekly time commitment of 165 minutes a week. Some tasks require extra work outside of class, such as soldering and troubshooting. 

Assuming that all parts of the project have been acquired this project should take roughly a weekend to complete. The materials themselves might take a day or two to arrive depending on the shipping method. The actual proccess of assembling and programming should not take longer than 3 days. A couple of hours each day can be dedicated towards the different aspects of the project to make time usuage more efficient and effective. Here is the time schedule I followed:</br>
[Time-Schedule](https://github.com/baltejbal/SWATCH/blob/master/ProjectTimeLine.mpp)<br>

## Mechanical Assembly
*Step 1: Preparing your development platform*
This step will outline how to prepare the project's development platform - the Raspberry Pi 3B+.

  1. Download the latest [Raspberry Pi image](https://www.raspberrypi.org/downloads/). NOOBS is recommended, as it includes the latest Raspbian operating system, a variety of useful software tools pre-installed, and a selection of alternate operating systems.
  
  2. Prepare your microSD card. Plug the card into any computer, and unzip the downloaded file to an easily-accessible folder on your computer, copy the unzipped files to the inserted microSD card. Once complete, unmount or safely eject the card.
  
  3. Insert the prepared microSD card into the port located on the bottom-side of the Pi. Insert a keyboard, mouse, HDMI cable and Ethernet cable into the Pi. Ensure the HDMI cable is connected to a functioning display, and then plug in the micro-usb power adapter to power on the Rpi.
  
  4. Upon booting, a splash screen with a variety of operating system options will appear. Select **Raspbian** and follow the on-screen prompts to configure your installation. The install process should take a few minutes. Once complete, the Pi will automatically restart to the the Desktop screen.
  
  5. Configure more connectivity options to your Pi. Open the *terminal* application, and enter `sudo raspi-config`. Navigate to *Interfacing options* and enable both **VNC** and **SPI**. VNC will allow for remote graphical connections to the Pi, and the MCP3008 uses SPI.
  
  6. Install required software tools and libraries. The ADC uses the **SpiDev** library, which must be installed. [Downloading SpiDev](https://github.com/baltejbal/PICS/blob/master/SpiDev_Doc.pdf).
  
  7. Collect information for remote access. Once connected to the internet, open the terminal and enter `ifconfig`. Make a note of the value found next to *inet* underneath the *eth0* heading. This is the Pi's IP address, and will be used to connect to the Pi from another computer. It can change, but rarely does assuming network conditions remain consistent.
  
  8. From another computer, open any remote-connection app. On a Windows computer, the *Remote Desktop Connection* application can be used. Alternatively, RealVNC's *[VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/)* can be used on any platform, and is generally the most reliable means of connecting.
  Enter the IP address you noted above. The application will prompt you for a username and password - the Pi's default username is `pi` and the default password is `raspberry`. Enter these credentials, and the Pi's graphical interface should appear on the computer you are using. You are now controlling the Pi remotely!
  
  9. At this stage, all the software required for the development platform has been installed and configured. The Pi can be shutdown using the menu bar option, or by entering `sudo powerdown` into the terminal. Once the Pi is off, all the cables can be unplugged and the Pi set aside until later.
  
*Step 2: Breadboarding and Prototyping*

This step will outline basic sensor connectivity using jumper wires and a breadboard. The design and layout established in this step will carry over to PCB design and soldering.

  1. Gather the following items: Breadboard, Pulse Sensor, MCP3008 Adc and many Female-to-Male cables. 
  
  2. Identify the correct pins on the sensor. For the sensor and the ADC.
  
  ![](https://github.com/baltejbal/PICS/blob/master/PULSE%20SENSOR_bb.png)
  
  3. Identify the corresponding pins on your development platforms GPIO header. 
  
  4. Line the sensor up with holes on the main part of the breadboard, and insert the male-end of the jumper cables into the pins previously identified. Insert the female end of each cable into the matching GPIO pin on the Raspberry Pi. 
  
  5. When your physical connections are secured, plug in your peripherals into the Raspberry Pi and power it on.
  
  6. Following the directions established above, create a remote desktop connection to the Pi. Use the ip address that you noted when preparing your platform initially - the login credentials should be the same.
  
 7. At this point, breadboard prototyping is complete, It is time to move on the designing and soldering a plug-and-play PCB.


# PCB/Soldering
<br/>

PCB design and soldering is the most crucial step to this project. PCB cutting is a time-consuming and costly process, and any errors in design will most likely require your board to be re-printed. Anyhow, it is heavily advised to ensure that your design is correct prior to any cutting being done. 

**Step 1: Fritzing**
The appilcation Fritzing is required along with the MCP3008-8-Channel 10-Bit ADC file which must be added to the application. The file can be downloaded <a href = "https://github.com/baltejbal/SWATCH/blob/master/PULSE%20SENSOR.fzz">Here</a>

Create the appropriate connections, ensuring that any traces do not cross. Try to get your board to be as compact as possible. Alternatively, you can use my fritzing file found [here](https://github.com/baltejbal/PICS/blob/master/PULSE%20SENSOR_bb.png).
  
Export as a Gerber file. `File > Export for Production > Extended Gerber` and select an easily-accessible folder. These files are the standard filetype used to etch and cut physical PCBs.
  
Compress the Gerber files, and send them to your etcher of choice. I used the school prototype lab provided. 

**Step 2: Soldering**
<br/>
Once the PCB has been created, it's time to solder. Ensure that you work in a well-ventilated area, wearing safety glasses and using an iron that you are comfortable with.
 
  1. Gather your sensor and ADC, a length of copper wire, a wire stripper, a 10-pin double-sided header (does not come with your sensor), a 40-pin stackable header, your PCB, solder and a soldering iron.
  
  2. Solder the 10-pin header to the sensor board. To make this easier, you can place the extended pins into a breadboard, and place the sensor on the shorter pins. This ensures a sturdy connection.
    
  3. Solder the vias on your PCB. The easiest method for this is to strip a copper wire, and place it through the via into a breadboard. Solder all vias on the exposed side, and then flip and repeat for the opposite side.
  
  4. Solder the sensor to the PCB. You will need to rest the PCB on a flat surface for this, as there is no way to access the extended pins while they are mounted. 
  
  5. Solder the stackable header on to the PCB. All 40 should be soldered to ensure stability when attached to the Pi.
  
  ![](https://github.com/baltejbal/PICS/blob/master/pcbdes.jpeg)
  
  At this point, soldering is complete. Attach your soldered board to the appropriate GPIO pins on the Pi, and get ready for further testing.

<br/>

# Power Up
With all peripherals plugged into your Pi, power it on. As above, establish a remote desktop connection, using a multi-meter check if you are recieving power to the chip and make sure the heartrate sensor is on.

# Unit Testing
All testing so far has been to verify that the sensor is in working condition, and that there is a valid connection to the Pi. Further testing needs to be done - particularly in verifying that the heartrate values can be read off the sensor and displayed in real-time.

  1. Download the python file found [here](https://github.com/tutRPi/Raspberry-Pi-Heartbeat-Pulse-Sensor).
  
  2. Open a terminal, and navigate to your home directory using `cd ~`. 
  
  3. Run the script by entering `python example.py`. It will prompt you a no heartbeat found, once you place you finger on the heartrate sensor it will measure your heartrate and display a BPM.
  
When you run the program you should end up with a screen that looks like this.![](https://github.com/baltejbal/PICS/blob/master/working.jpeg)
  








