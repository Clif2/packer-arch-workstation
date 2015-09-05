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
* Perhaps some of the work from [terrywang/vagrantboxes](https://github.com/terrywang/vagrantboxes/blob/master/archlinux-x86_64.md)

Status
------

Puppet:

My original install instructions mentioned AUR requirements of ``ruby-augeas`` and ``ruby-r10k``. The [ruby-r10k package](http://webcache.googleusercontent.com/search?q=cache:TI4BTNXI_TYJ:https://aur4.archlinux.org/packages/ruby-r10k/+&cd=1&hl=en&ct=clnk&gl=us)
had no maintainer and is now gone from AUR (and, as far as I can tell, the pkgbuild with it). I'm not yet sure if puppet 4 (in the community repo) still requires [ruby-augeas](https://aur.archlinux.org/packages/ruby-augeas/). We won't need r10k, as that can be done on the host.

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

## Requirements

This project uses Ruby/Rake to manage building; you'll need to have ruby and [bundler](http://bundler.io/) installed.

To get started:

    $ git clone https://github.com/jantman/packer-arch-workstation.git
    $ cd packer-arch-workstation/
    $ bundle install --path vendor

### VirtualBox Provider

Assuming that you already have Packer,
[VirtualBox](https://www.virtualbox.org/), and Vagrant installed, you
should be good to clone this repo and go:

    $ rake build

Then you can import the generated box into Vagrant:

    $ vagrant box add arch packer_arch_virtualbox.box

License
-------

The original upstream version of [elasticdog/packer-arch](https://github.com/elasticdog/packer-arch) is provided under the terms of the
[ISC License](https://en.wikipedia.org/wiki/ISC_license).

This version, and all of my modifications, are provided under the [GNU GPL v3 or Later](http://www.gnu.org/licenses/gpl-3.0.en.html).

Copyright &copy; 2013&#8211;2014, [Aaron Bull Schaefer](mailto:aaron@elasticdog.com).
Modifications Copyright &copy; 2015, [Jason Antman](mailto:jason@jasonantman.com).
