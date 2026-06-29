# Network Security Group (NSG) Configuration Details

## Overview

The Azure Network Security Group (NSG) was configured to secure remote access to the Azure Virtual Machines. Inbound access was limited to trusted source IP addresses while allowing only the required management ports.

## NSG Rules Implemented

| Rule Name | Protocol | Port | Source IP Restriction | Action | Purpose |
|---|---|---|---|---|---|
| Allow-RDP | TCP | 3389 | Authorized Public IP (/32) | Allow | Windows Remote Desktop Access |
| Allow-SSH | TCP | 22 | Authorized Public IP (/32) | Allow | Linux SSH Access |

## Rule Configuration

### Windows VM (RDP)
Protocol: TCP
Port: 3389
Source: <Authorized-Public-IP>/32
Action: Allow

Allows approved administrators to connect to the Windows VM using Remote Desktop Protocol.

### Linux VM (SSH)
Protocol: TCP
Port: 22
Source: <Authorized-Public-IP>/32
Action: Allow

Allows approved administrators to securely access the Linux VM through SSH.

## Security Controls Applied

- Restricted inbound traffic to trusted IP addresses.
- Removed unrestricted access (`0.0.0.0/0`).
- Allowed only required remote management ports.
- Verified successful RDP and SSH connections after configuration.

## Verification

Windows RDP:
- Confirmed access using Remote Desktop on port 3389.

Linux SSH:
- Confirmed access using SSH on port 22.

Verification commands:

Linux:
```bash
hostname
whoami
