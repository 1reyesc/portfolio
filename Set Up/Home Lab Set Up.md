# Over view of Home Lab
## List of VM's
- ### Wazuh OVA
  - Currently, my home lab consists of several different virtual machines running some common softwares in a SOC. My first VM is a Wazuh OVA this my SIEM that I am currently using to
ingest event data from my agent. 

<img src="https://github.com/user-attachments/assets/30ae1ddc-3804-45fb-8042-4044ba34429a">

- ### Ubuntu Agent
  - For my agent I currently am running a Ubuntu 22.04 LTS VM this contains Suricata as an extra layer of defense to get a more in-depth look at my network traffic. This helps with visualizng the events
that took place on my agent easier with the attacks that I am running on it. Suricata can also employ preventative measures in the case of an attack.

<img src="https://github.com/user-attachments/assets/ebb23e54-af53-4bd1-b1f1-3794c147e472">


- ### Kali Linux
  - As my attacker machine I'm utilizing a kali linux VM. Kali Linux comes pre-loaded with a ton of pen testing tools that I am taking advantage of to carry out attacks in all phases
    of the attacker kill chain.


