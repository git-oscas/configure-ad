<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of Active Directory within Azure Virtual Machines.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup & configure resources in Azure
- Ensure connectivity between client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client to domain
- Setup Remote Desktop for non-administrative users on client
- Create a bunch of additional users and attempt to log into client with one of the users

<h2>Deployment and Configuration Steps</h2>

![image](https://github.com/git-oscas/configure-ad/assets/156957308/b5a1fae0-b146-41f5-867e-e0ae01f2abb9)

After setting up both VMs ("Client-1: Windows 10 Pro" & "DC-1: Windows Server 2022 Datacenter"), configure DC-1's NIC Private IP address from "dynamic" to "static"

![image](https://github.com/git-oscas/configure-ad/assets/156957308/6075056a-3cfa-4f32-a5ff-6a251abe6caa)

After enabling IMCP requests within VM "DC-1", go into VM "Client-1" and ping VM "DC-1" to test connectivity between the two VMs (ping should be succesful)

![image](https://github.com/git-oscas/configure-ad/assets/156957308/dfe5b65d-452f-4951-b0ba-67ad12ddff99)
![image](https://github.com/git-oscas/configure-ad/assets/156957308/56be4c0f-c5d0-4794-96ad-cabfae50c413)


Inside VM "DC-1", install Active Directory Domain inside the Server Manager Panel to setup roles and features inside the wizard

After installation is complete, promote as a DC, and setup a new forest

Restart, then log back into VM "DC-1"

![image](https://github.com/git-oscas/configure-ad/assets/156957308/979ee685-111f-41cf-b087-f24e13393fa2)
![image](https://github.com/git-oscas/configure-ad/assets/156957308/fb21fbc7-0f8f-4abc-abcc-921dfa9195c8)
![image](https://github.com/git-oscas/configure-ad/assets/156957308/c9718a9b-613c-44f3-8d91-c95856db2d43)


In Active Directory Users and Computers (ADUC), create TWO Organizational Units (OU) called "_EMPLOYEES" & "_ADMINS"

Inside OU "_ADMINS", create a user "jane doe" (username: jane_admin), and add "jane doe" to the "Domain Admins" Security Group

Log out of Remote Desktop Connection to VM "DC-1" and log back in with "jane doe"'s credentials (user "jane_admin" as admin account from now on)

![image](https://github.com/git-oscas/configure-ad/assets/156957308/5f55f9e5-fdd5-47cb-afb5-17cd57e2c713)
![image](https://github.com/git-oscas/configure-ad/assets/156957308/3fceea8d-1780-4751-8baa-47276782eb2a)
![image](https://github.com/git-oscas/configure-ad/assets/156957308/57de349c-60fb-44f1-92ea-40c1f4a42077)

From Azure Portal, set VM "Client-1"'s DNS settings to VM "DC-1"'s private IP address then reset VM "Client-1" within Azure Portal

Login to VM "Client-1" as original local admin and join it to the domain (computer will restart)

Inside VM "DC-1", verify VM "Client-1" shows up in Active Directory Users and Computers inside the "Computers" container on the root of the domain

![image](https://github.com/git-oscas/configure-ad/assets/156957308/17948406-270b-483b-a727-dd78f330faae)

Login to VM "Client-1" with "jane doe"'s credentials and open System Properties, click "Remote Desktop", and allow "Domain Users" access to remote desktop

Non-Administrative users can now login to VM "Client-1"

![image](https://github.com/git-oscas/configure-ad/assets/156957308/dc0ab727-bf57-4c67-9379-62c7c7dbc8aa)
![image](https://github.com/git-oscas/configure-ad/assets/156957308/22e9f3d3-289e-429c-9aff-3309977d520a)

(used a script to add random users into OU "_EMPLOYEES")

Inside VM "DC-1" (logged in as "jane_admin"), open Active Directory Users and Computers, and open OU "_EMPLOYEES" and attempt to login to VM "Client-1" with one of the randomly generated users 

"baj.mip" is used for this demo and login is successful into VM "Client-1" using "baj.mip"'s credentials
