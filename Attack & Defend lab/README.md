# Overview
This Homelab simulates an attacker and defender scenario which features a Kali Linux and a Windows 10 virtual machine. 
The Windows 10 machine utilizes Splunk to ingest logs to identify malicious traffic by the Kali machine, as well as Sysmon

# Table of Contents
- [Setting up VirtualBox](#Setting-up-VirtualBox)
- [Configuring the Windows machine](#Configuring-the-Windows-machine)
- [Configuring the attacker machine](#Configuring-the-attacker-machine)




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

* Now we are able to add the ISO to VirtualBox and create our Windows 10 client, I chose a generic name for our Business User
* Note: I skipped the unattended installation
<img width="1736" height="407" alt="image" src="https://github.com/user-attachments/assets/1e834947-aed4-4c1b-8a60-3508a19d9c5f" />

* I've allocated 4 GB of RAM, as well as 50 GB of space for the VM
  <img width="1740" height="370" alt="image" src="https://github.com/user-attachments/assets/e5f36f87-620d-4636-b9f1-aae763418a30" />
* When setting up the Windows machine, ensure that the option for I don't have a product key is selected
  <img width="640" height="480" alt="image" src="https://github.com/user-attachments/assets/a9f2f0ef-4c41-4657-814c-95e8096853ca" />


  <img width="633" height="476" alt="image" src="https://github.com/user-attachments/assets/b8dda7fa-597a-4780-8efc-fd117dc50161" />
* Choose the custom installation option, and begin the installation:
<img width="632" height="471" alt="image" src="https://github.com/user-attachments/assets/a3a9e13b-a2a6-441a-bdd9-376e9499da490" />
Ensure you choose the option have a local account

For the security questions, I submitted dummy answers, and disabled the privacy settings
<img width="1022" height="668" alt="image" src="https://github.com/user-attachments/assets/2ec45967-5727-4a32-966e-bb32b03f3459" />
A successful installation of the Windows VM should look like this:
<img width="1023" height="776" alt="image" src="https://github.com/user-attachments/assets/1443a081-ed7c-427c-aaf7-ca7b8d21ab3f" />
Most importantly, I've taken a snapshot to revert back to if something goes wrong
  <img width="1512" height="140" alt="image" src="https://github.com/user-attachments/assets/ebce9f6d-a2fe-435d-a33d-7e16e41c526e" />
Now that we have successfully configure the Windows VM, we can now configure Splunk and Sysmon


  
# Configuring the attacker machine
* I retrieved the ISO for the Kali machine by visiting the installer images [page](https://www.kali.org/get-kali/#kali-installer-images)
* I chose the ISO image instead of a pre-built to have more control of the installation and configuration process
* Like the Windows machine setup, I skipped the unattended installation
  <img width="1740" height="406" alt="image" src="https://github.com/user-attachments/assets/c2d4de9c-62c6-4c09-8e62-64051c6b6e79" />
* I also allocated 2 GB of RAM, as well as 80 GB for the storage space for the Kali VM
  <img width="1743" height="357" alt="image" src="https://github.com/user-attachments/assets/57a30ef7-35f2-4f18-9127-e6d85f2ec858" />
* When booting the Kali machine, choose the graphical installation. I also chose the default hostname of kali
* Choose the credentials you want and use the Guided Partition to use the entire disk
  <img width="798" height="598" alt="image" src="https://github.com/user-attachments/assets/78b0b7aa-5a6f-4ca5-b7ab-0eb3ad5fe961" />
* Keep all files in one partition and choose the default software selection
  <img width="797" height="603" alt="image" src="https://github.com/user-attachments/assets/ab9344da-98d3-4f2f-bfbb-3668995af604" />
* Install GRUB, and have it set to the /dev/sda directory
  <img width="801" height="527" alt="image" src="https://github.com/user-attachments/assets/0a4223e6-4d17-4299-a152-14a0185fb6e5" />






  
# Implementing Splunk
# Configuring Sysmon





