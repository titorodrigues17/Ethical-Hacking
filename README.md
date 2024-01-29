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
   >Recuerda conectarte al servidor con tu android en este caso deben estar en la misma red ya que el servidor es local al igual que nuestro ataque
