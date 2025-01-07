# Packetsniffing using Wireshark
In this lab, I used Wireshark to sniff out log in credentials and files inside of a TCP stream. The purpose of this lab was to show the importance of using a secure protocols and display the issues that can arise when using unsecure
protocols.
## Telnet vs SSH
- First, I established a Telnet shell between my Kali Linux VM and Metasploit VM
![Telnet Shell](https://github.com/user-attachments/assets/599f3025-be32-441c-9c35-43418ae01215)
- Once I had my shell established I began capturing packets on my ETH0 inside Kali Linux then logging into msfadmin on the Metasploit VM
- I stopped the packet capturing and filtered the captured packets for Telnet. Finding the packets that were associated with my login I followed the TCP stream.  
![TCP Stream](https://github.com/user-attachments/assets/02a0e70d-d5ab-44df-911b-2696d0194251)
- As you can see, I successfully sniffed out the login credentails.
- Similarly, I followed all the same steps with SSH, but once I found the stream associated with my login. There were no full identifying login credentials.
## HTTP vs HTTPS
- Once clearing previously used packets, I began capturing again on my ETH0 Network Adapter.
- I used my web browser to navigate to a website with a login that was using HTTP.
- I logged in using a bogus login and stopped my packet capturing and found the associated TCP Stream.
![HTTP Stream](https://github.com/user-attachments/assets/8852a4f0-b2fd-40ec-bca7-fb64f71ec047)
- The exact same thing was preformed for HTTPS Stream.  
![HTTPS Stream](https://github.com/user-attachments/assets/96338e3f-afb8-4ad6-8b7d-86b347bbb372)
## File Snatching
- With this I established a FTP connection with my Metasploit VM.
- Once connected I downloaded a file from the VM and captured these packets during the download.
![FTP TCP Stream](https://github.com/user-attachments/assets/f85f9797-4f7d-44eb-8699-f74ecab089aa)
- With the TCP stream captured. I used third-party software to replicate the file I just downloaded showcasing how a attacker could steal files.  
![File replicated](https://github.com/user-attachments/assets/47d41385-9e6c-4dc3-887b-d2a3300a6433)
# Conclusion
I demonstrated in this lab ways that potential attackers could steal/replicate files and login credentials that are transmitted through protocols during the use of the internet. The importance of secure protocols is very heavily emphasized in this showcasing that encryption is a major component in keeping sensitive data safe.






