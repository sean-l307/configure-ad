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

![Capture2](https://github.com/user-attachments/assets/662c4018-55d1-4313-9793-5c5eb476de3c)
</p>
<p>
First, we'll create the resources needed for this tutorial. After that the 2 virtual machine will be named "DC-1" and "Client 1" and then select the Windows Server 2022. Make sure the size is set to be 2 VCPUs and then create the VM. We must ensure that it is made under the same resource group, region, and have the same size VCPUs of the first VM.
</p>
<br />

![Capture3clickonNIC](https://github.com/user-attachments/assets/3bd99d6f-1d32-4f99-9088-c368cbb4a7c5)
![Capture4nowStatic](https://github.com/user-attachments/assets/466c4e2a-3567-46d9-9058-7759b9450c3b)
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

![Capture15 1](https://github.com/user-attachments/assets/f46bbd90-485f-46e8-abe3-3509debea779)
</p>
<p>
Next, reconnect to 'DC-1' using RDC. This time, log in with a different account by entering the username as 'mydomain.com\labuser' or the custom username you created when setting up 'DC-1.' The password will remain the same.
</p>
<br />

![AD sc](https://github.com/user-attachments/assets/13ab5e76-3574-4073-a1f4-95e82827ad1f)
</p>
<p>
Now we'll go to the server manager and then go to tools. Press "Active Directory Users and Computers
</p>
<br />


![Capture16 1](https://github.com/user-attachments/assets/9e145ec9-6f0d-4811-a837-68747a458507)
</p>
<p>
Next, create two new Organizational Units (OUs) by selecting 'mydomain,' right-clicking in the blank area, and choosing New > Organizational Unit. Name the first unit '_EMPLOYEES' and the second '_ADMINS.
</p>
<br />

![Capture17](https://github.com/user-attachments/assets/8f09b067-c1a5-4087-9b23-aef193893922)
</p>
<p>
Next, create a new admin user by clicking the icon with a person and a star at the top. Set the user’s name to Jane Doe and the login username to jane_admin. On the following screen, uncheck User must change password at next logon and proceed to finish creating the user.
</p>
<br />

![Capture17p2](https://github.com/user-attachments/assets/11a2cb9f-349d-4d67-a974-e0382c7b18c2)
</p>
<p>
Next, add Jane Doe to the Domain Admins group. Right-click on Jane Doe > Properties > Member Of tab > Add. In the object box, type ‘Domain’ and select Check Names. Choose Domain Admins, then click OK and Apply. Afterward, log out and log back in to DC-1 as jane_admin.
</p>
<br />

![Capture6newDNS](https://github.com/user-attachments/assets/d36777ed-fd9c-48c1-9da2-58ff51a175e6)
</p>
<p>
Now, set Client-1's DNS server to the private IP of DC-1. To do this, go to Client-1's networking settings in the Azure portal and select the NIC. Navigate to DNS servers, add the private IP of DC-1 to the list, and press Save. Then, restart Client-1 by returning to the VM in Azure and clicking the Restart button at the top. After it restarts, log back in.
</p>
<br />


![Capture18](https://github.com/user-attachments/assets/a81a87d8-c854-4257-b1c3-811e62163b3a)
</p>
<p>
On Client-1, go to Settings > About > Rename this PC (Advanced), then select Change domain. Enter mydomain.com as the domain and log in with mydomain.com\jane_admin. Press OK to apply the changes. Restart Client-1 and log in as jane_admin after the reboot.
</p>
<br />

![Capture20](https://github.com/user-attachments/assets/94046e45-f855-4112-a0e3-d405f3f89bd5)
</p>
<p>
After logging in, navigate to Remote Desktop Settings and select Select users that can remotely access this PC. Click Add, then type Domain Users in the object box, select Check Names, and click OK. This will allow all domain users to connect to Client-1 remotely.
</p>
<br />

![Capture19clientsCreated](https://github.com/user-attachments/assets/bd4629d0-18b4-460a-a05b-f6f60690ab3f)
</p>
<p>
Return to DC-1 and open Active Directory Users and Computers (ADUC) from the Server Manager. In mydomain, navigate to the Computers folder to confirm that Client-1 is listed.
</p>
<br />

![Capture22](https://github.com/user-attachments/assets/cbfb5df7-7817-45f4-a1e1-c208ba36c11e)
</p>
<p>
Finally, create 10,000 users with randomly generated names by copying the PowerShell script linked below. To run it, create a new script by clicking the button in the top left corner, paste the script, and click the green Run Script button.

- [Script](https://github.com/sean-l307/configure-ad/blob/main/Generate-Names-Create-Users)

Once the users are created, you can use any of them to sign in to Client-1. The default password set by the script is Password1.
</p>
<br />


![Capture26GroupPolicy](https://github.com/user-attachments/assets/4b73dded-153a-4bb2-a875-bc9b95c391e0)
</p>
<p>
As mentioned above, sign in to Client-1 using one of the users you created (for example, ban.wumak). You should be able to log in without any issues if you remember your password. However, if you encounter any login problems, return to Active Directory Users and Computers.
</p>
<br />

![Capture31 other option](https://github.com/user-attachments/assets/2fce585a-73fc-4415-856d-ed623c81b7c1)
![Capture31](https://github.com/user-attachments/assets/6cdf0b48-c3bc-4356-9ec9-2904e7000f30)

</p>
<p>
Use the search feature to locate mydomain.com, then right-click to find the user whose account you want to unlock. Once you've located the account, check the box labeled Unlock Account, and click Apply to save the changes.
</p>
<br />



