# srv-web01

- [Network Interface Configuration](#network-interface-configuration)  
- [System Version Check](#system-version-check)  
- [Network Information](#network-information)  

---

## Network Interface Configuration

- As with **srv-ops01**, create and edit the Netplan configuration file:

```bash
sudo vim /etc/netplan/01-netcfg.yaml
```

- Configuration (uses routes instead of deprecated gateway4):

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      addresses:
        - 192.168.50.20/24
      routes:
        - to: 0.0.0.0/0
          via: 192.168.50.11
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```

- Apply the configuration:

```bash
sudo netplan generate
sudo netplan apply
```

## System Version Check

```bash
cat /etc/os-release
```

## Network Information

- Show IP address and mask:

```bash
ip -br a
```

- Show default gateway:

```bash
ip route
```

- Show DNS configuration:

```bash
resolvectl status
```
