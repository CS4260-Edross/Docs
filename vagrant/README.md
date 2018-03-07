# Vagrant setup

## General

[Vagrant][vagrant] is a tool that helps with setting up identical virtual
machines. We will use it to manage the servers and test environments needed for
this class. Because the directory the `Vagrantfile` is located in is shared with
the guest we can install the `Vagrantfile` in the root directory of the code
base to give the virtual machine access to the code base.

* Useful Plugins
    * [vagrant-vbguest][vbguest] If VirtualBox is your provider this plugin
      keeps the guest additions up to date. Run `vagrant plugin install
      vagrant-vbguest` to install this plugin. When a box is fisrt provisioned
      this plugin makes sure the guest OS has the correct version of the
      VirtualBox guest additions installed for your host's version of
      VirtualBox.

## `perf.html` Project

[`perf.html`][perf] is a web-based front-end for performance tools. An
example of a back-end is the [Gecko Profiler Addon][gecko] for FireFox.

The development environment is based around a Node.js server managed by the Yarn
dependency manager all on Linux. It also appears to be using Circle-CI and
ES-Lint for DevOps. We need a Linux box with Node, Yarn, Circle-CI, and ES-Lint.

You can find our `perf.html` specific `Vagrantfile` [here][perf_vagrant].

Progress:

[x] Linux base box
[x] Node.js installation
[ ] Yarn installation
[ ] Circle-CI installation
[ ] ES-Lint installation
[ ] Other package installation
[ ] Automate test runs


[vagrant]: https://www.vagrantup.com/intro/index.html
[vbguest]: https://github.com/dotless-de/vagrant-vbguest
[perf]: https://github.com/devtools-html/perf.html
[gecko]:  https://github.com/devtools-html/Gecko-Profiler-Addon
[perf_vagrant]: ./perf.html/Vagrantfile
