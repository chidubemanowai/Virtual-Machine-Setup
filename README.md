# Azure VM Remote Access Configuration Report

## Overview

This project documents the setup and verification of remote access to an Azure Virtual Machine using Remote Desktop Protocol (RDP) for Windows or Secure Shell (SSH) for Linux.

## Environment Details

* Cloud Platform: Microsoft Azure
* VM Type: Windows/Linux Virtual Machine
* Access Method:

  * Windows: Remote Desktop Protocol (RDP)
  * Linux: Secure Shell (SSH)

## Connection Process

### Windows VM (RDP)

1. Verified that the VM was running in the Azure Portal.
2. Located the VM Public IP address.
3. Configured the Network Security Group (NSG) to allow inbound TCP port 3389.
4. Restricted access to approved source IP addresses.
5. Opened Remote Desktop Connection.
6. Connected using administrator credentials.
7. Verified access to the Windows desktop.

### Linux VM (SSH)

1. Verified that the VM was running.
2. Retrieved the Public IP address.
3. Configured the NSG to allow inbound TCP port 22.
4. Connected using SSH authentication:

   * Password authentication, or
   * SSH key-based authentication.
5. Verified access by running Linux commands.

## Verification Commands

### Linux

```bash
hostname
whoami
uname -a
df -h
```

### Windows

```cmd
hostname
whoami
systeminfo
ipconfig
```

## Network Security Group Configuration

| Rule Name | Protocol | Port | Source Restriction         | Action |
| --------- | -------- | ---- | -------------------------- | ------ |
| Allow-RDP | TCP      | 3389 | Approved Public IP Address | Allow  |
| Allow-SSH | TCP      | 22   | Approved Public IP Address | Allow  |

## Security Measures Implemented

* Restricted inbound access to trusted IP addresses.
* Avoided exposing management ports to all internet traffic.
* Verified successful remote access before completing configuration.
* Terminated remote sessions after administration tasks.

## Troubleshooting Steps

Common issues encountered:

### RDP Connection Failure

* Confirmed VM was running.
* Verified public IP address.
* Checked NSG rule for TCP port 3389.
* Confirmed administrator credentials.

### SSH Connection Failure

* Verified port 22 access.
* Checked SSH key permissions.
* Confirmed correct username and IP address.

# Virtual Machine Hardware Configuration

## Windows VM Configuration

| Configuration Item | Details |
|---|---|
| Operating System | Windows Server |
| VM Size | Standard_B2s |
| vCPUs | 2 |
| Memory | 4 GiB |
| Storage Type | Premium SSD |
| OS Disk Type | Managed Disk |
| Disk Size | 128 GB |
| Network | Azure Virtual Network |
| Remote Access | RDP / Azure Bastion |

---

## Linux VM Configuration

| Configuration Item | Details |
|---|---|
| Operating System | Ubuntu Linux |
| VM Size | Standard_B2s |
| vCPUs | 2 |
| Memory | 4 GiB |
| Storage Type | Premium SSD |
| OS Disk Type | Managed Disk |
| Disk Size | 30 GB |
| Network | Azure Virtual Network |
| Remote Access | SSH / Azure Bastion |

---

## Storage Configuration

The virtual machines use Azure Managed Disks with Premium SSD storage to provide reliable and high-performance disk operations.

Storage details:

- Disk Type: Premium SSD
- Disk Management: Azure Managed Disk
- OS Disk: Attached to each VM
- Performance Tier: Based on selected disk size and VM configuration

---

## Hardware Verification

The VM hardware configuration was verified through the Azure Portal:

**Azure Portal → Virtual Machine → Overview → Size**

**Azure Portal → Virtual Machine → Disks**

## Conclusion

The Azure VM was successfully accessed remotely, security rules were configured, and access was restricted to authorized sources only.
