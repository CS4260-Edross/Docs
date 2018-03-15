# Vagrant setup

## General

[Vagrant][vagrant] is a tool that helps with setting up identical virtual
machines. We will use it to manage the servers and test environments needed for
this class. Because the directory the `Vagrantfile` is located in is shared with
the guest we can install the `Vagrantfile` in the root directory of the code
base to give the virtual machine access to the code base.

Vagrant needs to be installed before all of these can be done. You can get
instructions for installing Vagrant [here][vagrant_install].

You can get the `Vagrantfile`s either by cloning this git repo or by navigating
to the `Vagrantfile` on github, selecting Raw view, and doing your browser's
"Save As" to save it as `Vagrantfile` with no extensions.

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

### Progress

[✓] Linux base box<br/>
[✓] Node.js installation<br/>
[✓] Yarn installation<br/>
[ ] Other package installation<br/>
[ ] Automate test runs

### Getting Started

1. Clone the perf.html fork repository using git. The clone directory will now
   be referred to as `<perf>/`
2. Copy the [`Vagrantfile`][perf_vagrant] to `<perf>/Vagrantfile`
3. Edit `<perf>/.git/info/exclude` and add the lines `Vagrantfile`, `.vagrant`,
   and `ubuntu*.log` to the end (three lines).
    * This is because the provided `.gitignore` does not include settings for
      vagrant files. We don't want to accidentally commit our `Vagrantfile` and
      supporting log files to their repository and we also don't want to modify
      the `.gitignore` they provide
4. Run `vagrant up` from anywhere within `<perf>/`
5. Once this command finishes run `vagrant ssh` to connect to the guest OS
6. Run `cd /vagrant` to change to the shared folder
7. Edit server.js to change `"localhost"` to `"10.10.10.10"` on line 60
    * This will show up as a git change. Do Not commit it. This change is only
    for us.
8. Run `yarn install` to install the Yarn controlled dependencies

### Running Tests

1. Run through the Getting Started instructions.
2. Once `yarn install` is finished you can now run the various test suites
    * `yarn test-all` - Test all the things!
    * `yarn test` - Run the tests in [./src/test/].
    * `yarn lint` - Run prettier and and eslint to check for correct code formatting.
    * `yarn flow` - Check the [Flow types](https://flow.org/) for correctness.
    * `yarn license-check` - Check the dependencies' licenses.

### Running Server

1. Run through the Getting Started instructions
2. In Firefox on your host change the Gecko Profiler Addon preference for front
   end URL from `https://perf-html.io` to `http://localhost:4242`
3. On the guest run `yarn start` to start the server
4. Once the guest displays "webpack: Compiled Successfully" you can now use the server
    * Navigate to `http://localhost:4242` in a browser on your host to see the
      home page
    * Use the Gecko Profiler Addon tool to record a profile and open it in the
      configured url

### Example Files

#### `.git/info/exclude`

```
# git ls-files --others --exclude-from=.git/info/exclude
# Lines that start with '#' are comments.
# For a project mostly in C, the following would be a good set of
# exclude patterns (uncomment them if you want to use them):
# *.[oa]
# *~
Vagrantfile
.vagrant
ubuntu*.log
```

[vagrant]: https://www.vagrantup.com/intro/index.html
[vagrant_install]: https://www.vagrantup.com/intro/getting-started/install.html
[vbguest]: https://github.com/dotless-de/vagrant-vbguest
[perf]: https://github.com/devtools-html/perf.html
[gecko]:  https://github.com/devtools-html/Gecko-Profiler-Addon
[perf_vagrant]: ./perf.html/Vagrantfile
