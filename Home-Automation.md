# Home Automation Project

## Summary
  
   I created a server to control all automated tasks inside my house, including the shared services of my home such as Network-Attached Storage and the Media Server. I used a small form factor Lenovo Thinkcentre and installed a Proxmox hypervisor on it. I then installed multiple Virtual Machines to serve as each of the functions described above. Once all the services were set up, the userbase was sufficiently impressed with the feature set. This is the perennial home server project. 

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

Most of these VMs and containers were taken from [Proxmox VE Helper Scripts](https://github.com/tteck/Proxmox) and modified as needed. Later iterations may just run a Docker instance for the containers (LXCs are presumably less secure), but for now the LXC runs in the hypervisor.

Services:
  - Tailscale

This will provide us the VPN capabilities. By connecting mobile users to the VPN, we can securely connect to relevant servers. Tailscale also can implement ACLs to provide a more robust network and adhere more closely to Zero Trust principles. 
  
##  Research

Resources used in this project:

[Creating a New Home Hacking Lab with Proxmox ](https://mattglass-it.com/proxmox_home_lab/)

## Design 

![](images/Automation_Layout.png)

### Network Design

Once I dug into proxmox's internals, the project became far more complicated. With the abundance of choice afforded by the hypervisor, I had to make design decisions. How to design the architecture? Would I use an additional firewall such as pfsense or rely on Proxmox's internal firewall?

Ultimately I went with a more Agile approach - create the first iteration and then go through, test, and improve again. I implemented a simple star network structure, with each VM connected to the hypervisor and sharing the same subnet. 

The next iteration will place all the services on separate subnet behind a pfsense firewall. This will provide segmentation of this network and additional security. For now, the hypervisor firewall will act as our first line of network defense. 

### Virtual Machines

- Home Assistant VM
- Plex VM
- OpenMediaVault VM
- Unifi controller LXC
    
### Services

- [Tailscale VPN](https://tailscale.com/)

## Implementation

This project went through rather smoothly. Procuring the hardware took less than a week, and the hypervisor installation was easily achieved. Proxmox was installed with no trouble, and then I began the process of installing the virtual machines and containers.

The virtual machines were relatively easy to install. Using the tteck helpers made it simple enough to set up the VMs and the Unifi LXC. I did have trouble understanding exactly how to attach the external storage to the NAS logically. Once I understood that it needed to be mounted in the VM and mapped directly through the hypervisor, it fell into place.

Setting up the Home Assistant became a rabbit hole. Being able to create dashboards that fit any kind of device will mean that I have even more work to do on the details of the Home Assistant server. I may at some point do a write-up explaining how I have Home Assistant set up. Some of the highlights include:

- Map of both floors with indicators and buttons for each smart light
- Server dashboard showing the vital stats with notifications set to ping admin via mobile app when temperature reaches a certain point
- different dashboard permissions for each user
- Multiple layouts for old iPads mounted around the house

## Unexpected Issues

I was not aware of how much research this project was going to require. I had a good handle on the theory and I've worked with virtualization before, but having this particular configuration of software and hardware was new to me. Luckily, proxmox has some excellent community forums and I was able to find nearly everything I needed, especially when mapping the external storage devices through the hypervisor to the NAS. 

I was also not aware of the potential rabbit-holes here. Proxmox was one, and is at time of writing the backbone of my homelab. It's very useful dealing with virtualization locally under the hood. It provides the viewpoint of a datacenter and what cloud providers need to do to keep their systems running.

The other rabbit-hole was Home Assistant. It has a thriving community, and many many addons and scripts to use in setting it up for the average user. The project is one in the category of having non-technical users adopt a technical solution that has an easy to use frontend no matter how complex it has to be on the backend. I was able to set up the existing smart features of my house, and it will be very useful once we move to the new house later this year. I will be able to plan the automation setup from scratch at that point, and this will lead to yet another project. Which is what projects are supposed to do! 

## Conclusion

This was a lot of fun getting set up and I enjoyed learning all the intricate parts of this hypervisor. I've had months and months with this server, and I'm still tinkering with it all the time. I've trained my wife on how to use the Home Assistant App to control the lights, and we were able to watch our own media on a hotel TV while on a business trip in the Bay Area. Those were impressive features that my userbase (wife and kids) were able to understand and use right from the beginning. More projects are on their way, and this was just the beginning.

