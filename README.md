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

- Create the Resource Group and VNet in Azure
- Set up the Domain Controller VM in Azure and connect it to the newly created VNet.
- Set the Domain Controller's NIC Private IP address from Dynamic to Static.
- Set up the Client VM and connect it to the same region and VNet as the Domain Controller.
- Set the Client VM's DNS settings to the Domain Controller's Private IP. The domain controller will act as the Client VM's DNS Server.
- After changing the DNS settings for the Client VM, restart it in Azure to initiate the changes made.
- Log into the Client VM, open powershell and type "ipconfig /all". The DNS settings should show the Domain Controller VM's Private IP address.

<h2>Deployment and Configuration Steps</h2>

<p>

</p>
<p>

</p>
<br />

<p>

</p>
<p>

</p>
<br />

<p>
</p>
<p>
  
</p>
<br />
