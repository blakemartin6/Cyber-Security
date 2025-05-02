# 🖥️ Windows Server 2022 Lab: Active Directory, DNS, and DHCP Setup

This lab demonstrates setting up a virtualized Windows Server 2022 environment with Active Directory, DNS, and DHCP. A Windows 10 VM acts as the client machine, joined to the domain to simulate a small network environment.

## 🛠️ Lab Overview

- **Purpose**: Simulate an enterprise-style Windows environment
- **Server OS**: Windows Server 2022  
- **Client OS**: Windows 10  
- **Domain**: `test.lab`  
- **Network**: Host-Only Adapter using `192.168.56.0/24`  

## ⚙️ Configuration Steps

### 🔧 Windows Server 2022 VM

- Set static IP: `192.168.56.1`
- Installed the following roles:
  - Active Directory Domain Services (AD DS)
  - DNS Server
  - DHCP Server
- Promoted the server to a Domain Controller (`test.lab`)
- Created a Reverse Lookup Zone in DNS
- Configured DHCP scope:
  - Start IP: `192.168.56.100`
  - End IP: `192.168.56.200`
  - Subnet mask: `255.255.255.0`
  - Default gateway and DNS server: `192.168.56.1`

### 🧑‍💻 Windows 10 Client VM

- Initially received IP `10.0.2.15` (from default NAT network)
- Switched to Host-Only Adapter — received IP via DHCP or set static IP `192.168.56.101`
- Set DNS to point to the domain controller: `192.168.56.1`
- Attempted domain join:
  - Resolved `test.lab` successfully
  - Encountered error: "You cannot join a computer running this edition of Windows 10 to a domain"
  - Reinstalled with **Windows 10 Pro**
  - Successfully joined domain

## 🗂️ Active Directory Structure

Created a nested OU structure:

```
TestUser/
├── IT/
│   └── ITUser (member of Domain Access group)
└── Staff/
    └── StaffUser (no special group memberships)
```

## 🧪 Troubleshooting Summary

- Could not ping between VMs initially — resolved by switching to Host-Only networking
- Server received a `169.254.x.x` APIPA address — fixed by manually configuring static IP
- DNS resolution failed until DNS was correctly set to the domain controller's IP
- "Destination Host Unreachable" error was resolved after proper IP/DNS configuration
- Couldn’t join domain due to Windows 10 Home edition — fixed by switching to Pro
- After fixing above, `test.lab` domain join succeeded

## ✅ Final Outcome

- Server VM is now a fully functioning domain controller with DNS and DHCP configured
- Windows 10 Pro VM successfully joined the domain
- Created OUs and test users
- Network communication and name resolution are fully functional

## 📂 Folder Location

This project lives under:

```
Cybersecurity/
└── Projects/
    └── windows-server-lab/
        └── README.md
```

## 📝 Skills Practiced

- Active Directory setup  
- DNS and DHCP server configuration  
- OU and user management  
- IP addressing and name resolution  
- Troubleshooting network connectivity and domain issues  
