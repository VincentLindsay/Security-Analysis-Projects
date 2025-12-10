# Overview
This Homelab simulates an attacker and defender scenario which features a Kali Linux and a Windows 10 virtual machine. 
The Windows 10 machine utilizes Splunk to ingest logs to identify malicious traffic by the Kali machine, as well as Sysmon

# Table of Contents
- [Setting up VirtualBox](https://github.com/VincentLindsay/Security-Analysis-Projects/tree/main/Attack%20%26%20Defend%20lab#setting-up-virtualbox)
- [Configuring the Windows machine](https://github.com/VincentLindsay/Security-Analysis-Projects/tree/main/Attack%20%26%20Defend%20lab#configuring-the-windows-machine)




## Setting up VirtualBox
This Lab utilizes Virtual Box as our hypervisor
* I installed VirtualBox by visiting the downloads [page](https://www.virtualbox.org/wiki/Downloads), and select the download option based off your host machine
* Since my host machine is Windows, I chose the download option for Windows:

<img width="468" height="262" alt="image" src="https://github.com/user-attachments/assets/689fc577-cc7c-47eb-8155-cb9edbb17002" /> 

* A successful installation using default options should look like this:
<img width="612" height="482" alt="image" src="https://github.com/user-attachments/assets/a44108be-aa82-4f5e-96a5-00d3810ee0e9" />

# Configuring the Windows machine
* Now that the hypervisor is installed, we can now install and configure the Windows 10 client, which simulates a business user
* I will create a virtual machine for Windows by using the [media creation tool](https://www.microsoft.com/en-us/software-download/windows10)
  
* You will create an installation media to make an ISO file
<img width="792" height="252" alt="image" src="https://github.com/user-attachments/assets/c6f3431f-d441-4ab0-ada1-3ac75ea8147b" />

* Next, choose your settings for the installation media, I chose to keep the recommended options for my host machine
<img width="782" height="421" alt="image" src="https://github.com/user-attachments/assets/e1787bb7-26cf-4e96-94ef-6b58535e8e08" />

* With these settings, choose the option to create an ISO image to be used in VirtualBox
<img width="788" height="351" alt="image" src="https://github.com/user-attachments/assets/6e8707c4-db68-40bb-8b92-0cbed2da7ced" />

# Implementing Splunk
# Configuring Sysmon





