# cybersecurity-lab-setup-week1

Virtual cybersecurity lab setup using VirtualBox and Kali Linux — Week 1, NetworkWalks Cybersecurity Program

# 🖥️ Cybersecurity & Pentesting Lab Setup

**NetworkWalks | WK1-PM1 | Tools: VirtualBox + Kali Linux**

## 📌 Project Overview

This project documents the setup of a virtual cybersecurity and penetration-testing laboratory as part of the NetworkWalks Cybersecurity Internship.

The lab uses Oracle VirtualBox to run Kali Linux in a virtualized environment for cybersecurity learning, network testing, reconnaissance, and authorized security assessments.

The goal is to establish a reliable testing environment that can be expanded with additional virtual machines for future exercises, while keeping security testing within an authorized lab environment.

## 🎯 Objectives

- Install and configure Oracle VirtualBox.
- Create a dedicated NAT Network for the lab.
- Import and configure Kali Linux as the testing machine.
- Configure the required virtual network and IPv4 address.
- Verify internet connectivity and DNS resolution.
- Enable clipboard and drag-and-drop integration.
- Configure a host shared folder accessible at `/downloads`.
- Create a clean virtual machine snapshot for recovery.
- Document the configuration, verification steps, and troubleshooting process.

## ⚙️ Lab Configuration

| Component | Configuration |
|---|---|
| Host OS | Arch Linux with Hyprland |
| Hypervisor | Oracle VirtualBox |
| Security OS | Kali Linux 2026.3 |
| Virtual Network | NAT Network |
| Required Network Prefix | `10.0.0.0/24` |
| Required Kali IP | `10.0.0.2/24` |
| Expected Gateway | `10.0.0.1` |
| DNS | Verify against the actual configuration |
| Shared Folder | `/downloads` |
| Clipboard | Enabled as required |
| Drag-and-Drop | Enabled as required |
| VM Snapshot | Clean baseline snapshot |

**Note:** The IP address, gateway, DNS, shared folder, and integration settings must be checked against the running VM. The values above describe the assignment target, not proof that every setting is already configured.

## 🪜 Lab Setup Procedure

### Step 1. Prepare the Host Environment

Prepared the Arch Linux host for virtualization and confirmed that VirtualBox was installed.

The host system provides the environment in which the Kali Linux virtual machine runs.

### Step 2. Install and Verify VirtualBox

Installed Oracle VirtualBox using the available Arch Linux package manager and checked that the VirtualBox management utility was accessible.

Useful verification commands:

```bash
VBoxManage --version
VBoxManage list vms
```

These commands help confirm the installed VirtualBox version and list registered virtual machines.

### Step 3. Create the NAT Network

Configured a dedicated NAT Network in VirtualBox to meet the assignment's network requirements.

**Required network configuration:**

- Network mode: NAT Network
- IPv4 prefix: `10.0.0.0/24`
- Kali Linux address: `10.0.0.2/24`

A NAT Network is suitable for a lab where multiple virtual machines may need to communicate with one another while using outbound internet connectivity.

The network name and DHCP configuration should match the settings actually saved in VirtualBox.

### Step 4. Import and Configure Kali Linux

Registered and started the Kali Linux virtual machine in VirtualBox.

Checked the virtual machine's network adapter configuration to ensure that it was attached to the lab's NAT Network rather than an unintended network mode.

The Kali VM serves as the primary testing machine for this project.

### Step 5. Configure the Kali Linux Network

Configured the Kali Linux network interface according to the assignment's required subnet and IP address.

Target IPv4 configuration:

```text
IP Address:   10.0.0.2
Subnet Mask:  255.255.255.0 (/24)
Gateway:      10.0.0.1
DNS:          Verify actual configured server
```

Network configuration can be inspected using:

```bash
ip address
ip route
nmcli connection show
```

If the NetworkManager connection requires reactivation after a configuration change, use the actual connection name shown by `nmcli connection show`:

