# Home Automation Project

## Summary
  In this project, I created a server to control all automated tasks inside my home, including the shared services of my home such as Network-Attached Storage and the Media Server. I used a small form factor Lenovo Thinkcentre and installed a Proxmox hypervisor on it. I then installed multiple Virtual Machines to serve as each of the functions described above. 

## Purpose

  This is a project that is ongoing in my household. I have been constantly building and re-building the home server for nearly 15 years by this point. I have had it on a large ATX box, a Raspberry Pi, and a Mac Mini. This iteration is easier in design but more complex in implementation. However, this version of the home server will add on new features.

   ### Existing Feature List
   - Media Server
   - Media Storage

   ### New Features
   - Home Automation Hub to control IoT devices and provide reports 
   - Network Attached Storage that is RAID ready for further expansion
   - UniFi controller software to control the Ubiquiti network devices present without utilizing the cloud
   - Personal VPN for use when family members are mobile


## Material List

Hardware: 
  - Lenovo Thinkcentre m970q
    - 32 GB Ram
    - 1TB SSD
    - Gigabit Internet Connection
  - 5 TB Seagate External HDD

The Thinkcentre was sourced via Amazon, but one could look on eBay for multiples if budget is a concern. However, supply chain security does need to be taken into account.

Software:
  - Proxmox Hypervisor
    - Home Assistant VM
    - Plex VM
    - OpenMediaVault VM
    - Unifi controller container

Most of these VMs and containers were taken from https://github.com/tteck/Proxmox and modified as needed. Later iterations may just run a Docker instance for the containers (LXCs are presumably less secure), but for now the LXC runs in the hypervisor


Services:
  - Tailscale

        
        
