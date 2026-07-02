# Proxmox Time Synchronization Issue

**Date:** July 01, 2026

## Objective

Proxmox Web UI is booting me from my session every 5 or so minutes. I want to remain in my session and use the CLI without interference.

## Story

Proxmox has been booting me since I started using the web UI a few days ago.
After looking it up, a few forums mentioned something about a timing issue. I thought it was due to my location and the time zone I selected when I installed Proxmox.
To check the time on the machine vs the local time I used the command timedatectl. timedatectl displays the system's: current date and time, time zone, whether the clock is sychronized, and whether network time protocol (NTP) is synchronized. Miraculously, the system time was nearly 3 months behind.
I tried synchronizing the clock, but I quickly realized my host was unable to connect to the internet. During my original install I left my DNS settings as whatever it was populated with.
I navigated to the host's DNS settings and input the correct DNS and tested it a few times to confirm that was the problem by pinging google.com.
That was only part of the problem--I still had to find out why my time was not syncing.
I ran systemctl list-units --type=service | grep -E "chrony|chronyd|ntp|timesync". This string of commands lists all running services and filters the list for common time and sync services. I found the error "illegal attempt to update using time ... when last update time is ..."
I then enabled automatic time sync and restarted chrony.

## Tasks Completed

- Confirmed DNS was not working by pinging 1.1.1.1 and google.com
- Changed DNS server to correct one
- Checked running system services for timesync
- Enabled automatic time sync
- Restarted Chrony

## Commands Used

ping -c 4 google.com
cat /etc/resolv.conf
chronyc tracking
timedatectl
systemctl list-units --type=service | grep -E "chrony|chronyd|ntp|timesync"
timedatectl set-ntp true
systemctl restart chrony

## Lessons Learned

- DNS issues can prevent time synchronization because the server cannot resolve NTP server names.
- Proxmox host DNS should point to reliable infrastructure DNS, such as the router or public DNS, not a VM that may be offline.
- `timedatectl` is useful for quickly checking time zone, local time, NTP status, and clock synchronization.
- Proxmox uses Chrony for time synchronization, so `chronyc tracking` and `chronyc sources -v` are useful troubleshooting commands.
- Incorrect system time can cause Proxmox Web UI/session instability.
- Troubleshooting should separate network connectivity from DNS resolution by testing both an IP address and a domain name.

## Next Steps

- Install Windows Server
- Promote Windows Server to a Domain Controller
- Install Windows Etnerprise
- Practice domain logins, group policy, mapped drives, software deployment, and remote management
