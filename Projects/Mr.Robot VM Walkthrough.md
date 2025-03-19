# Mr.Robot VM Lab Report

## Introduction
In this lab, we are going to find 3 flags that are hidden inside a pre-built exploitable VM called the Mr.Robot VM. This VM is inspired by the popular show *Mr. Robot*. Using a walkthrough, we will find the three flags and explain the exploits used.

## Task 1: Information Gathering
- First, we need to determine the IP address of the Mr.Robot VM by running a quick network scan.
  - After the **Nmap** scan completes, we can identify the Mr.Robot VM and gather information about its open ports.
    - **Port 22 (SSH)** is closed, preventing us from using SSH.
    - **Ports 80 (HTTP) and 443 (HTTPS)** are open, which could be valuable for exploitation.
- We open a browser and navigate to the Mr.Robot VM's IP address to see the displayed website.

<img src="https://github.com/user-attachments/assets/1c2612f9-cec9-416c-b677-795e31413890" alt="NMAP of Website" width="300" height="200">

- Using **Nmap**, we perform **website directory enumeration** to uncover additional resources.
  - Several directories appear, and we begin probing for useful information.
  - The **robots.txt** file contains a reference to `key-1-of-3.txt`.

  ![Screenshot showing robots.txt file](path/to/your/image2.png)
  
<img src="https://github.com/user-attachments/assets/c8352257-f52f-4632-8d7f-2fe4d9883f7)" alt="Completed NMAP" width="300" height="200">

  - Navigating to this file reveals **the first key**.



## Task 2: Break Through WordPress Login
- Returning to the WordPress login page, we inspect the site to find the variable names used for login credentials (`log` and `pwd`).

<img src="https://github.com/user-attachments/assets/eb9d70c3-c1f9-4b79-a2b4-c521c25a10de" width="300" height="200">


- Using **Hydra**, we attempt to brute-force valid usernames:
  - This initial brute-force run helps identify correct usernames by testing with a placeholder password.
  - Once a valid username is found, we modify the Hydra command to brute-force passwords for that username.
  - **Successful login achieved!**

<img src="https://github.com/user-attachments/assets/c7bc52b1-c24a-47da-a458-891d7c8b9a84" width="300" height="200">


## Task 3: Leverage Admin Account
- With administrator access, we create a **reverse shell** inside the website.
- Using **Metasploit**, we deploy the `wp_admin_shell_upload` module to exploit the WordPress page.

<img src="https://github.com/user-attachments/assets/3bca591c-8b93-4299-ab3c-fb61e84436db" width="300" height="200">


- We navigate to the `/home/robot/` directory and find **the second key**, along with a file named `password.raw-md5`.



  - The file contains a username and a hashed password.
  - We use **Hashcat** to crack the hash, revealing the password: `abcdefghijklmnopqrstuvwxyz`.

  ![Screenshot of Hashcat cracking the password](path/to/your/image8.png)

  - With this password, we attempt to escalate privileges by creating a Python shell inside our **Meterpreter** session.
  - However, this does not grant root access.

- We check for binaries with **root privileges** and discover that **Nmap** is owned by root.
  - Since **Nmap** has an interactive mode, we exploit it to obtain **root access**.

  ![Screenshot showing privilege escalation using Nmap](path/to/your/image9.png)

- With root access, we locate **the third and final key**, successfully completing the challenge!

  ![Screenshot of key-3-of-3.txt](path/to/your/image10.png)

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
