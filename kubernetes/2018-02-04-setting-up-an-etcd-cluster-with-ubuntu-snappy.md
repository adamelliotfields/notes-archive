# Setting Up an ETCD Cluster with Ubuntu Snappy
> :calendar: *February 4, 2018*

There are a few different ways to install ETCD - `apt`, `snap`, and the recommended way by
downloading the binary from GitHub.

The first and most obvious way would be `sudo apt-get install etcd`. Unfortunately, the repository
hasn't been updated in a while, so you'll be stuck with v2. Unfortunately, the default storage layer
in Kubernetes 1.6 is ETCD v3.

The recommended way is to download the tarball from GitHub Releases and either run manually or
create a `systemd` service to launch at boot.

It appears that Canonical (specifically Tim Van Steenburgh - @tvansteenburgh) is maintaining a Snap
for ETCD, presumably to be used with their Juju deployment tool. I really like using Snaps whenever
possible, so I decided to try this method.

To start, I created 3 Ubuntu 16.04 Server virtual machines on a NAT network. I'm on Windows and
using VMware Workstation, but this should work on a Mac using Parallels.

As this was done locally, additional steps would be necessary for securing your servers in live
environment. The benefit of doing it locally is that you can figure out what steps need to be taken
to get a working ETCD cluster without incurring the costs of paying for servers on DigitalOcean.

### Log Into Each Machine

Before SSHing into your VMs, log in using the remote terminal (the window launched by VMware).

You'll need to install `openssh-server` at the very least (my distribution did not install it by
default).

Run `ip address` to list your IPv6 address for each VM.

### Check Your Network

You should be able to ping all of your VMs from your host.

```bash
λ ping 192.168.58.100

λ ping 192.168.58.101

λ ping 192.168.58.102
```

### SSH into Each VM and Install ETCD

Open 3 tabs in your favorite terminal emulator and SSH into each machine. Install the ETCD snap:

```bash
sudo snap install etcd --classic
```

This will install ETCD and create the data directory. Snap will also create the `systemd` service,
but it wont run because it has no configuration file yet.

A sample config is available at `/snap/etcd/current`. The service will look for
`/var/snap/etcd/common/etcd.conf.yml`. Copy the sample:

```bash
sudo cp /snap/etcd/current/etcd.conf.yml.sample /var/snap/etcd/common/etcd.conf.yml
```

You can now configure ETCD to use your cluster's IP addresses. Edit this on each VM (you can leave
the existing keys as defaults):

```yaml
# The human-readable name for each cluster member
# i.e., etcd-node-01, etcd-node-02, etc
name: 'etcd-node-01'

# List of comma separated URLs to listen on for peer traffic
# Default is port 2380
listen-peer-urls: http://192.168.58.100:2380

# List of comma separated URLs to listen on for client traffic
# You must also include the localhost IP for etcdctl to work
# Default is port 2379
listen-client-urls: http://192.168.58.100:2379,http://127.0.0.1:2379

# List of this member's peer URLs to advertise to the rest of the cluster
initial-advertise-peer-urls: http://192.168.58.100:2380

# List of this member's client URLs to advertise to the public
advertise-client-urls: http://192.168.58.100:2379

# Initial cluster configuration for bootstrapping
initial-cluster: 'etcd-node-01=http://192.168.58.100:2380,etcd-node-02=http://192.168.58.101:2380,etcd-node-03=http://192.168.58.102:2380'

# Initial cluster token for the etcd cluster during bootstrap
initial-cluster-token: 'etcd-cluster'

# Initial cluster state ('new' or 'existing').
initial-cluster-state: 'new'

# Reject reconfiguration requests that would cause quorum loss.
strict-reconfig-check: true
```

Once you've finished configuring each VM, you can start the service on each machine:

```bash
sudo systemctl restart snap.etcd.etcd.service
```

You should now be able to run `etcdctl cluster-health` and see that your cluster is healthy.

Check out the [admin guide](https://coreos.com/etcd/docs/latest/v2/admin_guide.html) for more
information.
