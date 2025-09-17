# host-01

- [Hostname](#hostname)
- [Network Interface Configuration](#network-interface-configuration)
- [System Information](#system-information)
- [Network Information](#network-information)

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

- Add a new static connection:

```bash
sudo nmcli con add type ethernet ifname ens160 con-name static-ens160 \
  ipv4.addresses 192.168.60.101/24 \
  ipv4.gateway 192.168.60.11 \
  ipv4.dns "8.8.8.8 1.1.1.1" \
  ipv4.method manual
```

- Enable the profile:

```bash
sudo nmcli con up static-ens160
```

- Verify configuration:

```bash
nmcli con show static-ens160
ip a
ip route
```

## System Information

```bash
cat /etc/os-release
```

## Network Information

- Show IP and mask:

```bash
ip -br a
```

- Show default gateway:

```bash
ip route
```

- Show DNS configuration:

```bash
cat /etc/resolv.conf
```
