# Session 03: Ubuntu Target VM Build

**Date:** August 3, 2026  
**Status:** In Progress

## Objective

Create an isolated Ubuntu Server virtual machine to serve as the initial target system in the cybersecurity lab.

## Host Validation

Before creating the VM, I verified:

- Architecture: x86_64
- Processor: Intel Core i5-6600K
- x86-64-v3 support: Confirmed
- VM storage available: Approximately 794 GiB
- ISO storage available: Approximately 81 GiB

The CPU verification also confirmed that the host can run future RHEL 10 x86_64 virtual machines.

## Ubuntu VM Configuration

- VM ID: 100
- Name: `ubuntu-target`
- Operating system: Ubuntu Server 26.04 LTS
- CPUs: 2
- Memory: 3 GiB
- Disk: 25 GiB
- Disk storage: `local-lvm`
- Disk controller: VirtIO SCSI
- Network model: VirtIO
- Network bridge: `vmbr1`

## Network Isolation

The VM was connected to `vmbr1`, an isolated Linux bridge with no physical network interface attached.

The VM was not connected to the Proxmox management bridge, `vmbr0`. Consequently, the Ubuntu installer did not receive an address from the home router and installation proceeded without internet access.

## Progress

The VM was successfully created and booted from the previously verified Ubuntu ISO. The Ubuntu installer was started and its proposed LVM storage layout was reviewed.

Installation will be completed during the next session.

## Next Steps

1. Complete Ubuntu installation.
2. Configure the static address `192.168.56.20/24`.
3. Provide controlled temporary internet access for updates.
4. Install and enable the QEMU guest agent.
5. Verify SSH operation.
6. Create a clean baseline snapshot.
7. Create the Kali VM at `192.168.56.10/24`.


## Static Lab Address

The Ubuntu target was assigned `192.168.56.20/24` on its isolated VirtIO interface. No default gateway or DNS server was configured, preventing unintended internet access.
