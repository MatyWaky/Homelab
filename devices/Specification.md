# Specification

- [Physical Parameters](#physical-parameters)  
- [srv-ops01](#srv-ops01)  
- [srv-web01](#srv-web01)  
- [srv-db01](#srv-db01)  
- [srv-mon01](#srv-mon01)  
- [host-01](#host-01)  

---

## Physical Parameters

Each VM has:

- 6 GiB RAM  
- 2 CPUs  
- 50 GB disk space  

## srv-ops01

- Operating system: Ubuntu Server 24.04.3 LTS (no GUI) 
- Hypervisor: VirtualBox  
- Network interfaces:  
  - **enp0s3** – NAT – DHCP – Internet access  
  - **enp0s8** – Internal Network – `192.168.50.11/24` – VirtualBox LAN  
  - **enp0s9** – Host-only/Isolated – `192.168.60.11/24` – VMware LAN  

## srv-web01

- Operating system: Ubuntu Server 24.04.3 LTS (no GUI)
- Hypervisor: VirtualBox  
- Network interfaces:  
  - **enp0s3** – Internal Network – `192.168.50.20/24` 
    - Gateway: `192.168.50.11`  
    - DNS: `[8.8.8.8, 1.1.1.1]`  

## srv-db01

- Operating system: Debian as Server 13 (with Gnome)  
- Hypervisor: VMware  
- Network interfaces:  
  - **ens33** – Internal Network – `192.168.60.20/24`  
    - Gateway: `192.168.60.11`  
    - DNS: `[8.8.8.8, 1.1.1.1]`  

## srv-mon01

- Operating system: CentOS Server 10 (no GUI)  
- Hypervisor: VMware  
- Network interfaces:  
  - **ens33** – Internal Network – `192.168.60.30/24`  
    - Gateway: `192.168.60.11`  
    - DNS: `[8.8.8.8, 1.1.1.1]`  

## host-01

- Operating system: Rocky Linux (desktop host) 10 (with Gnome)  
- Hypervisor: VMware  
- Network interfaces:  
  - **ens160** – Internal Network – `192.168.60.101/24`  
    - Gateway: `192.168.60.11`  
    - DNS: `[8.8.8.8, 1.1.1.1]`  


