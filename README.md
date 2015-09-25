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

Download
--------

If you just want to use this box for Vagrant/VirtualBox, you can use it from [Atlas](https://atlas.hashicorp.com/jantman/boxes/packer-arch-workstation):

    vagrant init jantman/packer-arch-workstation; vagrant up --provider virtualbox

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
