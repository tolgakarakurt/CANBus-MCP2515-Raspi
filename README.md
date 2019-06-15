# MCP2515 CANBus module installation on RaspberryPi  
It is aimed to build CANBus communication between two Raspberry Pi boards. This setup is accomplished with the Microchip's stand-alone MCP2515 CAN controller. 

## Project Items  
> 1 RaspberryPi 3 Model B+ (Raspi1)   
> 1 RaspberryPi 3 Model B v1.2 (Raspi2)   
> 2 MCP2515 CAN Bus Module TJA1050 Receiver SPI (CanModule1, CanModule2)    
> Environmental Setup     

## High Level Design 
Raspi1 --(SPIcomm)-- CanModule1 ==<CANbus H,L>== CanModule2 --(SPIComm)-- Raspi2
![Test Image 1](https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/CANBus-2MCP2515-Page-1.png)

## Wiring Diagrams
**MCP2515**
![Test Image 2](https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/CANBus-MCP2515-MCP2515%20Schematic.png)
**Note:** Modification is required! Since TJA1050 CAN Transciver operates at 4.75V~5.25V (Typically @5V), it is necessary to add Vdd 5V input pin to the module besides Vcc 3.3V. It is explained how the MCP2515 CAN module is adjusted below along with the pictures.  

> <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/1.jpeg" width="150">  1.MCP2515 CANBus Module  
> <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/2.jpeg" width="150">  2.Find the Vcc trace for TJA1050  
> <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/3.jpeg" width="150">  3.Cut the copper trace to replace with 5V  
> <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/4.jpeg" width="150">  4.Scrape the insulator to make soldering over the trace.  
> <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/6.jpeg" width="150">  5.Solder the jumper wire  
> <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/7.jpeg" width="150">  6.Put some silicon to strength the connection  
> <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/8.jpeg" width="150">  7.I preferably replace the 7 pin male headers with 8 pin Male PCB Mounting Right Angle connector  
> <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/9.jpeg" width="150">  8.Overall board with modification  

## Installation
**Download Updates:**  
> sudo apt-get update  
> sudo apt-get upgrade  
> sudo reboot  

**Enable SPI:**  
Applications Menu --> Preferences --> Raspberry Pi Configuration --> Interfaces --> Select SPI Enabled  
OR
> sudo raspi-config  

5 Interfacing Options --> P4 SPI --> Yes --> The SPI interface is enabled --> Finish  

**Check Kernel version:**  
> uname -a

Linux raspberrypi 4.19.42-v7+ 1219 SMP Tue May 14 21:20:58 BST 2019 armv71 GNU/Linux  

**Modify config.txt:**  
For later kernels (4.4.x onwards)

> sudo nano /boot/config.txt  

Add the following setup at the end of the file:

dtparam=spi=on
dtoverlay=mcp2515-can0,oscillator=8000000,interrupt=25  
dtoverlay=spi-bcm2835  
dtoverlay=spi-dma  
<img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/config_txt.jpeg" width="550">  
<img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/gpioreadall.jpeg" width="550">

Save: CTRL + X --> Enter  
> sudo reboot  

**Install Can-utils:**
> sudo apt-get install autoconf autogen  
> sudo apt-get install libtool  
> git clone https://github.com/linux-can/can-utils.git  
> cd can-utils  
> ./autogen.sh  
> ./configure  
> make  
> make install (with root privileges)  
> sudo apt-get install can-utils
> sudo reboot  

**can0 Availability Check**  
Full circuit wiring must be completed before checking the related folder. And do not miss having common ground, since there is not any additional GND pin for Can transmission lines (CAN_H, CAN_L). 

sys --> bus --> spi --> devices --> spi0.0 --> net --> can0  
OR
> ls /sys/bus/spi/devices/spi0.0/net  

<img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/ls_can0.jpeg" width="550">  

**Test: Sending data from RasPi1 to RasPi2**  

RasPi1
> sudo ip link set can0 up type can bitrate 500000  

> cansend can0 100#12FF34AA56DD66  

<img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/RasPi1_cansend.jpeg" width="550">  

Raspi2   
> sudo ip link set can0 up type can bitrate 500000  
 
>candump can0  

<img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/RasPi2_candump.jpeg" width="550">  

## Learn More  
**RaspberryPi 3 Model B+**     
> https://en.wikipedia.org/wiki/Raspberry_Pi    
> https://pinout.xyz/  

**MCP2515 Can Controller** 
> https://www.microchip.com/wwwproducts/en/en010406  
> http://ww1.microchip.com/downloads/en/DeviceDoc/MCP2515-Stand-Alone-CAN-Controller-with-SPI-20001801J.pdf  
> https://www.nxp.com/docs/en/data-sheet/TJA1050.pdf  

