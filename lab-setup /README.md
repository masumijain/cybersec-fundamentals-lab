# Cybersecurity Lab Setup (pfSense + Ubuntu + Kali)

## Overview

This lab simulates a small cybersecurity environment using pfSense as a firewall/router, Ubuntu as a target machine, and Kali Linux as a security testing machine. The setup provides a controlled environment for learning networking, traffic analysis, firewall management, and penetration testing fundamentals.

---

## Required Tools

### Hypervisor

Install one of the following virtualization platforms:

- VirtualBox (Recommended)
- VMware Workstation

### ISO Images

Download the following ISO files from their official websites:

- pfSense Community Edition
- Ubuntu Desktop
- Kali Linux

---

## Creating the pfSense Virtual Machine

### Virtual Machine Configuration

- Type: BSD
- Version: FreeBSD (64-bit)
- Memory: 2 GB
- Processors: 2 CPU Cores

### Network Configuration

#### Adapter 1 (WAN)

- Attached To: Bridged Adapter

#### Adapter 2 (LAN)

- Attached To: Internal Network
- Network Name: `labnet`

---

## Installing pfSense

1. Boot the virtual machine using the pfSense ISO.
2. Proceed with the default installation.
3. Reboot after installation completes.
4. Assign network interfaces:
   - WAN → em0
   - LAN → em1

5. Configure the LAN interface:

```text
IP Address: 192.168.10.1
Subnet Mask: /24
```

6. Enable DHCP on the LAN interface.

The pfSense LAN gateway will be:

```text
192.168.10.1
```

---

## Creating the Ubuntu Virtual Machine

### Virtual Machine Configuration

- Type: Linux
- Version: Ubuntu (64-bit)
- Memory: 2 GB
- Processors: 2 CPU Cores

### Network Configuration

#### Adapter 1

- Attached To: Internal Network
- Network Name: `labnet`

Start the virtual machine and verify network connectivity:

```bash
ip a
```

The system should receive an IP address within:

```text
192.168.10.x
```

Access the pfSense web interface:

```text
https://192.168.10.1
```

---

## Creating the Kali Linux Virtual Machine

### Virtual Machine Configuration

- Type: Linux
- Version: Debian (64-bit)
- Memory: 2 GB
- Processors: 2 CPU Cores

### Network Configuration

#### Adapter 1

- Attached To: Internal Network
- Network Name: `labnet`

Start the virtual machine and verify the assigned IP address:

```bash
ip a
```

Expected output:

```text
192.168.10.x
```

Both Kali Linux and Ubuntu should now be connected behind the pfSense firewall.

---

## Testing Internet Connectivity

Run the following command from Ubuntu or Kali Linux:

```bash
ping 8.8.8.8
```

If connectivity fails:

1. Log in to pfSense.
2. Navigate to:

```text
Firewall → Rules → LAN
```

3. Ensure a rule exists that allows LAN traffic to any destination.

---

## Network Architecture

```text
Internet
   │
Home Router
   │
pfSense (WAN)
   │
pfSense (LAN - 192.168.10.1)
   │
─────────────────────────
│                       │
Ubuntu VM         Kali Linux VM
192.168.10.x      192.168.10.x
```

---

## Learning Outcomes

This lab environment can be used to practice:

- Network traffic analysis
- Nmap scanning techniques
- Firewall rule configuration
- Intrusion Detection and Prevention Systems (IDS/IPS)
- Traffic monitoring and logging
- Basic network segmentation
- VLAN configuration and testing
- Security monitoring fundamentals

---

## Conclusion

Building a cybersecurity lab provides a safe environment for experimenting with networking and security concepts without affecting production systems. This setup establishes a foundation for learning reconnaissance, network defense, traffic analysis, and security testing techniques using industry-standard tools and platforms.
