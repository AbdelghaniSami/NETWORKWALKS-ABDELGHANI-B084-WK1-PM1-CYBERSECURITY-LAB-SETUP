# # WK1-PM1 — Cybersecurity Lab Setup

**Program:** Networkwalks Cybersecurity Internship  
**Project:** Week 1 — Project Module 1  
**Author:** Abdelghani Sami  
**Host OS:** Arch Linux with Hyprland  
**Virtualization:** Oracle VirtualBox  
**Testing Machine:** Kali Linux

## 1. Project Overview

This project documents the setup of an isolated cybersecurity testing lab using VirtualBox and Kali Linux.

The goal is to prepare a virtual environment for practicing cybersecurity fundamentals, testing network connectivity, and learning how virtual machines communicate.

## 2. Lab Requirements

| Component | Requirement |
|---|---|
| Host machine | Laptop or PC |
| Hypervisor | Latest recommended VirtualBox version |
| Testing VM | Kali Linux |
| Virtual network | NAT Network |
| Target subnet | `10.0.0.0/24` |
| Kali target IP | `10.0.0.2/24` |
| Internet access | Required |
| VM snapshot | Required |
| Shared folder | Host folder mounted at `/downloads` |

*The IP address and network configuration above are assignment targets. They must be verified against the actual VirtualBox and Kali configuration.*

## 3. Lab Architecture

1. Lab Setup Overview

```text
Arch Linux Host
      |
  VirtualBox
      |
  NAT Network
      |
  Kali Linux VM
      |
  Cybersecurity Practice Lab
```

## 4. Setup Procedure

### Step 1 — Verify VirtualBox

On the Arch Linux host, check the installed version and available virtual machines:

```bash
VBoxManage --version
VBoxManage list vms
VBoxManage list runningvms
```

### Step 2 — Configure the Virtual Network

In VirtualBox, create or configure the NAT Network according to the assignment requirements.

- Network: NAT Network
- Subnet: `10.0.0.0/24`
- Internet access: enabled

Verify the network settings before proceeding.

2. VirtualBox Network Settings

### Step 3 — Import and Configure Kali Linux

Import the Kali Linux virtual machine into VirtualBox.

In the VM settings:

- Configure the network adapter to use the intended NAT Network.
- Enable shared clipboard and drag-and-drop as required.
- Configure the shared folder to be accessible at `/downloads`.

Start Kali Linux and verify its network configuration.

```bash
ip -br address
ip route
```

Confirm the assigned address matches the assignment requirements before marking this step complete.

3. Kali Linux

### Step 4 — Verify Connectivity

From the Kali terminal, run:

```bash
ping -c 4 1.1.1.1
getent hosts kali.org
```

These checks help verify IP connectivity and DNS resolution. Record the results and investigate any failures.


3. Kali Linux


### Step 5 — Verify the Shared Folder

Confirm that the host shared folder is configured and accessible inside Kali Linux at `/downloads`.

Document any permission or VirtualBox Guest Additions issues encountered.

### Step 6 — Create a Snapshot

After confirming the VM is in a working baseline state, shut down or prepare it as appropriate and create a snapshot named:

`WK1-PM1-clean-lab`

This snapshot provides a restore point for future practice.

## 5. Verification Checklist

- [ ] VirtualBox version checked
- [ ] Kali Linux VM imported and started
- [ ] NAT Network configured
- [ ] Kali IP address verified
- [ ] Internet connectivity tested
- [ ] DNS resolution tested
- [ ] Clipboard and drag-and-drop settings checked
- [ ] Shared folder configured and tested
- [ ] Baseline snapshot created
- [ ] Screenshots added as evidence

## 6. Evidence

Add screenshots from your own working environment showing:

1. VirtualBox version and VM configuration.
2. NAT Network configuration.
3. Kali network interface and IP address.
4. Successful connectivity tests.
5. Shared-folder access.
6. Created VM snapshot.

Place each screenshot in the repository and embed it here with Markdown when available.

## 7. Troubleshooting Notes

Document problems encountered during setup, the diagnostic commands used, the solution attempted, and the final result.

Do not claim a fix worked unless you verified it.

## 8. Safety and Ethics

Use this environment only for authorized cybersecurity learning and testing. Test only systems you own or systems for which you have explicit permission.

## 9. References

- [Kali Linux Documentation](https://www.kali.org/docs/)
- [Oracle VirtualBox Documentation](https://www.virtualbox.org/manual/)
- [ArchWiki — VirtualBox](https://wiki.archlinux.org/title/VirtualBox)
