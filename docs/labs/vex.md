# Building a Juniper vEX

Juniper vEX is supported by the **netlab libvirt package** command. To build a vEX box:

* Create an empty directory on a Ubuntu machine with *libvirt* and *Vagrant*.
* Download vEX disk image (.qcow2 file) into that directory
* Execute **netlab libvirt package vex _virtual-disk-file-name_** and follow the instructions

```{warning}
* The **‌netlab libvirt package vex** command has been tested on Ubuntu 20.04 LTS and 22.04 LTS and might not work on other Linux distros.
* On Ubuntu 22.04 LTS, `libvirt-qemu` user needs read and execute access to the VM disk file. It's easiest if you create Vagrant boxes in a subdirectory of the `/tmp` directory.
```

## Preparing the Box Configuration

Initial device configuration is copied from an ISO image created by the installation process. You'll have to save it and shut down the VM. **netlab libvirt config vex** command displays the build recipe (based on the [recipe published by Brad Searle](https://codingpackets.com/blog/juniper-vex3-0-vagrant-libvirt-box-install/)):

```{eval-rst}
.. include:: vex.txt
   :literal:
```

## Notes on Using vex Box

The *netlab* Vagrant template for vex uses *default\_prefix* libvirt parameter to set the domain (VM) name.

The template has been tested with Vagrant version 2.2.14. Some earlier versions of Vagrant generated VM names using a slightly different algorithm (the underscore between _default\_prefix_ and VM name was added automatically) and might thus generate an unexpected VM name. To fix that problem remove parts of **vex-domain.j2** template:

* Remove _domain.default\_prefix_ parameter (default value should generate the expected VM name)
