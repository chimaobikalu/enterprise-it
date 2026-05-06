# Enterprise IT Lab – Active Directory Environment

## Overview
I simulated an enterprise IT environment for a fictional company, **Velora Logistics Ltd.** I took on 
the role of IT Administrator, setting up the domain, managing users, locking down access, and making sure there's Confidentiality, Integrity, and Availaibility of resources within the company's network.

---

## Objectives
- Get a Domain Controller (DC) up and running on Windows Server
- Sort users into departments using Organizational Units (OUs)
- Set up authentication and enforce security policies
- Connect a client machine to the domain
- Build out file sharing with proper role-based access
- Troubleshot issues and remedied employee challenges

---

## Infrastructure

| Component | Details |
|---|---|
| Domain Name | velora.local |
| Domain Controller | Windows Server 2019 (DC1) |
| Client Machine | Windows 10 |
| Environment | VMware Workstation |

---

## Domain Setup

The first step was configuring a Windows Server and promoting it to a 
Domain Controller, which is the backbone of the whole environment.

- Server name: DC
- Domain: `velora.local`

![Domain Configuration] <img width="1164" height="608" alt="image" src="https://github.com/user-attachments/assets/70bf61a6-8870-49f2-a8cc-b803849d7235" />


---

## Organizational Units (OUs)

For simplicity, I ran the  setup for four departments. So I separated them into Organizational Units (OUs). Four OUs were created:

- Operations
- Finance
- IT
- Support

This keeps things clean and makes it easy to apply policies at the 
department level.

![OU Structure] <img width="1366" height="660" alt="OUs" src="https://github.com/user-attachments/assets/246ebd5e-dc3c-49c0-9991-34c497dd9d9b" />

---

## User Management

Each user was created and placed into their department's OU.

| Name | Department | Role |
|---|---|---|
| Chimaobi Kalu | Operations | Operations Staff |
| Mary Joe | Finance | Finance Staff |
| Chris Eke | IT | IT Administrator |
| Kamsi Ezuma | Support | Customer Support |

![Users in OUs] <img width="1366" height="702" alt="Screenshot (253)" src="https://github.com/user-attachments/assets/fd3fe24e-dc04-4349-8b11-06dc8d84fb57" /> <img width="1366" height="768" alt="Screenshot (254)" src="https://github.com/user-attachments/assets/44f79fa1-3e78-4a2a-9178-0ec2d6239dd2" /> <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/13b25cb9-211d-449c-8b0e-1d834943e412" /> <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/c0f22105-bc78-4f03-8f71-23f1447ef8ed" />

---

## Security Policies

**Account Lockout Policy**

I configured lockout settings to protect against brute force attempts:
- Account locks after 3 failed login attempts
- Lockout lasts 30 minutes
- Failed attempt counter resets after 30 minutes
- Gpupdate /force in Command Prompt to push the update.

![Account Lockout Policy] <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/3b413bf0-6cd1-46f3-b33e-b6d70ad62706" />


**First Login Policy**

Every new user is forced to set their own password the first time they 
sign in — no one keeps the default

## Client Machine Integration

A Windows 10 machine was joined to the domain and tested with actual 
domain user credentials to confirm authentication was working end-to-end.

- Domain: `velora.local`
- Signed in successfully using domain credentials, and prompted to change password.

![Windows 10 Machine Joined to Domain]<img width="1164" height="608" alt="image" src="https://github.com/user-attachments/assets/47d96312-522b-4140-9dc0-4c5b1635ea26" />


![Password Change Prompt]<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/8822d44f-7a55-48cf-b0e2-cbf4e2da5c9e" />

---

## Account Lockout Scenario

An Operations staff forgot his password, entered the wrong one 3 times and got locked out.

![Account lockout] <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/6354cdeb-4bbb-4938-aad5-8432e5edc6e5" />

To restore his account, I went into Active Directory and unlocked it manually. I provisioned a default password and enforced a new password upon logon.

![Account Unlock] <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/362a14d5-18b7-4058-ab42-ff6c5b9df0b9" />


---

---

## File Sharing & Access Control

To ensure secure access to network resources for Velora, I setup shared folders with access controls for each group of employees.

Instead of assigning permissions directly to individual employees, (e.g. Mary Joe), I created a 
**Group** and gave the group access. This way, if the 
team grows, you just add people to the group, no need to touch folder 
permissions every time.

![Group Membership] <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/b2c5eea8-a4f2-4904-ba2c-6b4687ee0b22" />


**NTFS Permissions**

Configured at the file system level — Finance Group gets Read 
and Execute.

![NTFS Permissions] <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/6dc91f87-515a-4c8c-abaa-e339f6b3a9e6" />


**Share Permissions** 

Set at the network share level to complement the NTFS settings.

![Share Permissions] <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/4cd4c8c0-401c-4376-8bfa-1979a8b0c762" />

I also set Function Discovery Network Publication to automatic, and restarted it to ensure my network shares are discovered quicker.

I also opened file manager, went to Network and configured discoverability.

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/fa0a77c6-a057-4d7b-9d2e-c6c641a44742" />


---

## Access Control Testing

**Unauthorized Access**

One of the shared folders on the network was meant for members of the Finance group. A user outside the Finance department tried to open the shared folder.

Result: Access Denied, exactly as intended.

![Access Denied] <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/d423512b-4b80-4fe6-af14-5113ddd1f0f2" />

**Authorized Access**

The Finance user logged in, opened the folder, and found the text file.

![Successful Access] <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/f30078b8-21d2-401d-9d55-04254a13ba8f" />


---

## Project Walkthrough

Full video walkthrough covering the entire build — domain setup, user 
and group management, domain join, and access control testing.

[Watch Video](#)

---

## Tools Used

- Windows Server 2019
- Active Directory Domain Services (AD DS)
- VMware Workstation
- Windows 10

---

## Key Takeaways

Building this from scratch gave me a much stronger understanding of how 
Active Directory actually works in practice, not just theory. Structuring 
users into OUs, enforcing policies, and seeing access control work (and 
fail) in real time made the concepts click in a way that reading about 
them never quite does.
