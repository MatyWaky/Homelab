# srv-ops01

- [Hostname](#hostname)  
- [Network Interfaces](#network-interfaces)  
- [Routing](#routing)  

---

## Hostname

- Check the current hostname:

```bash
hostname
```

- Temporary change of hostname (until reboot):

```bash
sudo hostname 'new-name'
```

- Permanent change of hostname:

```bash
sudo vim /etc/hostname
sudo vim /etc/hosts
```

## Network Interfaces

- Show list of interfaces with details:

```bash
ip -c a
```

- Create a Netplan configuration file:

```bash
sudo vim /etc/netplan/01-netcfg.yaml
```

- Configuration:

> ⚠️ Important: Indentation must use spaces, not tabs. Each nested level = 2 spaces.

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: true
      nameservers:
        addresses: [1.1.1.1, 8.8.8.8]

    enp0s8:
      addresses:
        - 192.168.50.11/24

    enp0s9:
      addresses:
        - 192.168.60.11/24
```

- Adjust file permissions:

```bash
sudo chmod 600 /etc/netplan/01-netcfg.yaml
```

- Apply changes:

```bash
sudo netplan generate
sudo netplan apply
```

- Test connectivity:

```bash
ping -c 3 8.8.8.8
ping -c 3 1.1.1.1
ping -c 3 google.com
```

## Routing

- Enable IPv4 forwarding:

```bash
sudo vim /etc/sysctl.conf
```

Uncomment or add the following line:

```textile
net.ipv4.ip_forward=1
```

- Apply changes:

```bash
sudo sysctl -p
```

- Configure NAT (masquerading):

```bash
sudo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
sudo iptables -t nat -L -n -v
```

- Make iptables rules persistent:

```bash
sudo apt install iptables-persistent -y
sudo netfilter-persistent save
```

- Allow packet forwarding between internal networks:

```bash
sudo iptables -A FORWARD -i enp0s8 -o enp0s9 -j ACCEPT
sudo iptables -A FORWARD -i enp0s9 -o enp0s8 -j ACCEPT
sudo iptables -L -n -v
sudo netfilter-persistent save
```
