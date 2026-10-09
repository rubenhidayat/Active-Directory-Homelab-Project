# 01 - Lab Architecture

## Topology


|VM|Role|OS|RAM|vCPU|Static IP|
|---|---|---|---|---|---|
|DC01|Domain Controller / DNS|Windows Server 2022 (Server Core)|2 GB|2|192.168.10.1|
|CLIENT01|Workstation|Windows 11 Enterprise|4 GB|2|192.168.10.20|

**Domain**: `corp.homelab.local`, (NetBIOS: `corp`), **Hypervisor**: Oracle VirtualBox, **Network** VirtualBox Internal Network (`intnet`) isolated from the host's LAN and internet.

***

## Network Diagram

```
                    intnet (192.168.10.0/24)
   ┌───────────────────────┬───────────────────────────┐
   │        DC01           │       CLIENT01            │
   │  192.168.10.1         │   192.168.10.20           │
   │  Server 2022 Core     │   Windows 11 Enterprise   │
   │  AD DS + DNS          │   RSAT, domain-joined     │
   └───────────────────────┴───────────────────────────┘
```

CLIENT01 points its DNS at DC01; DC01 is self-referencing and authoritative for `corp.homelab.local`.

***

## Directory Structure

```
corp.homelab.local
├── CORP-Departments
│   ├── IT / Sales / HR / Finance
│   │   ├── Users
│   │   └── Workstations
├── CORP-Groups
└── CORP-ServiceAccounts
```

Modeled on a small business with four departments. Groups are kept in their own OUs, OU placement and group membership are deliberately treated as two different things throughout this project.

***

## Account Model


|Account|Used for|
|---|---|
|`CORP\Administrator`|Domain promotion, OU/GPO design, domain policy — structural work only|
|`GG-IT-Users` (delegated)|All day-to-day helpdesk tickets: account creation, password resets, unlocks, group changes|

***

## Why These Choices

Built on 16 GB RAM host where two full-desktop VMS had already caused lag. That constraint drove the real decision here:

- **Server Core for DC01** — smaller footprint, administered remotely via RSAT from CLIENT01, matching how production DCs are actually managed
- **Tight VM sizing** — 2 GB / 4 GB, 2 vCPU each, audio/USB disabled, no 3D acceleration
- **One DC, one client** — covers the full scope of AD administration and helpdesk scenarios without exceeding the hardware budget
