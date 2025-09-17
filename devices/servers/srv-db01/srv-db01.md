# srv-db01

- [Network Interface Configuration](#network-interface-configuration)  
- [System Information](#system-information)  
- [Network Information](#network-information)  

---

## Network Interface Configuration

- Edit the `interfaces` file:

```bash
su -
nano /etc/network/interfaces
```

Configuration:

```textile
auto ens33
iface ens33 inet static
    address 192.168.60.20
    netmask 255.255.255.0
    gateway 192.168.60.11
    dns-nameservers 8.8.8.8 1.1.1.1
```

- Restart networking services:

```bash
systemctl restart networking
```

- Edit the `resolv.conf` file:

```bash
nano /etc/resolv.conf
```

Configuration:

```textile
nameserver 8.8.8.8
nameserver 1.1.1
```

## System Information

- Check system version:

```bash
lsb_release -a
```

- Check desktop environment:

```bash
echo $DESKTOP_SESSION
# or
echo $XDG_CURRENT_DESKTOP
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
