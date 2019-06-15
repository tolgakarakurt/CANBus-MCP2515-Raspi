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

1. > <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/1.jpeg" width="150">  MCP2515 CANBus Module  
2. > <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/2.jpeg" width="150">  Find the Vcc trace for TJA1050  
3. > <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/3.jpeg" width="150">  Cut the copper trace to replace with 5V  
4. > <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/4.jpeg" width="150">  Scrape the insulator to make soldering over the trace.  
5. > <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/6.jpeg" width="150">  Solder the jumper wire  
6. > <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/7.jpeg" width="150">  Put some silicon to strength the connection  
7. > <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/8.jpeg" width="150">  I preferably replace the 7 pin male headers with 8 pin Male PCB Mounting Right Angle connector  
8. > <img src="https://github.com/tolgakarakurt/CANBus-MCP2515-Raspi/blob/master/9.jpeg" width="150">  Overall board with modification  

## Installation
>>ss
>>f

    
  
  

## Learn More  
**RaspberryPi 3 Model B+**     
> https://en.wikipedia.org/wiki/Raspberry_Pi    
> https://pinout.xyz/  

**MCP2515 Can Controller** 
> https://www.microchip.com/wwwproducts/en/en010406  
> http://ww1.microchip.com/downloads/en/DeviceDoc/MCP2515-Stand-Alone-CAN-Controller-with-SPI-20001801J.pdf  
> https://www.nxp.com/docs/en/data-sheet/TJA1050.pdf  

