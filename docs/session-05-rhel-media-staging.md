# Session 05: RHEL Installation Media Staging

**Date:** August 6, 2026  
**Status:** Complete

## Objective

Prepare verified RHEL installation media for the future RHCSA practice environment.

## Installation Media

- Product: Red Hat Enterprise Linux 10.2
- Architecture: x86_64
- Image type: DVD ISO
- Proxmox storage: `local`

The x86_64 image was selected because the Proxmox host supports the x86-64-v3 instruction level required by RHEL 10.

## Integrity Verification

The ISO was first verified on macOS using `shasum -a 256`.

After uploading it to Proxmox, the server-side copy was independently verified using `sha256sum`.

Both calculated values matched Red Hat's published checksum:

`e15cb333529c332e76e4b1b946efe3515c99f996546675aec18e8effdf2540a5`

This confirmed that the installation image matched the official release and was not corrupted during transfer.

## Storage Cleanup

The local Mac copy was removed only after the Proxmox copy passed its own checksum verification. This reclaimed approximately 10.3 GB without risking the only verified copy.

## Next Steps

1. Create the `rhcsa1` virtual machine.
2. Allocate its primary and practice disks.
3. Install and register RHEL.
4. Create the secondary `rhcsa2` machine.
5. Connect both systems to a private practice network.

## Lesson Learned

Simple second pass at verifying the she 256 hashed output both locally and after upload to promos server to verify file integrity.