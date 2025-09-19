# srv-web01

- [Network Interface Configuration](#network-interface-configuration)  
- [System Version Check](#system-version-check)  
- [Network Information](#network-information)  
- [Nginx Installation & Configuration](#nginx-installation-&-configuration)
- [Creation of user for website development](#creation-of-user-for-website-development)

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

## Nginx Installation & Configuration

- Install Nginx:

```bash
sudo apt update
sudo apt install nginx -y
```

- Verify the installation:

```bash
systemctl status nginx
```

- Create site file in nginx:

```bash
sudo vim /etc/nginx/sites-available/homelab-webapp
```

Configuration:

```nginx
server {
    listen 80;
    server_name _;

    root /var/www/html/homelab-webapp;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

- Turn on configuration:

```bash
sudo ln -s /etc/nginx/sites-available/homelab-webapp/ \
/etc/nginx/sites-enableled/
```

- Disable default configuration:

```bash
sudo rm /etc/nginx/sites/enabled/default
```

- Test and reload Nginx:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## Creation of user for website development

- Create user:

```bash
sudo adduser homelab-deployer

# Needed password
# Nice to add Company name, phone numer etc.
```

- Add developer user to default group of nginx:

```bash
sudo usermod -aG www-data homelab-deployer
```

- Set correct permissions:

```bash
sudo chown -R root:www-data /var/www/html
sudo chmod -R 775 /var/www/html
```

> Explanation:
> 
> * We do not change owner of /var/www/html, only give deployer/group proper write access.

- Check permissions:

```bash
ls -ld /var/www/html
```
