# ArchLinux for oVirt Packer Configuration
This repository contains [Packer][packer] configuration and [Ansible][ansible]
scripts to create a base [ArchLinux][arch-linux] image for use on oVirt/QEMU. It
includes the bare minimum of additional software beyond [cloud-init][cloud-init],
[ovirt-guest-agent][ovirt-guest-agent], and the [AUR][aur] helper [yay][yay].

The configuration pattern is cribbed heavily from [elasticdog/packer-arch][packer-arch]
but reorganized and reimplemented in Ansible to better support my own workflow.

## Overview
The default configuration is as follows:

* 1CPU
* 512MB RAM
* 8GB disk
* LVM configured with a single PV and VG
* Single root LVM partition formatted ext4
* No swap
* Includes `base` and `base-devel` package groups

## Usage
This configuration assumes that you have [Packer][packer], [Ansible][ansible],
and [QEMU][qemu] installed and configured on your local system. I am building
on [ArchLinux][arch-linux] so generally this will be tested against the latest
versions available there. To build:

```bash
$ git clone https://github.com/aetherith/packer-ovirt-arch.git
$ cd packer-ovirt-arch
$ cp ~/.ssh/id_rsa.pub ./srv/ssh.pub
$ packer build config.json
```

As configured the default user is `admin` and the only way to login is to use the
SSH key specified at creation.

[packer]: https://packer.io/
[ansible]: https://www.ansible.com/
[arch-linux]: https://www.archlinux.org/
[cloud-init]: https://cloudinit.readthedocs.io/en/latest/
[ovirt-guest-agent]: https://www.ovirt.org/develop/developer-guide/vdsm/guest-agent.html
[aur]: https://aur.archlinux.org/
[yay]: https://github.com/Jguer/yay
[packer-arch]: https://github.com/elasticdog/packer-arch
[qemu]: https://www.qemu.org/
