<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create resources in a resource group in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in Active Directory
- Join Client-1 to your domain
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users
- Delete resources

<h2>Deployment and Configuration Steps</h2>

![Capture2](https://github.com/user-attachments/assets/75565ae6-e365-4247-8a04-1865b86b7838)
</p>
<p>
First, we'll create the resources needed for this tutorial. After that the 2 virtual machine will be named "DC-1" and "Client 1" and then select the Windows Server 2022. Make sure the size is set to be 2 VCPUs and then create the VM. We must ensure that it is made under the same resource group, region, and have the same size VCPUs of the first VM.
</p>
<br />

![Capture3clickonNIC](https://github.com/user-attachments/assets/ab8bb334-5df2-4967-bfc7-1c59f5479310)
![Capture4nowStatic](https://github.com/user-attachments/assets/5d7d06c7-be2b-477e-b95f-76172538f6e4)
</p>
<p>
Next, open DC-1 and navigate to the NIC (Network Interface Card) as shown above. Go to 'IP Configurations' and select 'ipconfig1. Set the IP to static, then click 'Save' in the top left.
</p>
<br />

![Capture5offFirewall](https://github.com/user-attachments/assets/b11f64c9-df7b-45d1-af01-9d4fc329de2b)
</p>
<p>
Afterward, log in to "DC-1" and open Windows Defender Firewall with Advanced Security by searching for it in the search bar. After going to the Domain, Public, and Private profile turn the Firewall state off.
</p>
<br />

![Capture10](https://github.com/user-attachments/assets/01f7a5b6-97e0-4e63-a5f1-0e347fc00038)
![Capture11](https://github.com/user-attachments/assets/a8addb32-5ca4-46de-857a-595e8b9a0506)
</p>
<p>
Finally, we’ll install Active Directory on DC-1. Open DC-1 and go to Server Manager. First, select Add Roles and Features, then click Next until you reach the Server Roles section. Check the box for Active Directory Domain Services, select Add Features when prompted, and continue clicking Next until you reach the option to Install.
</p>
<br />

![Capture12](https://github.com/user-attachments/assets/ec3ea82e-9e7e-4c48-898d-b90ae2268744)
</p>
<p>
Next, we’ll promote DC-1 to a domain controller. In Server Manager, click the flag with the caution icon at the top right and select Promote this server to a domain controller.
</p>
<br />

![Capture13](https://github.com/user-attachments/assets/4d71c644-159a-4976-9b23-c132b01cb2da)
</p>
<p>
Next, check "Add a new forest" name it to anything you want. In this tutorial we will use "mydomain.com" and hit next.
</p>
<br />

![Capture14](https://github.com/user-attachments/assets/2cfda1e3-0f54-45d1-ae4d-141e713f316c)
</p>
<p>
Now you can make a DSRM password in the Domain Controller Options section and hit next until you are able to install. This will restart the virtual machine after it is finished.
</p>
<br />

<p>
------
</p>
<p>
 ---
</p>
<br />

<p>
------
</p>
<p>
 ---
</p>
<br />

<p>
------
</p>
<p>
 ---
</p>
<br />

<p>
------
</p>
<p>
 ---
</p>
<br />

<p>
------
</p>
<p>
 ---
</p>
<br />

<p>
------
</p>
<p>
 ---
</p>
<br />
