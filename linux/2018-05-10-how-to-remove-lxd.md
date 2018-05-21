# How to Remove LXD
> :calendar: *May 10, 2018*

### Stop `systemd` Services

```bash
sudo systemctl stop lxcfs.service
sudo systemctl stop lxd-bridge.service
sudo systemctl stop lxd-containers.service
sudo systemctl stop lxd.socket
sudo systemctl stop lxd.service
```

### Delete LXD Packages

```bash
sudo apt-get remove --purge --auto-remove -y lxcfs lxd-client lxd
```

### Cleanup LXD Folders

Make sure services are gone:
  - `/etc/systemd/system/`

Make sure network interfaces are gone:
  - `/sys/devices/virtual/net/`
  - `/sys/subsystem/net/devices/`

Look in the following locations:
  - `/etc/systemd/system/`
  - `/sys/devices/virtual/net/`
  - `/sys/subsystem/net/devices/`
  - `/var/lib/`
  - `/var/log/`
