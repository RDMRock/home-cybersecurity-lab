# Session 02: Ubuntu Server ISO Verification

**Date:** August 2, 2026  
**Status:** Complete

## Objective

Download Ubuntu Server from an official source, verify its integrity, and upload it to Proxmox.

## Verification Result

I calculated the ISO's SHA-256 checksum locally on macOS and compared it character-for-character with Canonical's published checksum.

- Expected:   `dec49008a71f6098d0bcfc822021f4d042d5f2db279e4d75bdd981304f1ca5d9`
- Calculated: `dec49008a71f6098d0bcfc822021f4d042d5f2db279e4d75bdd981304f1ca5d9`
- Result: **PASS — personally verified**

The verified ISO was then uploaded to the Proxmox `local` storage.

## Proxmox Upload

The verified ISO was uploaded to the `local` storage on the Proxmox node. No virtual machine was created during this session.

## Lesson Learned

Checksums are a method of confirming that a downloaded iso matches the file published by the distributor. Validating the checksum ensures that I downloaded the intended file, and am not installing something malicious instead. 

