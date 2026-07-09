# Windows 11 Enterprise Deployment

**Date:** July 08, 2026

## Objective

Create a Windows VM to promote to my DC so that I can learn active directory, and practice group policy, mapped drives, software deployment, and remote management.

## Story

Top to bottom:
I filled out the fields on Windows website to obtain a download link to Windows Enterprise. I copied the link and pasted it into my Proxmox drive that stores my ISO images. Then, I clicked create a VM, filled out the hardware fields, and created my Windows VM. But... for some reason it was stuck on a black screen once it booted. I didn't entirely narrow down the problem. Instead, I decided I'd start from scratch and really watch a tutorial on how to install it. So, I deleted the server and watch a tutorial.
After watching the tutorial, I realized I had several settings all mixed up... mostly because I wasn't paying super close attention, and I didn't know what I was doing.
You can't choose Linux as the OS when you deploy a Windows ISO to a VM... lol. Also, Proxmox VMs need a driver ISO to communicate with Windows. The reason is because Windows does not have built in drivers for VirtIO devices. I made my way to the VirtIO GitHub, downloaded the ISO, and added it to a seperate virtual CDROM.
When I loaded into Windows 11, there was no drive. I realized then I had to browse the VirtIO CDROM ISO file and install the network driver and SCSI controller.

## Tasks Completed

- Uploaded Windows Enterprise ISO to Proxmox via link
- Uploaded VirtIO drivers via GitHub download and manual upload
- Created Windows 11 Enterprise VM
- Loaded VirtIO drivers from secondary virtual CDROM

## Lessons Learned

- Learn before doing: don't "rawdog" the install for something
- Virtual machines do not have an inherent way to speak to Windows, that is why the VirtIO drivers are necessary.
- Windows 11 needs 4gb of ram for the install
- How to upload ISO images via download link to Proxmox
- How to correctly install Windows 11 enterprise

## Next Steps

- Promote Windows Server to a Domain Controller
- Create an image of the newest Windows Enterprise server so that I can deploy a Windows 11 client to my arsenal
- Practice domain logins, group policy, mapped drives, software deployment, and remote management
