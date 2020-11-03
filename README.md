# Cedille BareMetal Cloud using MAAS and juju

## Dependencies

1. [libvirt](https://libvirt.org/)
2. [vagrant](https://www.vagrantup.com/downloads.html)
3. [vagrant-libvirt](https://github.com/vagrant-libvirt/vagrant-libvirt#installation)

### what can be done

- [x] Start MAAS controller(VM) `vagrant up maas`
- [x] When finished will be accessible on `http://192.168.50.99:5240/MAAS/` `username:cedille` `password:cedille`
- [x] Connect to MAAS controller for debug, example:

  - `vagrant ssh maas`
  - `sudo su`
  - `sudo dpkg-reconfigure maas-rack-controller` and add http://192.168.50.99:5240/MAAS/
  - `service maas-dhcpd status`

- [ ] Start a node `vagrant up` and try to boot it by network with PXE
