# Enterprise IT Lab – Active Directory Environment

## Overview
This project simulates a real-world enterprise IT environment for a fictional company, **Velora Logistics Ltd.**
The objective was to design and implement a centralized system for identity management, access control, and basic security using Active Directory Domain Services (AD DS).

---

## Objectives
- Deploy a Domain Controller using Windows Server
- Create and organize users using Active Directory
- Implement Organizational Units (OUs) for departments
- Enforce basic security policies
- Integrate a client machine into the domain
- Configure network file sharing with access control
- Simulate real-world IT support scenarios

---

## Infrastructure

| Component | Details |
|---|---|
| Domain Name | velora.local |
| Domain Controller | Windows Server 2019 (DC1) |
| Client Machine | Windows 10 |
| Environment | VMware Workstation |

---

## Active Directory Structure

Organizational Units (OUs) were created to reflect company departments:

- Operations
- Finance
- IT
- Support

Each department contains assigned users for structured administration and policy management.

---

## Users

| Name | Department | Role |
|---|---|---|
| Chimaobi Kalu | Operations | Operations Staff |
| Mary Joe | Finance | Finance Staff |
| Chris Eke | IT | IT Administrator |
| Kamsi Ezuma | Support | Customer Support |

---

## Security Configuration

**Password Policy**
- Enforced password complexity
- Minimum password length configured

**Account Lockout Policy**
- Lockout after 5 failed login attempts
- Lockout duration: 15 minutes
- Reset counter after: 15 minutes

**First Login Policy**
- Users are required to change password at first login

---

## Client Machine Integration

A Windows 10 client machine was successfully joined to the domain:

- Domain joined: `velora.local`
- Login tested using domain credentials

**Result:** Users were able to authenticate through the domain controller.

**First Login Password Enforcement**
Upon first login, users were prompted:
> "The user's password must be changed before signing in."

- Password successfully updated
- User logged into system using new credentials

---

## File Sharing & Access Control

A shared folder was created to simulate departmental resource access.

**Shared Resource:** `\\DC1\Finance`

**Group-Based Access Control**

Instead of assigning permissions directly to users, a security group was created: **Finance Group**

- Mary Joe added to Finance Group
- Finance Group assigned access to shared folder

**Share Permissions**
- Finance Group → Read & Change access

**NTFS (Security) Permissions**
- Finance Group → Read, Write, Execute

This ensures proper enforcement of access control using both permission layers.

---

## Test Scenarios

**1. Authorized Access**
- Finance user accessed `\\DC1\Finance` successfully
- File created and modified (Payroll.txt)

**2. Unauthorized Access**
- Non-finance users attempted access
- Result: Access Denied

**3. Account Lockout**
- Multiple failed login attempts triggered lockout
- Account unlocked via Active Directory

---

## Screenshots

| | |
|---|---|
| Active Directory Structure | *(Add screenshot)* |
| Users & OUs | *(Add screenshot)* |
| Group Membership | *(Add screenshot)* |
| Folder Permissions | *(Add screenshot)* |
| Access Denied | *(Add screenshot)* |
| Successful Access | *(Add screenshot)* |

---

## Project Walkthrough

A full walkthrough demonstrating:
- Active Directory setup
- User and group management
- Domain join process
- File sharing and permission testing

[Watch Video](#)

---

## Tools Used

- Windows Server 2019
- Active Directory Domain Services (AD DS)
- VMware Workstation
- Windows 10

---

## Key Takeaways

- Implemented centralized identity management using Active Directory
- Applied role-based access control using security groups
- Configured and enforced security policies
- Integrated client systems into a domain environment
- Tested and validated real-world IT scenarios


