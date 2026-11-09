# Course network, baselines, and recovery

This page consolidates the build journal and later course-workflow records. It describes documented changes and checks through November 8, 2026. No Proxmox configuration was changed to prepare this page.

## Separation of environments

| Bridge | Recorded role | Important boundary |
| --- | --- | --- |
| `vmbr0` | Proxmox management and the home LAN. The course router's WAN was connected here. | Kali and Windows course targets were connected to the course LAN, not directly to this bridge. |
| `vmbr1` | Independent Ubuntu/Linux practice network without a physical bridge port. | Ubuntu's temporary update adapter was removed, leaving its static isolated interface without a default route at the baseline checkpoint. |
| `vmbr2` | Dedicated course LAN for Kali, Windows 7, and the pfSense LAN interface. | The bridge had no physical port or host IP. pfSense supplied routing, so bridge separation alone does not prove a deny-all firewall policy. |

The course handout described VirtualBox. The workflow record documents permission to use Proxmox and the adaptation of the router and guest images to this topology. Private management addresses, public addresses, MACs, credentials, and connection links are omitted here.

## Completed Linux baseline

The August 5 journal records the updated Ubuntu kernel, active QEMU guest agent, UFW default-deny inbound policy, and SSH restricted to the isolated interface and subnet. After removing the temporary update adapter, the remaining interface and routing table were checked. A powered-off snapshot named `baseline-updated-isolated` was created without RAM.

That is evidence of a checkpoint, not proof that the VM has stayed unchanged since then. The baseline journal supplies the actual observed configuration.

## Course image and disk troubleshooting

The later workflow records importing the router and Kali images, verifying Windows networking, and expanding Kali storage. A disk-resize attempt caused a GRUB boot problem. Rollback restored boot, after which the disk and filesystem were expanded successfully and the old swap arrangement was replaced with a persistent swap file.

Package maintenance also hit repository/network problems and a PyInstaller package transition conflict. The obsolete conflicting package was removed, package configuration was repaired, and the upgrade completed. A post-upgrade powered-off snapshot was recorded.

These are examples of recovery and verification work. The publication does not claim that every current guest or snapshot was freshly inspected.

## Cryptography environment

The course workflow includes configuration of the supplied Xubuntu disk import, and the cryptography reports contain completed Xubuntu exercises. The available setup messages alone do not establish the final Proxmox VM ID or current boot state, so this page does not present those as verified inventory facts.

## What still needs a fresh check

Before another active exercise, confirm guest identity, bridge attachment, routing/firewall state, and recovery point. Historical persistence demonstrations do not prove that every installed test mechanism has subsequently been removed. MFA and device-approval completion were not established by the reviewed public build journal.

Sources: the existing [Ubuntu baseline](session-04-ubuntu-baseline.md), private course-workflow messages, and the [completed coursework reports summarized here](course-lab-investigations.md).
