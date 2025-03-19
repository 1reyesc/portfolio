# Mr.Robot VM Lab Report

## Introduction
In this lab, we are going to find 3 flags that are hidden inside a pre-built exploitable VM called the Mr.Robot VM. This VM is inspired by the popular show *Mr. Robot*. We will find the three flags and explain the exploits used.

## Task 1: Information Gathering
- First, we need to determine the IP address of the Mr.Robot VM by running a quick network scan.
  - After the **Nmap** scan completes, we can identify the Mr.Robot VM and gather information about its open ports.
    - **Port 22 (SSH)** is closed, preventing us from using SSH.
    - **Ports 80 (HTTP) and 443 (HTTPS)** are open, which could be valuable for exploitation.
 <img src="https://github.com/user-attachments/assets/b88acf32-5bfa-45fd-adde-abfb8fe62bc0">





 <img src="https://github.com/user-attachments/assets/40080d63-9571-4c98-9305-9e37f9b9a9af">  
 
- We then open a browser and navigate to the Mr.Robot VM IP address to have the webpage displayed.  


- Using **Nmap**, we perform **website directory enumeration** to uncover additional resources.
  - Several directories appear, and we begin probing for useful information.

 <img src="https://github.com/user-attachments/assets/fd3872bb-9bba-4cd0-b093-d4232ce9d574">  

  - The **robots.txt** file contains a reference to `key-1-of-3.txt`.
  - Navigating to this file reveals **the first key**.

<img src="https://github.com/user-attachments/assets/c3b71f40-b7c3-4ded-a5b6-dca06cee2375">
<img src="https://github.com/user-attachments/assets/84f9ec6f-f844-45be-bdcb-2083e2f32def">





## Task 2: Break Through WordPress Login
- Returning to the WordPress login page, we inspect the site to find the variable names used for login credentials (`log` and `pwd`).
- Using **Hydra**, we attempt to brute-force valid usernames:
  - This initial brute-force run helps identify correct usernames by testing with a placeholder password.
    - "hydra -L /home/kali/Desktop/fscoity -p test 'IPADDRESS' http-form-post "/wp-login.php:log=^USER^&pwd=^PASS^:Invalid"
  - Once a valid username is found, we modify the Hydra command to brute-force passwords for that username.
  - **Successful login achieved!**

<img src="https://github.com/user-attachments/assets/d2b07654-6914-45d6-936d-a613ad72c1e4">


## Task 3: Leverage Admin Account
- With administrator access, we create a **reverse shell** inside the website.
- Using **Metasploit**, we deploy the `wp_admin_shell_upload` module to exploit the WordPress page.

<img src="https://github.com/user-attachments/assets/e8ad67bf-f827-47ca-9d13-aca5af89d440">



- We navigate to the `/home/robot/` directory and find **the second key**, along with a file named `password.raw-md5`.

<img src="https://github.com/user-attachments/assets/7b2b84f5-4049-422b-98af-28d46e19645f">


  - The file contains a username and a hashed password.
    - "hashcat -O -m 0 -a 0 hash.txt"
    - This command will run hashcat with the loaded hash inside hash.txt in testing a hash type MD5 and brute forcing it.
  - We use **Hashcat** to crack the hash, revealing the password: `abcdefghijklmnopqrstuvwxyz`.

  - With this password, we attempt to escalate privileges by creating a Python shell inside our **Meterpreter** session.
  - However, this does not grant root access
- We check for binaries with **root privileges** and discover that **Nmap** is owned by root.
  - Since **Nmap** has an interactive mode, we exploit it to obtain **root access**.

<img src="https://github.com/user-attachments/assets/9990f7d0-0aa9-4a56-a472-f4f52f17aedd">

- With root access, we locate **the third and final key**, successfully completing the challenge!

<img src="https://github.com/user-attachments/assets/129e7e86-3ecd-467e-bb26-1c106c49aa84">

## Discussion and Conclusion
In this lab, we used several tools to exploit vulnerabilities in the Mr.Robot VM, including:

- **Nmap** - A network scanning tool used to identify the Mr.Robot VM's IP address and enumerate website directories.
- **Hydra** - A password-cracking tool used to brute-force valid login credentials.
- **Metasploit (MSF)** - A penetration testing framework used to exploit the WordPress login page with the `wp_admin_shell_upload` module, granting access to the system.

By successfully finding all three flags, we gained hands-on experience in:
- Network scanning and reconnaissance.
- Brute-force attacks on login credentials.
- Privilege escalation techniques.
- Exploiting known vulnerabilities in web applications.

This lab provided valuable insight into real-world penetration testing methodologies and reinforced the importance of securing systems against common exploits.
