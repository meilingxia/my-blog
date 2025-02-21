# OSI Model layers
![image](https://github.com/user-attachments/assets/888851e2-a3ad-4c56-91c8-e276744fc990)

## How data is transmit in Physical Layer
Assuming devices are connected via network cables, ***electrical signals*** transmit data in binary (***1*** and ***0***) over the cables.
#### What is Electrical Signals
It refers to voltage changes or current changes, which represents binary data (1 and 0) and enables digital communication.
#### Binary Representation
1. Computers and digital devices can only understand binary (***1*** and ***0***).
2. These binary bits (bit) are represented using electrical signals.
#### How Do Electrical Signals Represent ***1*** and ***0***
1. ***High voltage*** (e.g., +5V) → Represents binary "***1***"
2. ***Low voltage***  (e.g., 0V)  → Represents binary "***0***"
#### Examples of Electrical Signals in Network Communication
Wired networks (e.g., Ethernet, fiber optics): Use electrical signals or optical signals to transmit data.
#### Why Use Electrical Signals?
Electrical signals allow fast transmission and can be easily processed and converted by computers.
#### Wireless transmit
1. Wireless networks (e.g., Wi-Fi, Bluetooth): Use radio waves to represent binary data.
2. In 5G networks, communication between the base station and your phone is still fundamentally binary (***1*** and ***0***) transmission, but the form of the signal is different.
 
#### How a Base Station Communicates with a Mobile Phone
Although data is ultimately binary, 5G networks use radio waves (electromagnetic waves) for transmission instead of directly representing ***1*** and ***0*** with high or low voltage.
#### Wireless Transmission of Digital Signals
1. The phone and the 5G base station communicate using radio waves.
2. Radio waves are analog signals (continuously varying waveforms).
3. ***1*** and ***0*** will be converted into different radio waveforms so they can be transmitted through the air.
#### Transmission and Reception Process
1. Phone sends data: The phone converts binary data into a modulated wireless signal and transmits it to the 5G base station via the antenna.
2. Base station receives data: The base station's antenna captures the wireless signal and demodulates it back into binary data before transmitting it to the internet via fiber optics or other transmission methods.
3. Data returns to the phone: Once the server responds with data, the base station converts the binary data back into a wireless signal and sends it to your phone, which then demodulates it into readable information (such as web pages or videos).
 
#### Summary
1. Nature of Data: Still ***1*** and ***0*** (binary).
2. Transmission Method: Binary is first converted into a wireless signal and then transmitted via radio waves.
3. Decoding Process: The receiving end (phone or base station) converts the wireless signal back into binary data for use by the device.

## The Data Link Layer
### Main Functions of the Data Link Layer
#### Physical Addressing
1. When data is transmitted from the Network Layer, the packet contains the IP address of the destination device.
2. The Data Link Layer adds the ***MAC*** address (Media Access Control) of the receiving device to ensure the data is correctly delivered to the specific device.
#### MAC Address
1. Every network-enabled device has a Network Interface Card (***NIC***) <--->***MAC*** address.
2. MAC addresses are assigned by the manufacturer and burned into the network card, meaning they cannot be changed. However, they can be spoofed (***MAC Spoofing***).
3. When data is transmitted across a network, it is actually the ***MAC*** address, not the IP address, that determines where the data should be sent.
#### Data Framing
Besides addressing, the Data Link Layer is also responsible for formatting data into a suitable structure for transmission over the physical medium.

#### Example of Data Transmission Process
Suppose  computer (A) wants to send data to another computer (B): A-->B
1.	The Network Layer of A generates a data packet that includes B’s IP address.
2.	The Data Link Layer of A checks for B’s MAC address (if unknown, it will be resolved through ***ARP***).
3.	The Data Link Layer of A combines the MAC address, IP address, and data into a frame and transmits it via the Physical Layer.
4.	The Data Link Layer of B receives the frame and checks whether the MAC address matches its own network card.
5.	If the MAC address matches, the Data Link Layer of B forwards the data to the upper layer (e.g., the Network Layer).
#### Conclusion
The Data Link Layer is primarily responsible for device identification through ***MAC*** addresses and ensuring data is correctly delivered to the receiving device. Additionally, it formats data for proper transmission over the network.



*The content of this blog is based on my learning experience on TryHackMe. 
I am a paid member of TryHackme and I use ChatGPT to help me understand the relevant knowledge. 
All articles are based on my personal study summaries and are not direct copies of TryHackMe's official contents.
Instead, these blogs reflect my understanding and organization of the courses.*

*本博客的内容来源于我在 TryHackMe 上的学习经验，我是其付费会员，并使用 ChatGPT 来帮助理解相关知识。
所有文章均基于我个人的学习总结，并非直接复制 TryHackMe 的官方内容，而是我对课程的理解和整理。*
