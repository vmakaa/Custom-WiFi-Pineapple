# NOTICE
ALL ATTACK RESEARCH WAS CONDUCTED ON AUTHORIZED NETWORKS WITH EXPLICIT PERMISSION

# Homemade WiFi Pineapple

The original WiFi pineapple is a wireless device used for wireless penetration testing. It can perform MITM attacks using what called an Evil AP, which is a type of attack where an attacker will set up an Access Point that has the same SSID as the target SSID or AP and will send the clients deauth packets to disconnect them from the legitimate AP so they join your AP.

It also has the ability for active reconnesance by listing all the MAC addresses connected to a targetted BSSID (MAC Address of target AP)

<img width="1200" height="1200" alt="image" src="https://github.com/user-attachments/assets/26d30831-7075-43be-962a-f0e810e8fa07" />


__________________________________________________

I thought to myself, this is just a small computer with wireless attennae, and I have a small computer with a USB WiFi Adapter. Why not make my own?

Note: technically you can just use a laptop and connect the usb adapter to get the same capabilities and use teh same open-source software, but thats less cool in my humble opinion.


<img width="3801" height="2550" alt="IMG_4931" src="https://github.com/user-attachments/assets/832fa623-5b89-4b2f-9301-f0daea34c20a" />

___________________________________________________________

To get started I first had to figure out how to perform the same functions the WiFi pineapple wanted to carry out.

This led me down a rabbit hole of different adapters not being able to support injection while most supported monitoring. I found a useful github repo called the [Plug and Play List](https://github.com/morrownr/USB-WiFi/blob/main/home/USB_WiFi_Adapters_that_are_supported_with_Linux_in-kernel_drivers.md) which tested popular adapters for both.

Note: you need two distinct attennas to support monitoring and injection at the same time

_________________________________


Now that I had the adapter I needed the open source software. Of course, the [aircrack-ng tool suite]() allows for most attacks to be done manually, but I wanted a point-and-click open source software similar to how I imagined the WiFi Pineapple would be.

After comparing many tools like WiFite and the WiFiPumpkin3, I settled on EAPHammer, Bettercap, and mitmproxy. According to my research, these tools appear to be the most recognized among actual WiFi pentesters and the most modular.


_________________________________


Before going into the weeds of the tools, I would like to go over some essential aircrack-ng tool suite commands I used in order to successfully test the wireless network I was targeting.

When you connect a USB wifi adapter and successfully install all needed dependencies, the (in my case Linux) system will assign a wlan interface to it. Usually wlan1 if you have an onboard wifi card on a Linux system. 

Knowing this information the first command is "sudo airmon-ng start wireless interface name".

This command puts the interface assigned to your USB WiFi adapter into monitor mode. 

Now that your interface is in monitor mode, with the right commands usually using the commands associated with airodump-ng, this will allow you to view all APs in your range, what channels they are communicating over, the MAC address (or BSSID) of the AP, and the MAC Addresses of each client connecting to the AP.


For example, to view all APs in your range use the command "sudo airodump-ng wireless interface name"

_______________________________________________________


Now there are many types of attacks you can perform using devices like these, but the ones that were the most interesting to me were ARP Spoofing, DNS Spoofing, SSL Stripping, and using mitmproxy to inspect both http and https traffic all in the CLI.


_______________________________________________________

# ARP SPOOFING
arp spoofing is
