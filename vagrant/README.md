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
dependency manager all on Linux. Yarn handles all other dependencies. We need a
Linux box with Node, and Yarn.

You can find our `perf.html` specific `Vagrantfile` [here][perf_vagrant].

Progress:

[✓] Linux base box<br/>
[✓] Node.js installation<br/>
[✓] Yarn installation<br/>
[ ] Other package installation<br/>
[ ] Automate test runs

Usage:

1. Clone the perf.html fork repository using git. The clone directory will now
   be referred to as `<perf>/`
2. Copy the [`Vagrantfile`][perf_vagrant] to `<perf>/Vagrantfile`
3. Edit `<perf>/.git/info/exclude` and add the lines `Vagrantfile` and
   `ubuntu*.log` to the end (two lines).
    * This is because the provided `.gitignore` does not include settings for
      vagrant files. We don't want to accidentally commit our `Vagrantfile` and
      supporting log files to their repository and we also don't want to modify
      the `.gitignore` they provide
4. Run `vagrant up` from anywhere within `<perf>/`
5. Once this command finishes run `vagrant ssh` to connect to the guest OS
6. Run `cd /vagrant` to change to the shared folder
7. Run `yarn install` to install the Yarn controlled dependencies
8. Run `yarn start` to start the server
9. Connect to `http://localhost:4242` in a web browser on your host

[vagrant]: https://www.vagrantup.com/intro/index.html
[vbguest]: https://github.com/dotless-de/vagrant-vbguest
[perf]: https://github.com/devtools-html/perf.html
[gecko]:  https://github.com/devtools-html/Gecko-Profiler-Addon
[perf_vagrant]: ./perf.html/Vagrantfile
