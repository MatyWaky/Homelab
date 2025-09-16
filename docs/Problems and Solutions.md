# Problems and Solutions



## Problem: Cannot boot CentOS, Rocky Linux, Debian on VirtualBox

- **Cause:** VirtualBox has compatibility issues with Ryzen 7800X3D CPU; some virtualization features may not work correctly.
- **Solution:** Install these systems on VMware instead.

## Problem: Gray screen during Rocky Linux installation

- **Cause:** Graphics/3D acceleration conflicts with VirtualBox on certain CPUs.
- **Solution:** Disable 3D Acceleration in VM settings.

## Problem: Cannot ping by hostname

- **Cause:** DNS addresses not configured.
- **Solution:** Add DNS addresses: `8.8.8.8`, `1.1.1.1`.

## Problem: `srv-ops01` does not boot

- **Cause:** Likely misconfiguration of network interfaces in netplan (wrong indentation, missing `netplan generate/apply`).

- **Solution:** Temporarily move the netplan config and recover:
  
  1. Press **Shift** during VM start (after VirtualBox logo)
  
  2. Go to **Advanced → Recovery**
  
  3. Open terminal and run:
     
     ```bash
     mv /etc/netplan/01-netcfg.yaml /root/
     reboot
     ```
  
  4. Restart the VM and restore the file.
     
     ```bash
     sudo mv /root/01-netcfg.yaml /etc/netplan/
     sudo netplan generate
     sudo netplan apply
     ```

## Problem: `gateway4` in netplan configuration is deprecated

- **Cause:** `gateway4` is no longer recommended in newer Netplan versions.
- **Solution:** Use `routes` instead (example in `srv-web01` configuration).

## Problem: DNS not added in CentOS connection configuration

- **Cause:** DNS not configured when adding static connection via `nmcli`.

- **Solution:** Update connection and restart it:
  
  ```bash
  sudo nmcli con mod static-ens33 ipv4.gateway 192.168.60.11
  sudo nmcli con down static-ens33
  sudo nmcli con up static-ens33
  ```
