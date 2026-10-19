# PVE Sync services

This services allows to synchrorize resources (ISO and LXC templates) between all nodes inside a cluster. This way you can upload a resource into one node and make it available on the rest of them.

This is an **addon for Proxmox VE** for making work easier.

## Installation

**Note:** Ensure every node can ssh using public key and without any restrictions to each other nodes of the cluster.

### PVE-sync-iso

**Steps**

- Move "pve-sync-iso.service" to directory "/lib/systemd/system/"
- Move "pve-sync-iso" to directory "/sbin/"
- Reload Systemd services

Execute following commands:
```
$ install -u root -g root -m776 pve-sync-iso.service /lib/systemd/system/
$ install -u root -g root -m776 pve-sync-iso /sbin/
$ systemctl daemon-reload
```

Finally, run on every node:
```
$ systemctl enable --now pve-sync-iso
```

### PVE-sync-lxc

**Steps**

- Move "pve-sync-lxc.service" to directory "/lib/systemd/system/"
- Move "pve-sync-lxc" to directory "/sbin/"
- Reload Systemd services

Execute following commands:
```
$ install -u root -g root -m776 pve-sync-lxc.service /lib/systemd/system/
$ install -u root -g root -m776 pve-sync-lxc /sbin/
$ systemctl daemon-reload
```

Finally, run on every node:
```
$ systemctl enable --now pve-sync-lxc
```

## Usage

When service is running, it detect automatically if a new resource was uploaded on the node, then it spread the new resource to the other nodes of the cluster using an ssh connection.

If a resource is deleted from one node, it is also erased from the other nodes of the cluster.

## Compatibility

This services was tested successfully on ProxMox VE 9.

Previous versions of ProxMox was not tested, however, if resources are stored in the same path and pve cluster commands (pvecm nodes) behaves equal, it can work. Test it with caution.