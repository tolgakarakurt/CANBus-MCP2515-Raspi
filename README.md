# CANBus-MCP2515-Raspi
MCP2515 CANBus module installation on RaspberryPi

## Project Items  
1 RaspberryPi 3 Model B+ (Raspi1)   
1 RaspberryPi 3 Model B v1.2 (Raspi2)   
2 MCP2515 CAN Bus Module TJA1050 Receiver SPI (CanModule1, CanModule2)    
Environmental Setup     

## High Level Design 
Raspi1 --<SPIcomm>-- CanModule1 ==<CANbus H,L>== CanModule2 --<SPIComm>-- Raspi2
