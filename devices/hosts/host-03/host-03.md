# host-03

- [Hostname](#hostname)
- [Network Interface Configuration](#network-interface-configuration)
- [System Information](#system-information)

---

## Hostname

- Check the current hostname:

```bash
hostnamectl status
```

- Change the hostname:

```bash
sudo hostnamectl set-hostname 'new-name'
```

- Verify the change:

```bash
hostnamectl
hostname
```

- Edit the hosts file if needed:

```bash
sudo nano /etc/hosts
```

## Network Interface Configuration

> **Note:** After the interface is launched, the host should automatically establish a connection and obtain an IP address, gateway, and DNS server from the DHCP server. If this does not happen, the connection must be configured manually.

- Check connection name:

```bash
nmcli con show
```

- Set the interface to obtain an IP automatically via DHCP:

```bash
sudo nmcli con mod 'connection_name' ipv4.method auto
sudo nmcli con up 'connection_name'
```

- Verify the assigned IP, gateway, and subnet:

```bash
ip -br a
ip route
cat /etc/resolv.conf
```

- Test connectivity:

```bash
ping -c 3 192.168.60.11
ping -c 3 google.com
```

## System Information

```bash
cat /etc/os-release
```
