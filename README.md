# Introduction 

We are going to continue the configuration of Pfsense from our last post. 

# Process

First We need to create our machine, if you have been through the process and installed the VirtualBox and the Active Directory from my last post, Pfsense is a straightforward installation, but we’ll make some changes in the configuration. When the configuration asks us about the partition disk, we will choose the BIOS option, and that would be the only change for the moment. 

![pfpartition](https://github.com/Wfrestrepo/PFsense/assets/108705302/72dc08e2-f3ab-483c-82e9-072d1d6807ea)

After clicking on Reboot to finalize the installation process, we need to turn off the machine and navigate to settings > Storage > Remove attachment to delete the ISO file. This is because we already have a copy of the ISO file in the virtual disk, and if we don't remove the ISO file, the machine will enter into a loop, continuously attempting to install the software.

![pf remove](https://github.com/Wfrestrepo/PFsense/assets/108705302/d5642f6c-9066-4fb0-98fd-7754f96eec4d)

During the installation process, we will be asked if we want to set up VLAN. For now, select "n". Also, note that the WAN interface may be different for you. In my case, it is "em0". Next, we will be asked if we want to configure the LAN. The answer is "n" for now. After that, we can proceed with the installation by selecting "y".

![pf Vlanwan](https://github.com/Wfrestrepo/PFsense/assets/108705302/4beacfa3-59c2-496e-acf1-88bd0faf1928)

After you have set up the firewall, three things will be displayed: the WAN, interface, and IPv4. It is important to note that we assign a static IP address to our firewall. To do this, you must log in to your web browser using the IP address. The default credentials for logging in are "admin-pfsense".

![pfsense](https://github.com/Wfrestrepo/PFsense/assets/108705302/250a338b-a866-4db9-bfb8-88b237b8104e)

In General information, we just changed the DNS to be the Google DNS of 8.8.8.8.


![pf Google](https://github.com/Wfrestrepo/PFsense/assets/108705302/7b7745d0-3b6a-49ce-a1ad-823297fa2017)

After, we will assign the static IP and the default gateway to our physical host.

![pf IP and Static](https://github.com/Wfrestrepo/PFsense/assets/108705302/19238778-964a-4715-98ca-4a21046510d8)

Let's talk about some of the features you can implement on your firewall. For example, you may want to restrict access to a specific website. To achieve this, we need to add Aliases. To get started, click on Firewall > Aliases at the top of your dashboard.


![Aliases](https://github.com/Wfrestrepo/PFsense/assets/108705302/7ac0b530-9d7b-4b78-ad4c-a13555beaf55)

I have already created the rule, but I'll guide you through the process of creating one. The website's domain name is "Defend the Web" and it has an IP address of 3.10.42.19/32. To find this IP address, you can open the command prompt and type "nslookup". This command will provide you with the IP address of any domain name, such as "Defend the web". 

![pfcmd](https://github.com/Wfrestrepo/PFsense/assets/108705302/c7fcf272-8e0e-4923-8e16-6cf596c33f4c)

Now that we have the IP address we proceed to create the Aliases:

![pfaliases](https://github.com/Wfrestrepo/PFsense/assets/108705302/b19a99cc-4881-4246-bba4-29089e39dcb4)

To create rules in Pfsense, navigate to Firewall > Rules. The Firewall comes with two default rules – the Anti-lock rule and the Block bogon networks rule. Both of these rules serve a specific purpose, and if you need more information about them, you can refer to Pfsense documentation.  https://docs.netgate.com/pfsense/en/latest/firewall/rule-methodology.html  

That being said, the two rules that we going to create are: 

To block traffic going from our network to the specific IP address.

![pfdefen](https://github.com/Wfrestrepo/PFsense/assets/108705302/58b4038e-f457-4edb-ab3a-34514a996caf)

A rule to allow us to access the internet through our Firewall, due to Pfsense having an implicit deny by default.

![pfallow](https://github.com/Wfrestrepo/PFsense/assets/108705302/def90674-b5c7-4884-9f35-8f8e8a8ea444)

It's possible that even after setting the aliases and rules, you may not notice any changes in the traffic. This could be happening because the Firewall might be connected to the internet and your workstation, but not in between them. The image below will make this clearer. 

![pfchangefateway](https://github.com/Wfrestrepo/PFsense/assets/108705302/7ed6038e-9902-4fd4-bf2f-a6cd6db54b8b)

To access the configuration, go to Control Panel > Network and Internet>  Network and Sharing Center> click on your WI-FI properties > IPv4 > and change your default gateway to the IP address of the firewall, the same as the DNS server. This will place your firewall in the middle of your connection.

![pfip4](https://github.com/Wfrestrepo/PFsense/assets/108705302/be1fb04d-79ac-4564-802f-0829d4c7abe0)

![pfirewallip](https://github.com/Wfrestrepo/PFsense/assets/108705302/c4889e77-a921-4b20-90bf-9b10962584bc)

# Conclusion

Firewalls are essential tools to manage network traffic and monitor activity. However, proper configuration of firewall rules is crucial to ensure network security. 
