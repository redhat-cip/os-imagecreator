# os-imagecreator

## Abstract

It consists of a simple set of script dedicated to automate the creation of OpenStack image:

* It includes cloud-init
* It produces image for KVM hypervisor
* It supports debian and centos
* It works in update mode, ie if the images is up-to-date is it leave as-is, if update available the image is rebuild

Planned features:

* Image validation (upload, boot, ping, ssh, destroy)
* Image upload (only if updated, will use glance checksum to test if upload is required)

## Requirements

* Debian jessie (may work on debian wheezy) with:
```
apt-get install -y openstack-debian-images git dpkg-dev debhelper python-all libvirt-bin supermin

apt-get install -y libguestfs-tools

apt-get -y install kvm # if you have hardware virtualization assistance available and enabled

and/or

apt-get -y install qemu
```
* Working oz and dependencies (https://github.com/clalancette/oz)
```
git clone https://github.com/clalancette/oz.git
cd oz
dpkg-buildpackage
dpkg -i ../oz*.deb
apt-get install -f -y
```

## Usage
### Quickstart
* Check requirements
* Git clone
```
git clone https://github.com/enovance/os-imagecreator.git
```
* Fire up
```
cd os-imagecreator

./generate_images
```

### Add an image

Just go inside ./images there is one directory per image. There is two (more can easily be added) kind of image: debian (use the openstack-debian-images) and oz (support a wide range of linux and other os).


## Troubleshooting

If you get error like "Permission denied" when Oz is called ensure the libvirt user is allowed to walk through the path where you are building your images.
