# Active-Directory-Homelab-Project
## Overview

A homelab project simulating a small fictional company's Windows Server Active Directory environment, built in VirtualBox. Created to demonstrate practical IT support/helpdesk skills, directory services administration, Group Policy, access control, and realistic ticket troubleshootings, for an IT support/Helpdesk/sysadmin role.

Two VMS, **DC01** (Windows Server 2022, domain controller) and **CLIENT01** (Windows 11, domain-joined workstation). From a working domain, `corp.homelab.local`. On top of that: an OU structured modeled on a small business, security groups, a permissioned shared folder, domain-wide policy via GPO, and a least-privilege help desk role used to resolve real support tickets, without touching the Domain Admin account. 

***

## Objectives

- Build and romote a functioning AD domain on constrained hardware.
- Apply least-privilege access via OU design, security groups, and delegated permissions.
- Configure Group Policy for both domain-wide and scoped/targeted settings.
- Secure a shared resource with NTFS + share permissions, and prove it with a denied-access test
- Resolve common helpdesk with documented diagnosis, not just fixes.

***

## Table of Contents

- 01 - Lab Architecture
- 02 - Tools and Software Used
- 03 - VM Creation and OS Installation
- 04 - Initial Configuration, Domain Promotion, and DOmain Join
- 05 - Organization Units, Users, Groups and Shared Folder Permissions
- 06 - Group Policy and Delegated Access
- 07 - Helpdesk Scenario Walktroughs