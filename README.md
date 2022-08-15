# Communication-Subsystem-for-cubesat

COMMUNICATION SUBSYSTEM INITIAL PROPOSAL REPORT  
 
 
 
Objective :- To explain the communication Subsystem for the CubeSat. 
 
Modulation Scheme: 
The main communication channel used by the satellite is its LoRa radio, with the following configuration:  
•	Carrier frequency 436.7 MHz  
•	Bandwidth 125 kHz 
•	Spreading factor 11  
•	Coding rate 4/8  
•	Sync word 0x0F0F 
 
 
Terminology : 
Spreading factor : 
 The spreading factor defines the relation between symbol rate and chip rate. A higher spreading factor increases sensitivity and range, but also prolongs the airtime of a packet and will likely raise the risk of a collision. LoRaWAN uses six different orthogonal spreading factors numbered 7– 12. 
 
 
Coding Rate :  
The code rate can be defined as the ratio of the data rate that is allocated for a subframe and the maximum data rate that ideally can be allocated in the subframe. 
Or simply the ratio of number of message hits to the total number of bits in a word. 
 
Sync Word : 
The syncword is a known sequence of data used to identify the start of a frame and is also called reference signal in wireless communications. 
In general, exchanges with the satellite can occur on either automatic, or manual basis. Automatic frames are sent by the satellite based on fixed transmission period, and consist of system information, such as battery voltage, temperatures, solar cell voltages, etc.These frames are sent via LoRa modulation each 30 seconds. In addition, system frame is also transmitted via RTTY every 3 minutes with the following configuration:  
•	Carrier frequency 436.7 MHz  
•	Frequency shift 182 Hz  
•	Baud rate 45 baud  
•	Encoding ITA2 (5-bit, aka “Baudot code”)  
•	Single stop bit, no parity 
In RTTY mode, system information is sent as ASCII-encoded hexadecimal numbers, so that every 2 hexadecimal numbers give a single byte. The format of LoRa and RTTY system info frame is identical. Manual exchanges with the satellite are initiated by the ground station and are replied to by the satellite. Because the satellite uses multiple different modulations and contains a single radio module, only single communication channel is active at any given point: the satellite listens for incoming LoRa transmissions for 5 seconds out of any given 9-second period. It should be noted that the satellite contains safety precautions that may prevent it from responding under certain conditions. In addition, some on-board actions have higher priority than responding to incoming frames. Because of this, it cannot be guaranteed that every frame sent will induce a response. 
 
 
Hardware / Software decided to use : 
We are going to implement our CubeSat on Lora Radio Module and choosing best among the modules like SX1272,SX1276 by observing the specification could be a wise decision and also other available and compatible LoRa modules like RFM96xx are also being investigated. 
 
Specifications 	SX1272 	SX1276:
		
Frequency bands of operation 	850 MHz to 1 GHz 	169 MHz, 433 MHz, 
850 MHz to 1 GHz 
Programmable Bandwidth 	125 KHz , 250 
KHz, 500 KHz 	7.8 KHz, 10.4 KHz, 
15.6 KHz, 20.8 KHz, 
31.2 KHz, 41.7 KHz, 
62.5 KHz. 125 KHz, 
250 KHz, 500 KHz 
Receiver Sensitivity 	Good (down up to 137dBm) 	Better than SX1272, 
(down up to -148 dBm) 
Max. Link Budget 	157 dB 	168 dB 
IIP3 	-12.5 dBm 	-11 dBm 
Rx current 	10 mA, 100nA 
register retention 	9.9 mA, 200nA register retention 
Modulation types supported 	GFSK, FSK, MSK, 
GMSK, LoRa™ as well as OOK. 	Same as SX1272 
Dynamic Range (RSSI) 	127 dB 	127 dB 
Temperature sensor and low battery indication 	YES 	YES 
packet engine size 	256 bytes 	256 bytes 
Blocking Immunity 	89 dB 	Excellent 
Bit Synchronizer 	YES 	YES 
Preamble detection 	YES 	YES 
 
SPI is used as the hardware interface between the LoRa radio and the microcontroller. In addition, DIO0 and DIO1 pins must be connected. On SX126x, the BUSY pin must also be connected to the MCU. 
 
 
Software : We could be using a Arduino IDE to receive and decode the frames. Additionally we could import the libraries of Lora Modules and our custom defined communication receiving/transmitting communication protocols. 
RadioLib is used as the driver for LoRa radio modules, whereas libraries with communication protocol that are yet to be custom configured once the implementation of CubeSat starts. Both libraries contain ready to-use examples on both LoRa radio control (in RadioLib), as well as sending and receiving various frames. 
 
Communication Protocols:
Cubesat’s communication subsystem implements simple frame-based communication protocol using LoRa modem. This protocol allows ground stations to perform basic actions with the satellite, for example fetch current status, send ping/pong exchanges or request retransmission of a message. 
The proposed Frame structure for the communication protocol is  
 
  
Terminology : 
Callsign : String of printable ASCII characters, sent as the first field of each frame.  Data Into Data Base  
Finally it is expected to upload the received or sent data  from the Cubesat is uploaded into a data base by creating one for future references or studies. 
 
