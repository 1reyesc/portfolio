# Designing a Secure Network Topology


## Introduction
In this lab, we will cover a fundamental concept that every great Network Security (NetSec) engineer should understand: **Defense-in-Depth**. With this concept in mind, we will create a network topology using **GNS3**. Using GNS3, we will capture the traffic between devices and perform **packet sniffing** to validate network connectivity.

---



## Design a Simple Network Topology

### Network Topology 
<img src="https://github.com/user-attachments/assets/ac38ee8c-cd22-47f0-b64f-6ce397fe19c7">  

**Use GNS3 to build a simple network.**  
- Once PC1 - PC4 are configure correctly we can use the terminal to test connectivity between the 2 PC's in each subnet

- **Ping result from PC4 to PC3**
<img src="https://github.com/user-attachments/assets/9ee8df5c-6177-415e-8663-9ec574df81f8">  

- **Ping results from PC2 to the vWorkstation**  
<img src="https://github.com/user-attachments/assets/5bbe421e-6001-47e7-ae46-aa0427e87b82">

  
- Now that I've correctly configured PC1 - PC4 I want to add two switches to be able to ping host's in different subnets. At this stage, I'll configure both **Switch 1** and **Switch 2**.

<img src="https://github.com/user-attachments/assets/f8e6c644-57fc-46a3-98c5-92f096c0373c">

- Now that both switches are configured I can ping PC1 from PC4 to test subnet connectivity.

---

## Task 2: Capture Network Traffic to Validate Connectivity  
**Use Wireshark to capture packets between LANs.**  

<img src="https://github.com/user-attachments/assets/da957d2f-ae39-4c44-b2ed-b5f39d81ecfc">

- **Packets between ICMP echo of PC2 to PC3**

<img src="https://github.com/user-attachments/assets/93b449b9-a2cd-48bc-9708-648d83fc08a1">

- **Wireshark capture between PC3 and vWorkstation** 

---
## Task 3: Design a More Complex Network Topology
- **Now that we have all of our IOT's setup we can create a more complex network topology by configuring our Interfaces.**

<img src="https://github.com/user-attachments/assets/e35daef7-2067-461b-839e-29b984d82b36">  

   - **Interface assignments page**
<img src="https://github.com/user-attachments/assets/d1f488ed-98ac-40da-8d54-223bfa41125c">  

   - **VLAN settings updated**
<img src="https://github.com/user-attachments/assets/052da270-1964-476d-a436-90d500d95f9d">
   - **Updated settings for both VLANs**
---

## Task 5: Enhance the Network Topology with a DMZ  
**Know that we have our LAN interfaces and our switches configured. We can make a router and configure our WAN to create a DMZ or a outward facing interface. Our pfSense router also acts as a firewall.**

<img src="https://github.com/user-attachments/assets/acbb992d-0832-4a6e-a9a8-2fae54a0f1b8">
- Interface configurations in the **pfSense** console

<img src="https://github.com/user-attachments/assets/e36bf2a2-45da-4b50-a93e-bfb560ee0968">
- **WAN configurations to route all IPv4 traffic to the DMZ**  
---

## Task 6: Validate DMZ Connectivity  
**Finally, we can create two virutal PC's that are on the outside of our network and have them ping an inside VPC to test connectivity between external and internal hosts. We can have these hosts connected directly to the pfSense router to test our DMZ.**  


<img src="https://github.com/user-attachments/assets/44563af2-238d-477e-8b01-fa84e0754691">  

- **Successful and unsuccessful ping from WAN host and LAN host**

---

## Discussion and Conclusion  
This lab was **challenging** at times, and I still feel a bit **uncertain** about some of the configurations, especially with setting up the **DMZ**. However, I believe I gained valuable **knowledge** in understanding how **networks function** and how to **reverse engineer** them. This is a **critical skill** for a security analyst, and I hope to improve my understanding through further practice.


