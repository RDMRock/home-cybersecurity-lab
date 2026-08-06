# Session 04: Ubuntu Update and Isolation Baseline

**Date:** August 5, 2026  
**Status:** Complete

## Objective

Update the Ubuntu target, establish a host firewall policy, install Proxmox guest integration, restore network isolation, and create a known-good baseline snapshot.

## Temporary Connectivity

The Ubuntu target normally uses only the isolated `vmbr1` bridge.

A second VirtIO network adapter connected to `vmbr0` was added temporarily so Ubuntu could reach its official software repositories. The adapter received its configuration through DHCP.

Connectivity was verified in two stages:

1. A numeric public IP address was reached successfully, confirming internet routing.
2. `ubuntu.com` was reached successfully, confirming DNS resolution.

No router port forwarding was configured.

## Firewall Configuration

Before performing updates, UFW was configured with the following policy:

- Deny incoming traffic by default
- Allow outgoing traffic by default
- Allow SSH on `ens18` only
- Restrict SSH sources to `192.168.56.0/24`
- Start UFW automatically during boot

This blocked unsolicited connections through the temporary home-network interface while preserving future SSH access from the isolated lab.

## System Updates

The Ubuntu package indexes were refreshed using `apt update`. The system initially reported 141 upgradeable packages.

The available updates were installed using `apt full-upgrade`. This included a kernel update from `7.0.0-14-generic` to `7.0.0-29-generic`.

After rebooting, `uname -r` confirmed that the system was running kernel `7.0.0-29-generic`.

## Proxmox Guest Integration

The `qemu-guest-agent` package was installed to improve communication between Ubuntu and the Proxmox hypervisor.

The guest agent supports functions such as:

- Reporting guest IP addresses
- Coordinating clean shutdowns
- Improving snapshot and backup consistency
- Communicating guest state to Proxmox

The guest agent is a static systemd service that starts when the appropriate virtual QEMU device is detected.

After rebooting, `systemctl is-active qemu-guest-agent` returned `active`.

Proxmox subsequently displayed the Ubuntu target’s IP address, confirming that communication between the hypervisor and guest agent was working.

## Isolation Restoration

After completing the updates:

1. Ubuntu was shut down cleanly.
2. The temporary `vmbr0` network adapter was removed.
3. The Ubuntu installer ISO was ejected.
4. The VM was restarted.
5. Its interfaces and routing table were inspected.

The final network configuration contained:

- Interface: `ens18`
- Address: `192.168.56.20/24`
- Connected network: `192.168.56.0/24`
- Default route: none

The temporary interface and its home-network and globally scoped addresses were no longer present.

The absence of a default route confirmed that the Ubuntu target could no longer reach the home network or internet.

## Baseline Snapshot

Ubuntu was shut down before the snapshot was created.

A snapshot named `baseline-updated-isolated` was created with RAM excluded.

The snapshot represents a recoverable baseline containing:

- Ubuntu Server 26.04
- Current operating-system updates
- Kernel `7.0.0-29-generic`
- UFW enabled
- SSH restricted to the isolated lab interface and subnet
- QEMU guest agent active
- Static address `192.168.56.20/24`
- Temporary internet connectivity removed
- Installer ISO ejected

## Verification Summary

The following conditions were verified before considering the checkpoint complete:

- The updated kernel was running.
- The QEMU guest agent was active.
- Proxmox could retrieve information from the guest agent.
- UFW denied incoming traffic by default.
- SSH was allowed only on `ens18` from `192.168.56.0/24`.
- The temporary network adapter was removed.
- The isolated static address remained configured.
- No default route remained.
- A powered-off baseline snapshot was created.

## Lessons Learned

Fun little session to finish setting up the ubuntu server and the networking portion within a VM. Creating a snapshot offline was surprisingly easy. Learned about the QEMU guest agent and how it can communicate with the hypervisor.

AI was good at making me verify every step of the process, and explaining the commands as we went through the motions.

