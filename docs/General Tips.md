# General Tips

## Configuring Connections Between Hypervisors

- **VirtualBox:**
  
  - Create a **VirtualBox Host-Only Ethernet Adapter**.
  - IPv4 address and netmask are assigned automatically.
  - Disable the DHCP server.

- **VMware:**
  
  - Open **Virtual Network Editor** → select an existing network or create a new **bridged network** (e.g., **VMnet0**).
  - Bridge to: **VirtualBox Host-Only Ethernet Adapter**.
  - Change the network interfaces of VMware VMs to VMnet0.

- **srv-ops01:**
  
  - Change the interface responsible for the 192.168.60.11 network gateway to **Isolated network card (host-only) – VirtualBox Host-Only Ethernet Adapter**.
