# Overview
This Homelab simulates an attacker and defender scenario which features a Kali Linux and a Windows 10 Enterprise virtual machine. 
The Windows 10 machine utilizes Splunk to ingest logs to identify malicious traffic by the Kali machine, as well as Sysmon.

# Table of Contents
- [Setting up VirtualBox](#Setting-up-VirtualBox)
- [Configuring the Windows machine](#Configuring-the-Windows-machine)
- [Configuring the Attacker machine](#Configuring-the-attacker-machine)
- [Implementing Splunk](#Implementing-Splunk)
- [Configuring Sysmon](#Configuring-Sysmon)




## Setting up VirtualBox
This Lab utilizes Virtual Box as our hypervisor
* I installed VirtualBox by visiting the downloads [page](https://www.virtualbox.org/wiki/Downloads), and select the download option based off your host machine
* Since my host machine is Windows, I chose the download option for Windows:

<img width="468" height="262" alt="image" src="https://github.com/user-attachments/assets/689fc577-cc7c-47eb-8155-cb9edbb17002" /> 

 A successful installation using default options should look like this:
<img width="612" height="482" alt="image" src="https://github.com/user-attachments/assets/a44108be-aa82-4f5e-96a5-00d3810ee0e9" />

# Configuring the Windows machine
* Now that the hypervisor is installed, we can now install and configure the Windows 10 enterprise client, which simulates a business user
* Normally, you would to access the evaluation [center](https://www.microsoft.com/en-us/evalcenter) to be able to retrieve enterprise ISO files
* There is a work-around where you can have the media creation tool generate an ISO for a Windows 10 enterprise machine, to do this you can perform the following:
  
* You will download the medial creation tool for Windows [10](https://www.microsoft.com/en-us/software-download/windows10)
* For the work-around, I found a method on [youtube](https://www.youtube.com/watch?v=DR_75hjFFas),credit goes to [TimsComputerRepair](https://www.youtube.com/@TimsComputerRepair)
* Now, the work-around involves the use of a powershell script in the same directory as the windows 10 media creation tool:

```Bash
.\MediaCreationTool_22H2.exe /Eula Accept /Retail /MediaArch x64 /MediaLangCode en-US /MediaEdition Enterprise
```
Note: in the video, the edition of the Media Creation Tool is different, you can simply change the verion (e.g 22H2), and the script will execute

In powershell as Administrator, navigate to the directory using the **cd** command in which you downloaded the media creation tool in
<img width="962" height="263" alt="image" src="https://github.com/user-attachments/assets/242bf9ed-6c91-4006-ae91-f5676c35d159" />

I can now use the script listed above to achieve the ability to retrieve an enterprise ISO

Next, the Windows 10 Setup will now ask for a Product key, you can enter a generic key found on ten [forums](https://www.tenforums.com/tutorials/95922-generic-product-keys-install-windows-10-editions.html)
<img width="790" height="696" alt="image" src="https://github.com/user-attachments/assets/ac06638b-88de-4122-b98e-5ec3c9912d7f" />

All the product key does is allow you to use the edition

Once you enter the generic retail key, you can create an ISO file
<img width="776" height="697" alt="image" src="https://github.com/user-attachments/assets/fef58071-5641-4ffb-b8ce-f9caf7fc0940" />

Here is a screenshot that demonstrates the successful creation of a Windows 10 ISO for our machine

Now we are able to add the ISO to VirtualBox and create our Windows 10 client, I chose a generic name for our Business User
Note: I skipped the unattended installation
<img width="1736" height="407" alt="image" src="https://github.com/user-attachments/assets/1e834947-aed4-4c1b-8a60-3508a19d9c5f" />

 I've pre-allocated 4 GB of RAM, as well as 150 GB of space for the VM


  Choose the custom installation option, and begin the installation
  <img width="633" height="476" alt="image" src="https://github.com/user-attachments/assets/b8dda7fa-597a-4780-8efc-fd117dc50161" />

  Choose the option for Windows 10 Pro, and ensure you choose the option have a local account

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
* A fresh install of a Kali VM looks like this:
  <img width="1918" height="982" alt="image" src="https://github.com/user-attachments/assets/52653fda-58b5-4c52-9b6f-7c657a6cea4b" />
* Prior to conducting any simulated attacks, I updated the packages using this command:
  ```bash
   sudo apt update
  ```
# Implementing Splunk
* Splunk is our Security Information & Event Management (SIEM) tool that will be installed on our Windows machine to analyze telemetry generated by the attacker's machine
* To Install splunk, we will navigate to Splunk's Enterprise landing [page](https://www.splunk.com/en_us/download/splunk-enterprise.html)
* Enter Basic information, or login to a splunk account
* Download splunk based on your VM's operating system, and agree to the EULA
* I chose the default configuration settings for splunk
<img width="487" height="382" alt="image" src="https://github.com/user-attachments/assets/215dbd11-1f7b-45c5-8dee-941d346f696f" />

* Create account credentials for the splunk local administrator account

* After this, splunk can begin to install, and you should get this page once Splunk is installed
<img width="492" height="385" alt="image" src="https://github.com/user-attachments/assets/6cd2ef2c-2353-4cc7-8006-363ce447f58b" />
* Once installed, you can login to Splunk using the credentials you entered when installing Splunk
* Since we will be using Sysmon, we can also download the Splunk for Sysmon application on the Splunk dashboard
 <img width="965" height="625" alt="image" src="https://github.com/user-attachments/assets/108953b7-be4c-461b-bd48-d7f7fbe8cefa" />
* To properly configure our machine to send logs to splunk, we must implement configuration settings
* You will need to modify the local configuration file, which is located on a fresh in stall in the directory: C:\Program Files\Splunk\etc\system\default\inputs.conf
* I copied and pasted the file onto the C:\Program Files\Splunk\etc\system\local directory
<img width="711" height="226" alt="image" src="https://github.com/user-attachments/assets/2ed4718f-50bd-4074-8dca-98f75f320cdd" />
* I Utilized MyDFIR's guide on how to create the additional configurations for (sysmon)[https://www.youtube.com/watch?v=-8X7Ay4YCoA&t=757s]
* Here is an example of some of the configuration settings:
<img width="651" height="533" alt="image" src="https://github.com/user-attachments/assets/33eec338-1eb8-449a-a2dd-5f5a933af191" />






# Configuring Sysmon
* To install Sysmon, we will navigate to the Sysmon installation on Microsoft's System Internals [page](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon) 
* Once installed, extract the .Zip file, and they should look like this:
<img width="847" height="175" alt="image" src="https://github.com/user-attachments/assets/afbac984-893f-4c8c-8e6f-b546faa24ad3" />

* We will utilize the popular olaf configuration [settings](https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml)
* On the github page, navigate towards the sysmonconfig.xml file
* Click the raw option and save the file to the folder that Sysmon belongs to
* Open a PowerShell window as Administrator







