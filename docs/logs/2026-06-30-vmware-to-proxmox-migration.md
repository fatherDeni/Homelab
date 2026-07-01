# VMware Workstation to Proxmox Migration

**Date:** June 30, 2026

## Objective

Migrate my Ubuntu Server VM from VMware Workstation running on my gaming PC to my dedicated Proxmox server.

## Tasks Completed

- Installed Proxmox on Dell OptiPlex
- Mounted Windows HDD containing VM files
- Used WinSCP to transfer Ubuntu VM files
- Imported VMware VMDK into Proxmox
- Attached imported disk to VM 100
- Configured boot order
- Successfully booted Ubuntu Server
- Verified login after migration

## Commands Used

```bash
qm importdisk 100 "/root/Ubuntu 64-bit/Ubuntu 64-bit.vmdk" local-lvm
```

## Lessons Learned

- VMware VMs can be migrated without reinstalling the OS.
- Proxmox converts VMware disks into its own storage format.
- WinSCP makes transferring VM files much easier.
- Boot order is critical after importing a disk.
- MAC addresses change after migration, so DHCP reservations may need updating.

## Next Steps

- Verify Docker containers
- Verify AdGuard Home
- Verify Portainer
- Migrate Windows Server
- Configure backups
