
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

Microsoft Active Directory Deployed in the Cloud with Microsoft Azure.
This tutorial outlines the implementation of Microsoft Active Directory with Microsoft Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- Deploying Microsoft Active Directory within Microsoft Azure https://www.youtube.com/watch?v=LR8009GgGAQ

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop Connection
- Microsoft Active Directory Domain Services
- PowerShell Ise

<h2>Operating Systems Used </h2>

- Domain Controller Virtual Machine (DC-1). Windows Server 2022
- Client 1 Virtual Machine (Client-1). Windows 10 Pro

<h2>High-Level Deployment and Configuration Steps</h2>

- Install Active Directory
- Create a Domain Admin User within the Domain
- Join Client-1 Virtual Machine to the domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on the Client-1 Virtual Machine
- Create additional Non-Administrative Users and attempt to log into Client-1 Virtual Machine with one of the new users



<h2>Deployment and Configuration Steps</h2>

<p>

![add roles and features](https://github.com/user-attachments/assets/e304d5ee-fce9-4b9d-b7e8-e148696c921e) ![Install ADDS](https://github.com/user-attachments/assets/2543fd29-1010-4c59-8785-7fe548d6ad00) ![adding  client-1 to the domain](https://github.com/user-attachments/assets/67bb888f-8c85-4d79-b47f-383b8fac5d67)

  
</p>
<p>
Installing Active Directory. From the Domain Controller (DC-1) virtual machine, open Server Manager and click "Add Roles and Features", install Active Directory Domain Services. In the third screenshot, we select "Rename this PC (advanced)", Promote as a Domain Controller: Setup a new forest as "mydomain.com" (can be anything). Restart the Domain Controller virtual machine and log back in as username: "mydomain.com\labuser".
</p>
<br />

<p>

![create jane doe](https://github.com/user-attachments/assets/4f8eb0fc-d6f2-4943-908b-75a7082cb274) ![jane as domain admins](https://github.com/user-attachments/assets/872a2324-fcd9-439b-9f58-cac5cb5258c4)

</p>
<p>
Creating a Domain Admin user within the Domain, In Active Directory Users and Computers (ADUC), create two Organizational Units (OU) called “_EMPLOYEES” and “_ADMINS” by right clicking on my domain, hover over "New", and click "orgizational unit". Create a new employee named “Jane Doe”, for example, with the username of “jane_admin”. Add jane_admin to the “Domain Admins” Security Group. Finally, log out and close the connection to the Domain Controller virtual machine and log back in as “mydomain.com\jane_admin”. This would become the main Administrative account for the Domain.    
</p>
<br />

<p>

![client-1 as part of the domain](https://github.com/user-attachments/assets/e3235c44-beeb-48bd-811c-ff7ef1b743b4) ![client-1 dragged into clients OU](https://github.com/user-attachments/assets/0ddbb558-9160-456e-9812-851093990baf)

</p>
<p>
Joining Client-1 Virtual machine to the Domain. Login to the Client-1 virtual machine as the original local administrator and join it to the domain... (computer will restart). Login to the Domain Controller virtual machine and verify that Client-1 virtual machine shows up in Active Directory Users and Computers. Create a new Orgizational Unit (OU) named “_CLIENTS” and drag Client-1 into the newly created Orgizational Unit. 
</p>
<br />

<p>

![allowing domain users remote desktop](https://github.com/user-attachments/assets/3e956cd5-5294-4f8f-bd1c-f6b3cd4257fa)

</p>
<p>
Setup Remote Desktop Connection for non-administrative users on Client-1 virtual machine. Login to the Client-1 virtual machine as "mydomain.com\jane_admin". Right click on the "Start" menu and select "System", click “Remote Desktop” on the right of the screen, click on "Select users that can remotely access this PC" and allow “Domain Users” access to Remote Desktop Connection. You can now log into Client-1 virtual machine as a non-administrative user. At a real job, you’d want to do this by creating a Group Policy that allows you to change many systems at once.

</p>
<br />

<p>

![creating users in powershell](https://github.com/user-attachments/assets/682f42aa-8854-497f-ad40-626dcd6fddf2)

</p>
<p>
Creating additional non-administrative users and login to Client-1 virtual machine as one of the new users. Login to the Domain Controller virtual machine as a Domain Admin. Open PowerShell_ise as an administrator. Create a new file and paste the contents of the script into it. Run the script and observe the accounts being created. When finished, we open Active Directory Users and Computers and observe the accounts under "_EMPLOYEES". We now have the ability to login to the Client-1 virtual machine as one of the new aon-administrative accounts. Every non-administrative account was created with the same password.   
</p>
<br />

<p>

![viewing new users](https://github.com/user-attachments/assets/60b1ec57-935a-4f50-8ea3-ddb38d92d2f5)

</p>
<p>
Under the "_EMPOLYEES" tab, we can now see the newly created non-administrative accounts. This concludes the Deployment of Microsoft Active Directory in the Cloud with Microsoft Azure!   
</p>
<br />
