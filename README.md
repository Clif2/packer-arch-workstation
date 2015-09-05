Packer Arch Workstation
=======================

This project was originally forked from [elasticdog/packer-arch](https://github.com/elasticdog/packer-arch),
which seemed to be the most popular [Packer](http://www.packer.io/) template to generate a
[Vagrant](http://www.vagrantup.com/) base box for [Arch Linux](https://www.archlinux.org/). The original
template was designed to replicate a [DigitalOcean](https://www.digitalocean.com/) Arch Linux droplet;
my own use case is to test my Puppet-based [archlinux-workstation](https://github.com/jantman/puppet-archlinux-workstation)
module ecosystem that I use to manage my desktop and laptop; as such, I've made some relatively
major changes.

This will eventually merge in some work from other forks and projects as needed:

* Forks of [elasticdog/packer-arch](https://github.com/elasticdog/packer-arch), namely [garsue/packer-arch](https://github.com/garsue/packer-arch), [joelnb/packer-arch](https://github.com/joelnb/packer-arch) and [pedromaltez/packer-arch](https://github.com/pedromaltez/packer-arch)
* [daimatz/arch64-packer](https://github.com/daimatz/arch64-packer), [medvid/arch-packer](https://github.com/medvid/arch-packer) and [takei-shg/arch64-packer](https://github.com/takei-shg/arch64-packer/tree/jdk)

Overview
--------

My goal was to roughly duplicate the attributes from a
[DigitalOcean](https://www.digitalocean.com/) Arch Linux droplet:

* 64-bit
* 20 GB disk
* 512 MB memory
* Only a single /root partition (ext4)
* No swap
* Includes the `base` and `base-devel` package groups
* OpenSSH is also installed and enabled on boot

The installation script follows the
[official installation guide](https://wiki.archlinux.org/index.php/Installation_Guide)
pretty closely, with a few tweaks to ensure functionality within a VM. Beyond
that, the only customizations to the machine are related to the vagrant user
and the steps recommended for any base box.

Usage
-----

### VirtualBox Provider

Assuming that you already have Packer,
[VirtualBox](https://www.virtualbox.org/), and Vagrant installed, you
should be good to clone this repo and go:

    $ git clone https://github.com/jantman/packer-arch.git
    $ cd packer-arch/
    $ packer build -only=virtualbox-iso arch-template.json

Then you can import the generated box into Vagrant:

    $ vagrant box add arch packer_arch_virtualbox.box

License
-------

The original upstream version of [elasticdog/packer-arch](https://github.com/elasticdog/packer-arch) is provided under the terms of the
[ISC License](https://en.wikipedia.org/wiki/ISC_license).

This version, and all of my modifications, are provided under the [GNU GPL v3 or Later](http://www.gnu.org/licenses/gpl-3.0.en.html).

Copyright &copy; 2013&#8211;2014, [Aaron Bull Schaefer](mailto:aaron@elasticdog.com).
Modifications Copyright &copy; 2015, [Jason Antman](mailto:jason@jasonantman.com).
