# Azure VM Remote Access Troubleshooting Guide

## Overview

This document records common issues encountered while establishing remote access to an Azure Virtual Machine using Remote Desktop Protocol (RDP) for Windows and Secure Shell (SSH) for Linux. It also documents the steps taken to resolve connectivity and configuration problems.

---

## Issue 1: Unable to Connect Through RDP (Windows VM)

### Symptom

The Remote Desktop client failed to connect to the Windows VM.

### Possible Causes

* VM was not running.
* Incorrect Public IP address was used.
* Network Security Group (NSG) did not allow inbound TCP port 3389.
* Incorrect administrator credentials.
* ReadOnly lock prevented NSG modification.

### Troubleshooting Steps

1. Verified that the VM status was **Running** in the Azure Portal.
2. Confirmed the VM Public IP address.
3. Checked the Network Security Group inbound rules.
4. Added an inbound rule allowing:

   * Protocol: TCP
   * Port: 3389
   * Source: Trusted public IP address only
   * Action: Allow
5. Verified that the correct administrator username and password were used.
6. Retested the RDP connection.

### Resolution

The RDP connection was successful after updating the NSG rule to allow TCP port 3389 from the authorized source IP address.

---

## Issue 2: Unable to Connect Through SSH (Linux VM)

### Symptom

The SSH client returned a connection failure or timeout error.

### Possible Causes

* SSH port 22 was blocked.
* Incorrect username.
* Incorrect SSH key.
* Incorrect file permissions on the private key.
* VM Public IP address was incorrect.

### Troubleshooting Steps

1. Verified the VM was running.
2. Confirmed the assigned Public IP address.
3. Checked the NSG inbound rules.
4. Allowed inbound SSH traffic:

   * Protocol: TCP
   * Port: 22
   * Source: Authorized IP address only
5. Verified SSH username.
6. Confirmed the correct private key was used.

Example connection command:

```bash
ssh -i private-key.pem azureuser@<public-ip-address>
```

### Resolution

The SSH connection was established successfully after correcting the NSG configuration and authentication details.

---

## Issue 3: Resource Was Read-Only

### Symptom

Attempting to modify VM networking settings returned a read-only error.

### Possible Causes

* A ReadOnly resource lock was applied.
* User account lacked sufficient Azure permissions.

### Troubleshooting Steps

1. Checked the resource, resource group, and subscription for locks.
2. Reviewed Azure role assignments.
3. Confirmed that the account had appropriate permissions.
4. Removed the ReadOnly lock after obtaining the required authorization.

### Resolution

The resource became editable after the lock was removed or appropriate permissions were assigned.

---

## Issue 4: Connection Timeout

### Symptom

The remote connection timed out.

### Troubleshooting Steps

* Verified the VM was online.
* Confirmed the Public IP address was correct.
* Checked NSG inbound rules.
* Confirmed the correct port was open:

  * Windows: TCP 3389
  * Linux: TCP 22
* Tested connectivity again.

### Resolution

The issue was resolved after correcting the network security configuration.

---

## Security Improvements Implemented

* Restricted inbound access to specific trusted source IP addresses.
* Removed unnecessary open internet access rules.
* Used SSH keys where possible for Linux authentication.
* Closed remote sessions after completing administration tasks.
* Regularly reviewed NSG rules.

---

## Final Status

Remote access to the Azure VM was successfully configured and verified. The VM was accessible through RDP or SSH, and security controls were applied to restrict unauthorized access.
