# Ubuntu Server Provisioning Notes
> :calendar: *January 29, 2018*

These are my notes from provisioning a couple bare-metal servers running Ubuntu Server 16.04 LTS.

I decided to try [Packet](https://packet.net) and [Vultr](https://www.vultr.com), as they both have
provide the same experience as other cloud VPS providers, except with the benefit of running
bare-metal hardware with no hypervisor.

Packet has the best deal at the moment. You can get a 4-core Atom CPU, 8GB of RAM, and 80GB of SSD
storage for $36/mo, which is better than the $40 offerings at Digital Ocean.

Vultr currently only has one pricing tier, with more on the way. For $120/mo (regular price is
$300), you get a 4-core Xeon (8 with HyperThreading), 32GB of RAM, and 2 RAIDed 240GB SSDs. Also,
the Vultr machine has a 10GbE NIC. If you need that sort of power and speed, $120 is a steal. Vultr
gets their hardware from [Choopa](https://www.choopa.com).

For pricing reasons, I'm going to stick with Packet, but huge props to Vultr and I'm looking forward
to seeing their future bare-metal offerings.

The rest of this document will cover the steps I took to secure the server. I'm not a CISSP, but I
can say that these steps will give you a solid security foundation.

### Create a New `sudo` User

```bash
# The disabled-password flag allows you to skip adding a password when creating the user
# You'll need to add the NOPASSWD option to the user's `sudoers` file
λ adduser --disabled-password adam

λ usermod -aG sudo adam

λ su - adam
```

### Install the Micro Text Editor

```bash
# The Snap daemon may already be installed, but sometimes it is not
λ sudo apt-get install snapd

# Make sure /snap/bin is in your PATH
λ sudo snap install micro --classic
```

### Enable `NOPASSWD`

I recommend adding individual `sudoers` settings to files in the `sudoers.d` folder.

```bash
λ cd /etc/sudoers.d

λ sudo touch adam

λ sudo micro adam
```

**`/etc/sudoers.d/adam`**

```bash
adam    ALL=(ALL:ALL) NOPASSWD: ALL
```

### Create RSA Key

I recommend generating the key on your personal computer and saving it to Dropbox so you can access
it on all your computers.

Running this will by default create `~/.ssh/id_rsa`. I recommend giving it a new name so you don't
overwrite your existing `id_rsa` key - e.g., `user@host.pem`.

Also, the `.pub` key will have the user and hostname that created the key appended to it. I change
this to the user and hostname of the target server - e.g., `adam@macbook` becomes `adam@server`.

```bash
λ ssh-keygen
```

This also generates a `.pub` key that you need to paste into your `authorized_keys` file.

```bash
λ touch ~/.ssh/authorized_keys

λ micro ~/.ssh/authorized_keys
```

Finally, you'll get an error trying to use a key with liberal permissions.

```bash
# Run this on your personal computer (the one with the keys)
λ sudo chmod -R 600 ~/.ssh
```

### Configure `sshd_config`

Once you're done editing `sshd_config`, you need to restart the `ssh` service or the machine.

Vultr has a special in-browser terminal and randomly generated root password that you can use to
gain access to the machine in the event you lock yourself out. I recommend enabling 2FA on your
Vultr account to ensure nobody can access this.

I don't believe Packet has anything like this yet, but they do allow you to give them a RSA key for
the root account that will be added to the root `authorized_keys` file when the machine is booted
for the first time.

```bash
# Enable SSH over IPv4 only
# This goes under the ListenAddress keys
AddressFamily inet

# Disable root login (Vultr only)
# Vultr has an in-browser terminal connected directly to the machine that you can use if you lock
# yourself out
PermitRootLogin no

# Disable password authentication
# You only want to connect using RSA
PasswordAuthentication no
```

### Enable and Configure Firewall

I use `ufw` (Uncomplicated Firewall) as a front-end for `iptables`. You can certainly edit
`iptables` directly, but `ufw` makes it really easy.

By default, `ufw` blocks all incoming traffic and allows all outgoing traffic. You shouldn't need to
touch these.

I did lock myself out by messing with the default settings and the quickest way to fix it was to
uninstall `ufw` and delete the `/etc/ufw`, `/etc/default/ufw`, and `/var/lib/ufw` folders.

Make sure you allow SSH traffic before enabling `ufw`, otherwise you'll lock yourself out.

```
λ sudo apt-get install ufw

λ sudo ufw allow ssh

λ sudo ufw allow http

λ sudo ufw allow https

λ sudo ufw enable
```

### Install Fail2Ban

Fail2Ban monitors log files and adds rules to `iptables` to block IP addresses that exhibit
suspicious behavior.

By default, Fail2Ban has SSH monitoring enabled, so I run the default settings.

To edit Fail2Ban settings, you need to create a `/etc/fail2ban/jail.local` file. Do not edit the
default `jail.conf` file directly, as it will get overwritten during updates.

```bash
λ sudo apt-get install fail2ban
```

### Install `unattended-upgrades`

This package will install updates for you.

By default, the `xenial` and `xenial-security` packages will be updated. You can whitelist
additional repositories by uncommenting them.

It's worth mentioning that updates *could* break things, so use your best judgement.

One important setting is `Automatic-Reboot`. Make sure to set this to `false` and also
delete the `/var/run/reboot-required` and `/var/run/reboot-required.pkgs` files. You do not want
your production server rebooting unexpectedly.
