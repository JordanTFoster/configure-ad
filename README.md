<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell [(Script)](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

<h2>Operating Systems Used </h2>

- Windows Server 2025 Datacenter Azure Edition: - x64 Gen2
- Windows 11 Pro (25H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create the Resource Group VNet, and subnet in Azure. (SET EVERYTHING TO THE SAME REGION TO PREVENT ISSUES)
- Set up the Domain Controller VM in Azure (Titled dc-1) and connect it to the newly created VNet.
- Set the Domain Controller's NIC Private IP address from Dynamic to Static.
- Log in to the Domain Controller VM & Deactivate the firewall for dc-1.
- Set up the Client VM (Titled Client-1) and connect it to the same Region, VNet and Subnet as the Domain Controller.
- Set the Client VM's DNS settings to the Domain Controller's Private IP. The Domain Controller will act as the Client VM's DNS Server.
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
After reaching the prerequisites check tab, click install once everything has been checked and approved. After the install the VM will restart automatically to initiate the changes just made.
</p>
<br />

<p>
<img width="798" height="801" alt="image" src="https://github.com/user-attachments/assets/7387fb05-171b-4aa2-871d-60524a46d566" />
</p>
<p>
Due to dc-1 becoming an actual Domain Controller now, the login credentials have changed. The user is now "mydomain.com\labuser". with mydomain.com being our domain that we created & labuser being the user in that domain that we're logging in as. "\" A back slash must be used not "/"  a front slash when spacing the domain and user in the username login.
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/cdc3b667-0853-4192-98fd-b570c5f49716" />
</p>
<p>
After signing in to dc-1, open the start menu and search for "Active Directory Users and Computers" and run the application.
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/7ecab276-fa92-4239-ac2d-d425f0710b84" />
</p>
<p>
On the far left panel, right click "mydomain.com" to bring up some options, hover over "New", then click "Organizational Unit".
</p>
<br />

<p>
<img width="762" height="660" alt="image" src="https://github.com/user-attachments/assets/59bef233-2706-4664-a4c2-6a1aa403e7dc" />
</p>
<p>
Title the new Organizational Unit "_EMPLOYEES" do not forget to include the underscore. Click Okay when finished. 
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/7ecab276-fa92-4239-ac2d-d425f0710b84" />
<img width="760" height="660" alt="image" src="https://github.com/user-attachments/assets/ed6248a7-d93b-49d0-8f3e-5e5527cbf815" />
</p>
<p>
Create one more Organizational Unit, but this time title it "_ADMINS". Same as last time don't forget the underscore and click Okay when finished. The script we'll be running later that creates all of our "employees" relies on the Organizational Units being named correctly. 
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/31b7d942-ff58-4318-8616-d71f1095978d" />
  
With the "_ADMINS" folder selected right click either on the folder itself or inisde the empty space. Hover over "New", and click "User".
</p>

<p>
<img width="766" height="662" alt="image" src="https://github.com/user-attachments/assets/733c3a34-3638-416c-a86d-f78cd5189487" />

This user is going to be named "Jane Doe" with the username set as "jane_admin". Click next when the information has been filled in.
</p>

<p>
<img width="766" height="662" alt="image" src="https://github.com/user-attachments/assets/0358fedc-a064-49ef-ac9b-a192426b1e6f" />
  
Set the password as the same password used to sign into dc-1, just to keep things simple. Only check the box that says "Password never expires". then click next when done.
</p>

<p>
<img width="766" height="662" alt="image" src="https://github.com/user-attachments/assets/415865fa-7af4-44f0-8348-f98123407145" />

Verify the information is correct and click Finish to create the new user.
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/4b8fcfe8-cf6c-4765-9602-2978d3be29c1" />

Right click on the user you just created and click on properties. We're going to make this user an admin by adding them to the Domain Admins Security Group.
</p>

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/3d3912f1-c115-491b-9b3c-79fbb7c29690" />

Inside of the users properties, click on the "Member Of" tab, Click "Add" to create a new group titled "Domain Admins". Click "Check names" to verify correct spelling and spacing, then click "Ok" to create the group and finally click "Apply" to finalize the changes made.Then log out of the VM so we can sign in with the new Admin users credentials.
</p>
<br />

<p>
<img width="798" height="804" alt="image" src="https://github.com/user-attachments/assets/cd110dca-d8db-4ae4-9d5a-928f458c1928" />

When signing back into the dc-1 VM as the new Admin user we just created, you want to ensure the user info is typed in correctly. For example my user info will be "mydomain.com\jane_admin". Ensure the Domain comes first, seperated by a back slash " \ ", followed by the username. Then fill in the password you created and sign into the VM.
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/9334c136-8a26-47ed-8c65-96a0aa355187" />

Signed into the client-1 VM with the labuser credentials, right click on the windows logo on the task bar. Then click on "System"
</p>
<br />

<p>
<img width="2103" height="1625" alt="image" src="https://github.com/user-attachments/assets/e7df30f7-8689-4719-b64a-8916ed3a80db" />

Click on advanced system settings
</p>

<p>
<img width="2103" height="1625" alt="image" src="https://github.com/user-attachments/assets/19a0f219-295d-4d5c-91fc-f385a394dc4d" />

Click on the tab "Computer Name", then click "Change". 
</p>

<p>
<img width="2104" height="1626" alt="image" src="https://github.com/user-attachments/assets/93a5c36d-798d-4119-b03d-8d292b2dc89b" />

Under "Member of" click the circle titleed Domain to change the domain for client-1. In the box type "mydomain.com" this is joining client-1 to the domain we created. 
</p>

<p>
<img width="2103" height="1625" alt="image" src="https://github.com/user-attachments/assets/f5ae475e-62bf-4bc4-82c1-75505f804434" />

You will need to enter the Admin credentials we created earlier in order to authorize the changes made and join the domain. Click Ok when finished. You will get a pop up saying welcome to the domain and it will prompt a restart to initiate the changes made. 
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/9c302cb4-e453-4749-9e53-97a457c2932b" />

Back on the dc-1 VM, search for Active Directory Users and Computers and run the application. We are going to verify that clinet-1 is showing up on the domain under the computers tab.
</p>
<br />

<p>
<img width="1321" height="928" alt="image" src="https://github.com/user-attachments/assets/08794a9d-5a85-475d-ac9d-412cb3ffc9ef" />

Under the mydomain.com drop down on the left side panel, select computers and we should see client-1 under that list. Next we will create a new Organizational Unit and title it "_CLIENTS" and drag client-1 into that new OU.
</p>
<br />

<p>
<img width="1321" height="928" alt="image" src="https://github.com/user-attachments/assets/faf6702d-5524-4548-aed2-2e68f908c796" />

Right click on mydomain.com from the left side drop down, hover over New, Click Organizational Unit.
</p>

<p>  
<img width="3199" height="1799" alt="image" src="https://github.com/user-attachments/assets/503a8ab1-c64b-49c7-8b3f-875cfa21613d" />

Title the new Organizational Unit "_CLIENTS" then click Ok when finished. 
</p>
<br />

<p>
<img width="1321" height="928" alt="image" src="https://github.com/user-attachments/assets/4d0d5dee-daf1-4100-a8a3-e9ac90856547" />

Open the Organizational Unit titled Computers to locate client-1 again so we can drag it to the newly created OU titled _CLIENTS. Just simply drag and drop it to the location.
</p>

<p>
<img width="3199" height="1799" alt="image" src="https://github.com/user-attachments/assets/f38983e2-deb6-4c56-bc3b-1e37592c48ec" />

You will recieve a pop-up just click yes to confirm and move it over. 
</p>
<br />

<p>
<img width="798" height="800" alt="image" src="https://github.com/user-attachments/assets/e0ba9216-9940-4d48-a85d-0a37ef198f5f" />

Sign out of client-1 and sign back in using the Admin Credentials we created, mine is jane_admin. 
</p>
<br />

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/46537836-c459-4b84-9e43-1fa79bc71eb4" />

After signing in to client-1 with the admin credentials, right click the windows logo and click on system.
</p>

<p>
<img width="3200" height="1716" alt="image" src="https://github.com/user-attachments/assets/0a8a6086-556b-4817-93f2-9a2197a02f58" />

Scroll down and click on remote desktop.
</p>

<p>
<img width="3200" height="1716" alt="image" src="https://github.com/user-attachments/assets/cd349c7a-d981-46c2-8b4e-f078bb09dd72" />

Click "Remote Desktop Users", we're going to add "Domain Users" to the list of users able to remote into this machine. 
</p>

<p>
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/bbd89c17-c643-48fa-ab52-6a10634cfce6" />

Click add to bring up another pop-up window, from here we will type "Domain Users" then click check names to verify spelling and click ok when finished.
</p>

<p>
<img width="691" height="609" alt="image" src="https://github.com/user-attachments/assets/4e99e3ed-7ba2-4fe9-99b4-00e5aaf92d4d" />

After successfully filling in the required information click Ok to apply the changes to the remote desktop users.
</p>
<br />

<p>
<img width="1400" height="1312" alt="image" src="https://github.com/user-attachments/assets/a5eeebb3-36d2-4794-9cbf-832e698ac2e9" />

Back on dc-1 logged in with the admin credentials, look up Windows Powershell ISE and run it as an admin. Click yes to allow changes to the device when prompted.
</p>
<br />

<p>


</p>
