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

- Windows Server 2025 Datacenter Azure Edition: - x64 Gen2
- Windows 11 Pro (25H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create the Resource Group VNet, and subnet in Azure. (SET EVERYTHING TO THE SAME REGION TO PREVENT ISSUES)
- Set up the Domain Controller VM in Azure (Titled dc-1) and connect it to the newly created VNet.
- Set the Domain Controller's NIC Private IP address from Dynamic to Static.
- Log in to the Domain Controller VM & Deactivate the firewall for dc-1.
- Set up the Client VM (Titled Client-1) and connect it to the same region, VNet and subnet as the Domain Controller.
- Set the Client VM's DNS settings to the Domain Controller's Private IP. The domain controller will act as the Client VM's DNS Server.
- After changing the DNS settings for the Client VM, restart it in Azure to initiate the changes made.
- Log into the Client VM, open powershell, type "ipconfig /all", hit Enter. The DNS settings should show the Domain Controller VM's Private IP address.

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/3848648c-c750-4955-9b6a-0a63d04f7185" />
</p>
<p>
Upon connecting to dc-1, Server Manager should automatically start up. If not, go ahead and launch it. Click on #2 "Add roles and features". 
</p>
<br />

<p>
<img width="1381" height="982" alt="image" src="https://github.com/user-attachments/assets/4834283f-a4c1-4cd9-90d1-9fe6304ccaea" />
</p>
<p>
Click "next" for the first two prompts, then ensure dc-1 is the selected and only server listed and click next.
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/388324f5-95c9-4d48-9dab-a5cdc7d591de" />
</p>
<p>
Check the box that correlates with "Active Directory Domain Services" and click "Add features" from the pop-up. Click next when finished.
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/96118466-aa30-42b5-a809-26bbe0abad32" />
</p>
<p>
Continue to click "next" until you reach the "Confirmation" tab. Check the box at the top to enable restarting the destination server automatically if required, then click Install.  
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/1253113f-d07a-4894-8be5-4baecc302007" />
</p>
<p>
After succesfully installing the AD Domain Services, click on the flag icon located at the top right of the Server Manager window. Click on the blue text to promote dc-1 to an actual Domain Controller.
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/b3a1c03b-d436-4a80-ae33-23b7af5f4cc0" />
</p>
<p>
In the window that pops up, select "Add a new forest" and in the box below type "mydomain.com" click next when done.
</p>
<p>
<img width="1335" height="982" alt="image" src="https://github.com/user-attachments/assets/185bdbee-2bf8-4840-9898-e4dfdee84f8f" />
</p>
<p>
This password will never be used, just fill one in and keep track of it just in case. Click next when finished.
</p>
<br />

<p>
<img width="1335" height="982" alt="image" src="https://github.com/user-attachments/assets/4d0b2550-d1b3-4cc3-a488-5495512321cd" />
</p>
<p>
Leave "Create DNS Delegation" unchecked and click next until you reach the prerequisites check not changing anything else.
</p>
<br />

<p>
<img width="1335" height="982" alt="image" src="https://github.com/user-attachments/assets/1f476b43-b767-4ae5-b25a-3f787e233082" />
</p>
<p>
After reaching the prerequisites check tab, click install once it everything been checked and approved.
</p>
<br />