```bash
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

Replace `"Wired connection 1"` if your connection has a different name.

### Step 6. Configure Shared Resources and Integration

Checked the VirtualBox integration settings required by the assignment:

- Shared clipboard.
- Drag-and-drop.
- Host shared folder mounted or accessible at `/downloads`.

These features should be tested from inside Kali Linux rather than assumed to work solely because they are enabled in the VM settings.

### Step 7. Create a Clean VM Snapshot

After confirming that the network and required integration features work, create a baseline snapshot from VirtualBox.

**Suggested snapshot name:** `Clean setup - network configured`

A baseline snapshot provides a recovery point before future lab exercises or configuration changes.

## 🔎 Lab Verification

The following checks can be used to validate the setup.

| Test | Command or action | Expected result |
|---|---|---|
| Check IP address | `ip address` | Required address appears on the active interface |
| Check routing | `ip route` | Expected default route is present |
| Test gateway | `ping -c 4 10.0.0.1` | Replies if the configured gateway is reachable |
| Test internet by IP | `ping -c 4 1.1.1.1` | Replies if outbound connectivity is working |
| Test DNS | `getent hosts google.com` | A result is returned |
| Test shared folder | Inspect `/downloads` | Shared files are accessible |
| Test snapshot | Check VirtualBox snapshots | Baseline snapshot is present |

Record the real results after running each test. A failed ping does not always prove that the network is completely unavailable, because some destinations may block ICMP traffic.

## 🐞 Problems Encountered & Solutions

Use this section to document problems that actually occurred during your setup. Include the error, the cause if known, the fix, and the verification result.

### Problem 1. VirtualBox Kernel Modules

On Arch Linux, VirtualBox may require compatible kernel modules before virtual machines can start.

**Verification commands:**

```bash
uname -r
lsmod | grep -E 'vboxdrv|vboxnet'
```

If a kernel-module problem occurs, check the installed kernel, the matching VirtualBox host modules or DKMS package, and the relevant system logs before applying a fix.

### Problem 2. Kali Linux Network Connectivity

If Kali Linux cannot reach the gateway or internet, check the configuration in this order:

1. Confirm the VM is running and its virtual network adapter is enabled.
2. Confirm the adapter is attached to the intended NAT Network.
3. Check the NAT Network subnet and gateway settings in VirtualBox.
4. Inspect Kali's IP address and routing table.
5. Test gateway connectivity, internet connectivity, and DNS separately.

Document the specific error and the verified solution if a problem occurs.

### Problem 3. Static IP Not Applying

If Kali Linux continues to show an unexpected IP address after changing IPv4 settings, inspect the active NetworkManager connection and its configuration:

```bash
nmcli connection show
nmcli device status
ip address
ip route
```

Reactivate the correct connection if necessary, then verify the address and route again.

### Problem 4. Shared Folder Not Accessible

If `/downloads` is not accessible from Kali Linux, check the VirtualBox shared-folder configuration, the configured mount point, and the guest integration requirements.

Record the actual error and fix once verified.

## 💡 What I Learned

- **Virtual networking:** How a dedicated NAT Network can support communication between virtual machines while allowing outbound connectivity.
- **Linux network configuration:** How to inspect interfaces, routes, and NetworkManager connections.
- **Layer-by-layer troubleshooting:** How to investigate adapter settings, addressing, routing, internet access, and DNS separately.
- **Virtual machine snapshots:** Why a clean baseline is useful before making changes during security exercises.
- **Lab documentation:** Why recording actual configuration and test results makes a technical project easier to reproduce and troubleshoot.

## 🔐 Security & Ethical Use

This laboratory is intended for educational cybersecurity practice and authorized testing. Any assessment outside the lab must be performed only on systems for which explicit permission has been obtained.

## 🔗 Tools & Resources

- [NetworkWalks](https://networkwalks.com/)
- [Oracle VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads)
- [Kali Linux Downloads](https://www.kali.org/get-kali/)
- [Kali Linux Documentation](https://www.kali.org/docs/)
- [ArchWiki — VirtualBox](https://wiki.archlinux.org/title/VirtualBox)

## 👤 Author

**Abdelghani Sami**  
Cybersecurity Student — NetworkWalks Cybersecurity Internship

## 📌 Project Information

- **Program:** NetworkWalks Cybersecurity Internship
- **Week:** 01
- **Project:** WK1-PM1 — Cybersecurity Lab Setup
- **Environment:** Arch Linux, Oracle VirtualBox, Kali Linux

---

**Project Status:** Update this status after verifying the required network configuration, connectivity, shared folder, integration settings, and baseline snapshot.
