
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Domain Controller Virtual Machine (DC-1). Windows Server 2022
- Client 1 Virtual Machine (Client-1). Windows 10 Pro

<h2>High-Level Deployment and Configuration Steps</h2>

- Install Active Directory
- Create a Domain Admin User within the Domain
- Join Client-1 Virtual Machine (VM) to the domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on the Client-1 VM
- Create additional users and attempt to log into client-1 VM with one of the new users



<h2>Deployment and Configuration Steps</h2>

<p>

![add roles and features](https://github.com/user-attachments/assets/e304d5ee-fce9-4b9d-b7e8-e148696c921e) ![Install ADDS](https://github.com/user-attachments/assets/2543fd29-1010-4c59-8785-7fe548d6ad00) ![adding  client-1 to the domain](https://github.com/user-attachments/assets/67bb888f-8c85-4d79-b47f-383b8fac5d67)

  
</p>
<p>
Installing Active Directory, from the Domain Controller Virtual Machine, also known as DC-1. Open Server Manager and click "Add Roles and Features", install Active Directory Domain Services. In the third screenshot, select "Rename this PC (advanced)", Promote as a Domain Controller: Setup a new forest as "mydomain.com" (can be anything). Restart and then log back into DC-1 as user: "mydomain.com\labuser".
</p>
<br />

<p>

![create jane doe](https://github.com/user-attachments/assets/4f8eb0fc-d6f2-4943-908b-75a7082cb274) ![jane as domain admins](https://github.com/user-attachments/assets/872a2324-fcd9-439b-9f58-cac5cb5258c4)

</p>
<p>
Creating a Domain Admin user within the Domain, In Active Directory Users and Computers (ADUC), create two Organizational Units (OU) called “_EMPLOYEES” and “_ADMINS” by right clicking on my domain, hover over "New", and click "orgizational unit". Create a new employee named “Jane Doe”, for example, with the username of “jane_admin”. Add jane_admin to the “Domain Admins” Security Group. Finally, log out / close the connection to the Domain Controller VM and log back in as “mydomain.com\jane_admin”. This would become the main Administrative Account for the Domain.    
</p>
<br />

<p>

![client-1 as part of the domain](https://github.com/user-attachments/assets/e3235c44-beeb-48bd-811c-ff7ef1b743b4) ![client-1 dragged into clients OU](https://github.com/user-attachments/assets/9ec8844f-e111-4f97-a302-086ef3b63152)

</p>
<p>
Joining Client-1 to the Domain, login to Client-1 as the original local admin and join it to the domain (computer will restart). Login to the Domain Controller VM and verify that Client-1 VM shows up in Active Directory Users and Computers (ADUC). Create a new Orgizational Unit (OU) named “_CLIENTS” and drag Client-1 into it. 
</p>
<br />

<p>

![allowing domain users remote desktop](https://github.com/user-attachments/assets/3e956cd5-5294-4f8f-bd1c-f6b3cd4257fa)

</p>
<p>
Setup Remote Desktop for non-administrative users on Client-1 VM. Login to the Client-1 VM as mydomain.com\jane_admin. Right click on the Start Menu and select "System", click “Remote Desktop” on the right of the screen, click "Select users that can remotely access this PC" and allow “Domain Users” access to remote desktop. You can now log into Client-1 VM as a non-administrative user. At a real job, you’d want to do this by creating a Group Policy that allows you to change many systems at once.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a bunch of additional users and attempt to log into client-1 with one of the users
</p>
<br />
