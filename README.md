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
